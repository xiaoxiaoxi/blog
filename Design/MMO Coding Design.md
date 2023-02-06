# MMO Coding Design Series 1: Basic Overview

by [Taylor](http://taylorroberthill.com/GameDevStation/author/taylor/)



MMO design is hard. Really hard. There’s no sugar-coating it–if you decide to roll your own server code, you will spend a *lot* of hours doing so, and most of that time will be spent debugging.

That said, since you are here to begin with, you probably have an interest in the topic, and me telling you it is hard should not dissuade you. It can be really rewarding during those eureka moments.

First you should have an understanding of what the heck we’re trying to accomplish with all this. In the early days of networking, games took the obvious approach to networking: when your character moves, propagate that change to the other machines connected to the game. It’s simple and dirty, but is not used because of how easy that is to hack. While the client can do error checking, it’s just not secure enough. There’s also the problem of the game state being out of sync for each machine–if your machine says you hit someone, but your opponent’s machine disagrees, who is right? Technically, they’re *both* right, and we can’t have that.

In the 90s, a new system became prevalent: the server-client paradigm. In this solution each client sends their data to a master server, which then calculates whether what the player did is correct and proper. If so, it updates the world locally, takes a snapshot, and sends it to the rest of the players at regular intervals. While players may receive packets at different rates, having an authoritative server eliminates many of the “who is right” scenarios and centralizes all the big number crunching, reducing the processing load on less endowed computers.

This is the approach that is prevalent today in gaming, and is the one we will be focusing on. This is not so much a tutorial with code examples as it is a high-level discussion of the systems that must be in place for an MMO to work with a half-decent design. For everything I say here, there will be a hundred exceptions, or a thousand reasons why this specific feature won’t work in someone’s game–and that’s ok. This is intended solely to get you thinking about the design requirements of a scalable MMO.



# MMO Coding Design Series 2: Network Protocols

by [Taylor](http://taylorroberthill.com/GameDevStation/author/taylor/)

 

**PREVIOUS: [Basic Overview](http://taylorroberthill.com/GameDevStation/2015/04/27/mmo-coding-design-series-1-basic-overview/)
NEXT: \**[Packet Structure & Entity System](http://taylorroberthill.com/GameDevStation/2015/04/28/mmo-coding-design-series-2-packet-structure-entity-system/)\**[
](http://taylorroberthill.com/GameDevStation/2015/04/27/mmo-coding-design-series-1-basic-overview/)**

One of my earlier self-guided projects was to create a Java-based MMO server. The first iteration was nothing fancy; it was a server that opened sockets with clients, then blasted them with as many packets as they could handle under the theory that the player’s data should always be up to date as much as possible. This often led to situations where the client had more packets than it could process–if one packet took too long, the program had a hard time recovering and getting ahead again, eventually causing a stack overflow as the packets mounted over time.

This first version also had so many instances of naivete (which is understandable, as there are very few resources on the topic) and premature optimization that it eventually caused me to completely trash everything I had written (though I have rewritten it a few times for fun since–I became a much better programmer in the interim!).

Since then, I’ve had a few more years of research to approach the problem with a more refined methodology. Here’s a few of the things I’ve learned, spread out over a series of posts, aimed to help others produce kickass games for me to play.

**UDP vs TCP**

We will start off slow. Which protocol do we choose to transfer the data? First I will explain the difference.

**UDP** is a very basic way to send data. The sender basically says “I’m going to send this data and I don’t care what happens after that.” It has an address where it drops off the data, and then it dies. If a message is split into multiple packets, and the second arrives before the first, too bad–you either have to find a way to make sense of it yourself, or forget about it entirely. In addition, UDP packets may not arrive at all. There is no guarantee for anything.

**TCP** is the protocol that the internet is largely based on. It was designed originally to solve the problem of packets arriving out of sync, or being lost in the maelstrom of the series of tubes we call the internet. Each packet has metadata associated with it that tell the receiver to put it back into the correct order, and then calls home to say it was received. As such, it has a higher overhead, both in packet size and processing requirements.

The correct answer for which protocol you should use depends on the nature and size your game, of course, but since I am focusing on AAA blockbuster MMOs, the real correct answer is both. When a user sends a chat message, you don’t want that data to be lost under any circumstance, ever. This means TCP should be used for objects whose delivery is necessary. But when a player moves, the client is sending that data over and over and over. If a packet is lost, who really cares? The new position will just be sent again in a fraction of a second. If the data is not necessarily important or is highly repetitive, use UDP.

For the early stages of game design, I recommend starting only with TCP in your networking code because it is a little easier to manage and debug in most cases. When you become a AAA blockbuster MMO, then you can transition to UDP to lessen the load on your servers.

# MMO Coding Design Series 3: Packet Structure & Entity System

by [Taylor](http://taylorroberthill.com/GameDevStation/author/taylor/)



**PREVIOUS: [\**Network Protocols\**
](http://taylorroberthill.com/GameDevStation/2015/04/28/mmo-coding-design-series-1-basic-network-protocols/)NEXT: \**[Managing Client Connections](http://taylorroberthill.com/GameDevStation/2015/04/28/mmo-design-coding-series-3-packet-transmission-delta-compression/)\**
**

Now that we understand how the data will be traveling, we need to understand how to *create* that data. A little bit of planning here goes a long way, and there really is no right answer, but there are a heck of a lot of wrong ones, as I’ve found.

The approach that I ultimately took was based on World of Warcraft’s packet structure. Here I will give a simplified overview for how they work. In reality, it is quite a bit more complex, with layers of encryption and custom bit-packing, but most of the complexity is specific to WoW and is unnecessary for our design.

**WoW Packets**

There are two parts to a packet: the header and the body. The header has all the metadata, such as where it came from, who it is intended for, and so on.

In our server, the recipient and sender should be a unique key that is assigned to that connection upon login. This is for two reasons: security and centralization. It is always a good idea to hide identifying information about a player, as any hacker will take a mile if given an inch. Second, for the same reason you would never use someone’s first name or phone number as a primary key in a database, you should never use their IP address or anything other than a master identifier because it can change (even if it shouldn’t–it can. In my professional life this has been a nightmare). And if you centralize your data using this key, it means the same thing to every part of the program, whereas an IP address should conceptually mean nothing to your game logic.

The second part of the packet is the body. This is the means by which your two endpoints manipulate the other. Each body contains an opcode, which maps to a command. These opcodes are actually hex codes, but they map to strings that we can understand, which I believe were uncovered from resources in the WoW binaries. Let’s use CMSG_LEARN_SPELL as an example ([here ](http://www.pxr.dk/wowdev/wiki/index.php?title=Opcodes)is a full list). The first four characters of an opcode tells us which end of the connection sent it: a CMSG for client, an SMSG for server, or just MSG when it doesn’t matter. After the underscore is the command. In this case, the player has visited a trainer and upgraded a skill on the client side. A packet with this character’s unique identifier is sent to the server with the opcode in its body, followed by the spell the player clicked on. The server then processes this command by checking to see if the player is within range of a trainer and has the dialog open, then updates the player model with that spell. A sent back to the client, which causes its UI and player model to update.

**Design Requirements**

Now that we have a little understanding of how WoW’s packets work, we can distill them down into a series of requirements that we can use to design the objects that our packets will interact with.

Each object must:

- Understand a common lexicon of opcodes and manipulate the world model (or decline from doing so) based on these codes.
- Understand its relationship to other objects through a set of rules.
- Have unique identifying information which can be used to specify targets in opcodes.

The general idea for the first point is that a single **Entity** class will be the superclass for all objects in the world. It will have overridable methods that govern how each object’s opcodes interacts with the world model. For example, a **Player** and a **Horse** might both derive from **Entity**. If a packet with the opcode SMSG_LEARN_SPELL comes addressed to the **Player** entity, the **Player** entity will have overridden the **SMSG_LEARN_SPELL(Spell spellName)** method to check if the player is in range of a trainer, and then to add the spell to that player’s model. However, if the packet arrives addressed to the **Horse**, the horse will not have overridden the method, and nothing will happen (or it will be logged for later examination–a horse should probably not be receiving those packets to begin with). This means we can add opcode methods to **Entity** as we please and only override the method in classes who care about its functionality.

The second point will be a bit trickier. The **Entity** class will have a property called **Rules** that contains a list of rules that can be added or removed at runtime. Each **Rule** will implement an interface **IRule**. On this interface will be a **CalculateRule(Entity entity, Entity entity)** method that will return a **RuleResult** object that contains data about what happened during the compare, which can then be used by whomever invoked the rule.

For example, if a player bumps into a wall, the collision triggers the **Collision** rule on the player (and the wall, but the wall doesn’t care what bumps into it, so it probably would do nothing). This calls **Collision.CalculateRule(myPlayerEntity, wallEntity).** A **RuleResult** is returned with some data that says “Player, you can’t pass through here.” The section of the logic that was in charge of moving the player into the wall then stops the player from moving further.

The last point is pretty straightforward. To have an opcode manipulate the world, we need the world’s entities to have identifying information. This can be a guid, integer, whatever you would like to use.

So that’s how I organize the entities. Now that we have a way to structure how our server operates, we now need a way to send the data in a meaningful way that avoid blasting the client with superfluous information.

# MMO Design Coding Series 4: Managing Client Connections

by [Taylor](http://taylorroberthill.com/GameDevStation/author/taylor/)



**PREVIOUS: [Packet Structure & Entity System
](http://taylorroberthill.com/GameDevStation/2015/04/28/mmo-coding-design-series-2-packet-structure-entity-system/)NEXT: [Delta Compression & Lerping](http://taylorroberthill.com/GameDevStation/2015/04/28/mmo-coding-design-series-4-delta-compression-lerping/)
**

We last discussed the design of a system to manipulate our world model using opcodes. Before we continue on to transmitting this data, we need to figure out how to handle arbitrarily many connections.

In part 1, I suggested sticking with TCP in the early stages of development. While it really shouldn’t make much of a difference in terms of design-from-above, as we are doing, I still want to mention that debugging in early stages of development will be easier doing it this way. UDP can always be added later, but knowing that your obscure bugs aren’t stemming from dropped packets is huge. This is a great example of premature optimization.

Handling connections is a bit tricky, I’ve found. The problem is one of concurrency. Handling multiple sockets at once is a multi-threaded affair, and this can be intimidating for devs who rarely have to deal with this realm of programming. Let’s say we have 100 players. These players each have a socket that is receiving data. However, not all of these sockets are receiving or sending at the same time, and are idle the majority of their existence. How do we allocate our precious processing time to eliminate wasted cycles?

There are a million suggestions online, and I will begin with the easiest and least scalable (though tens of players should be no problem whatsoever on a multi-core processor). This is the way I did it for my first iteration, and I wouldn’t write it off in the early stages of development (or even into production. Refactoring can be done later when you anticipate hitting these limits, or when you get to the stage where load balancing comes into play, a topic which I hope to cover in this series).

The first approach is to simply create two new threads for each socket: one for listening and one for sending. Inside each thread you can create an object whose sole purpose is to wait for data to process (and blocking the thread in the process, which makes this the easy approach). However, the cost of this approach is significant: each time a thread awakens, cycles are lost by switching contexts. In my earlier iterations, I started hitting these limits around 500 simultaneous connections (though this was sending lean packets at a *very* liberal rate; your mileage may vary. Most games will not even reach this number of concurrent users. These numbers are largely useless for your game, however, and included running the IDE, debugger, and probably Spotify and other unnecessary junk). Of course the machine running your server and the content of your packets make all the difference in this case.

The second way to do this is to create a limited number of threads and reuse them in a smart way. The common term for this collection of threads is a Thread Pool. Check your language to see if it has built-in functionality. Java has ThreadPoolExecutor, .NET has both thread pooling and the **async** / **await** keywords built into the language. Since those are my two primary languages, I cannot, unfortunately, offer recommendations for C/C++ or others. This was a bit of a chore to implement, and had I scaled higher, I’m sure the benefits would have been great–but I never did, so it was not worth the extra hassle of making everything run beautifully.

Whichever way you decide to manage your threads, the end result must be a wrapper around the socket that facilitates sending and queuing data that has two queues: one for incoming packets and one for outgoing packets. These queues must be blocking; if user 23 sends a packet to the server and its wrapper is already putting it into the incoming queue, and 54 does the same, we want 54 to wait until 23 is done, rather than throwing an exception or just deleting the data. Basically, you want blocking queues and thread safe data structures *everywhere.* If you do not, you will run into issues.

Using these tips, you want to structure your networking manager like a thread funnel. Consolidate the data from each of these threads/pools that are communicating constantly with their clients into one thread whose only job is to feed incoming packets to the logic layer and vice versa. This allows the meat of your server full separation from the multi-threaded complexity inherent in networking.

As far as authentication/logging in goes, the approach many AAA games use is to have a separate login server that has its own backdoor to the database. The user types their username and password, the client sends it off to the authentication server, the server verifies its authenticity, and then returns a unique key to the client. This key is also recorded in the database. Then the client sends another request to the main server using this key, and all communication happens based on this key. If the session dies for any reason, this key is cleared from the database, and further communication is impossible because it was the only link between the client and the user’s data.

# MMO Coding Design Series 5: Delta Compression & Lerping

by [Taylor](http://taylorroberthill.com/GameDevStation/author/taylor/)



**PREVIOUS: [Managing Client Connections
](http://taylorroberthill.com/GameDevStation/2015/04/28/mmo-design-coding-series-3-packet-transmission-delta-compression/)NEXT: [World Model](http://taylorroberthill.com/GameDevStation/2015/04/29/mmo-coding-design-series-6-world-model/)
**

Now that we can manage arbitrarily many connections, how do we go about sending data, and what data do we send? The obvious conundrum is the sheer quantity of data we need to keep track of. Think about World of Warcraft and its ten million players. Even split into multiple realms, that is a ***massive*** amount of data. How does everything keep in sync?

Enter the concept of *delta compression.* Think back to high school physics: delta means change. At a glance, it means to send only the changes to the client, and let the client figure out where to put things.

When the user first logs in, we want to send our entire world state (or at least the parts our client cares about at this moment; we don’t need to know what’s happening in Azerbaijan when we’re running a marathon in Boston, and neither do your players). The world state is sent by going through every object in the “world container” (a collection of Entities, which we will go more into later) and creating a packet representing its state, then sending it to the client.

After that it gets a little more tricky. Before we can determine the changes, we need to set our bounds. At regular intervals, we take a snapshot of the world to freeze as our current state, then compare this with the previous snapshot. We iterate through every single object and find the differences (or, alternatively and more efficiently, whenever something changes we set a “dirty” flag on that object, and then simply iterate through the dirty objects. This prevents us from going through AFK players or objects that have been left on the ground to expire). These differences are converted to opcodes, then packets, and then sent to the client. This process happens many times a second, and the type of game determines the frequency: an MMO such as WoW needs fewer snapshots than a fast-paced shooter like Call of Duty.

Also note that you need to filter out packets headed to a client that reposition its own character, otherwise you will be stuck in a loop of the player moving locally with their keyboard and being repositioned remotely based on their last known value. Instead, you need to listen for movement server-side and only reposition the player when the movement seems out of sync. This is the simplest form of cheating detection–if the player has moved from a to b faster than their movement speed could possibly allow, or they have spent too much time in the air (this was a bug in Minecraft for a long time), there was either a bug that caused it or the player is using a modified client to run faster/fly. Some games kick the player when this happens.

Now, think back to when I told you about my first iteration of this server, back when I mentioned my server simply blasted packets to the client, causing it to occasionally fall behind and cause a stack overflow. This was because if I limited them, I was seeing a lag in player movement as the game waited for the next packet, so why not just send them as quickly as possible? Well, this is simply not possible with thousands of players connected. But if we’re only sending 5-15 packets a second, why don’t the players jump in WoW?

To fix this, we use a technique called *lerping* or *interpolation*. This is another word for the client’s game engine filling in the animation between packets to create the appearance of continuous movement, even when only 10 of those 60 frames per second have actual data from the server attached to them.

You might be thinking “but the client doesn’t know which direction the player is actually moving! What if the player turns right suddenly?” This is a [hot area](http://techcrunch.com/2014/08/22/microsoft-research-shows-off-delorean-its-tech-for-building-a-lag-free-cloud-gaming-service/) of research at the moment, but the basics have been around for a while. What most games do is to delay the processing of packets until the next one has been received, causing the avatar you see for your buddy to be behind a packet at all times. This allows your client to have a start point and an end point, and all values can be calculated in between based on the timestamps.

Games like Call of Duty have made impressive strides in researching ways to mitigate this lag. While lerping is necessary to prevent weird, unnatural movement, games where exact positioning is paramount must then post-process the player movements server-side and account for the lag. Have you ever been surprised you survived an encounter with an enemy, only to die a fraction of a second later? Lag correction was probably at work there, and many games use it–particularly shooters. Unless your game is highly fast paced, your players probably won’t notice if they are a packet behind if you implement lerping.

# MMO Coding Design Series 6: World Model

by [Taylor](http://taylorroberthill.com/GameDevStation/author/taylor/)



PREVIOUS: [Delta Compression & Lerping](http://taylorroberthill.com/GameDevStation/2015/04/28/mmo-coding-design-series-4-delta-compression-lerping/)

I keep referencing this “world model.” What is it really? I saved this question until now because it is important to understand how data is relayed to clients before gathering requirements on how the data should be structured. While the two layers should be completely conceptually different and independent, it is still helpful to model them in a collaborative design, at least to begin with.

The world model should be encapsulated largely in a single class, which we will call **WorldModel**. How this class is structured will depend on your game, but in my example I had three lists that made up the vast majority of everything that needed to be organized. Using C# notation, my properties look like this:

- **public List<Entity> World { get; set; }**
- **public List<Entity> Dirty { get; set; }**
- **public List<Player> Players { get; set; }**
- **public Dictionary<string, string> Snapshot { get; set; }**

Recall that in a previous example, **Player** inherits from **Entity,** so all three of these lists contain **Entities**.

**World** contains everything but active players. These are your shrubs, wise old yogi NPCs, walls–but only the things that can be interacted with. There should never be a static “sky” object sitting in this list; the server doesn’t care one bit about things that don’t change or that don’t need to be tracked. The client’s engine should handle rendering these things. Everything else, though, should belong here. These classes are simply models that hold numbers, strings, or other data that make up your world.

**Dirty** is a quick list of things that have changed since the last snapshot was taken. Whenever an object has changed, it should be placed into this list, and then the list should be cleared whenever the snapshot is taken. This is to prevent iterating through objects that rarely change to save CPU cycles.

**Players** is a special list that only contains, well, players. Sometimes you just need to iterate through a list of players, and having them in its own list can be helpful.

The **Dirty** and **Players** are optional, of course–you could just as easily have everything in the **World** list. I just found that it was easier to debug when you could set a breakpoint and see the contents of these lists at a glance.

The rest of **WorldModel** will be methods such as **GetPlayer, GetWorldObject,** **GetDirtyPlayers**, and so on. There should’t be too much logic in the world model, simply because it’s just that–a model. Its job is to hold data.

Now, regarding the **Snapshot** dictionaries. After trying several different methods of conveying entity state, I found a pretty decent way to do so. Going back to our **Entity** superclass, we modify the setters for each of our properties to go into **WorldModel.Snapshot** and create a key in the format “uniqueKey-propertyName”. The value is the new, updated value. This can change based on what the property is, of course, and you may want to use real opcodes in WoW form to be more descriptive, but it could be this simple for properties like X position. When the time comes to send out the snapshot diff, the work is already done, and we have a list of opcodes that perfectly describe how things have changed.

These setters could be where you validate for cheating and bugs, and then add opcodes to the snapshot accordingly.