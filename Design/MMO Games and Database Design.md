[EXAMPLE ER DIAGRAMS](https://www.vertabelo.com/blog/example_er_diagrams)

# MMO Games and Database Design

[![img](https://www.vertabelo.com/authors/emil-drkusic/emil-drkusic_hu906145c8be8fbce48eb9af1ea1c4a863_24343_32x32_fill_box_center_2.png)Emil DrkušićDatabase designer and developer, financial analyst.](https://www.vertabelo.com/authors/emil-drkusic/)

- Tags:

- [database design](https://www.vertabelo.com/tags/database-design)



Let’s be honest: we all love to play games, especially on our computers. Until the Internet became widespread, most of us played computer games by ourselves, usually against AI opponents. It was fun, but as soon as you realized how the gameplay mechanics worked, the game lost most of its magic.

The development of the Internet moved games online. Now, we can play against human opponents and test our skills against theirs. No more rote gameplay!

Then massive multiplayer online (MMO) games emerged and changed everything. Thousands of players found themselves in the same game universes, competing over resources, negotiating, trading and fighting. To make such games possible, a database structure was needed that could store all the relevant information.

In this article, we will design a model that incorporates the most common elements found in MMO games. We will discuss how to use it, its limitations, and its possible improvements.

### An Introduction to Data Models for MMO Games

There are plenty of very popular MMO games today, and they involve all kinds of scenarios. I will focus here on strategy games like *Ogame*, *Travian*, *Sparta*: *War of Empires* and *Imperia Online*. These games are more about planning, building and strategizing, and less about direct action.

MMO games are set in different universes, are visually different, and use more or less different gameplay options. Still, some ideas are the same. Players compete for locations, fight for them, and form alliance with (and against) other players. They build structures, collect resources, and research technologies. They build units (such as warriors, tanks, traders, etc.) and use them to trade with allies or to fight with opponents. All of that needs to be supported in our database.

We can think of these games as online board games with many indexed squares. Each square can have many different actions associated with it; some actions will include multiple squares – e.g. when we move units or resources from one location to another.



EDIT MODEL IN YOUR BROWSER

AlliancesPlayers / UsersUnitsLocations and StructuresResearch and Resourcesplayeriduser_namepasswordnicknameemailconfirmation_codconfirmation_dateintvarchar(64)varchar(64)varchar(64)varchar(254)varchar(128)timestampPKNallianceidalliance_namedate_foundeddate_disbandedintvarchar(128)timestamptimestampPKNalliance_memberidplayer_idalliance_iddate_fromdate_tomembership_type_iintintinttimestamptimestampintPKFKFKNFKmembership_typeidtype_nameintvarchar(64)PKmembership_historyidalliance_member_idmembership_type_idate_fromdate_tointintinttimestamptimestampPKFKFKNlogin_historyidplayer_idlogin_timelogout_timlogin_dataintinttimestamptimestamptextPKFKNmembership_actionsidaction_nameintvarchar(64)PKaction_allowedidmembership_type_idmembership_actions_idintintintPKFKFKlocationidlocation_namecoordinatesdimensionplayer_idintvarchar(64)varchar(255)varchar(255)intPKN FKstructureidstructure_nameupgrade_time_formulintvarchar(64)textPKstructure_builtidlocation_idstructure_idcurrent_levelupgrade_ongoingupgrade_end_timeintintintintbooltimestampPKFKFKNresourceidresource_nameintvarchar(64)PKstructure_formulaidstructure_idresource_idupgrade_formulaproduction_formulintintinttexttextPKFKFKunitidunit_nameintvarchar(64)PKunit_costidunit_idresource_idcostintintintintPKFKFKunits_on_locationidunit_idlocation_idnumberintintintintPKFKFKgroup_movementidplayer_idmovement_type_ilocation_fromlocation_toarrival_timereturn_timewait_timeintintintintinttimestamptimestampintPKFKFKFKFKNNunits_in_groupidunit_idgroup_moving_idnumberintintintintPKFKFKmovement_typeidtype_nameallows_waitintvarchar(64)boolPKallied_movementidtime_createdplayer_idinttimestampintPKFKallied_groupsidallied_movement_idgroup_movement_idintintintPKFKFKresources_on_locatioidresource_idlocation_idnumberintintintintPKFKFKcharacteristicidcharacteristic_nameintvarchar(64)PKunit_characteristicidunit_idcharacteristic_idvalueintintintintPKFKFKresearchidresearch_nameupgrade_time_formulintvarchar(64)textPKprerequisite_researcidresearch_idstructure_idlevel_requiredintintintintPKFKFKprerequisite_structuridstructure_idresearch_idlevel_requiredintintintintPKFKFKresearch_unitidresearch_idunit_idlevel_requiredintintintintPKFKFKresearch_formulaidresearch_idresource_idupgrade_formulaintintinttextPKFKFKresearch_levelidplayer_idresearch_idcurrent_levelupgrade_ongoingupgrade_end_timeintintintintbooltimestampPKFKFKNresources_in_groupidresource_idgroup_movement_idnumberintintintintPKFKFKstructure_requiredidstructure_idstructure_required_idlevelintintintintPKFKFKresearch_requiredidresearch_idresearch_required_idlevelintintintintPKFKFK





The database is divided into five main areas:

- `Players / Users`
- `Alliances`
- `Locations and Structures`
- `Research and Resources`
- `Units`

The remaining seven ungrouped tables are related to units and describe unit position and in-game movements. We will look at each of these areas in much more detail, starting with **Players** and **Alliances**.

### Players and Alliances

Without a doubt, players are the most important part of any game.

![Players / Users area](https://www.vertabelo.com/blog/mmo-games-and-database-design/players-users-area.png)

The `**player**` table contains a list of all registered players taking part in a game instance. We will store the players’ usernames, passwords, and screen names. These will be stored in the `user_name`, `password`, and `nickname` attributes respectively.

New users will need to provide an email address during registration. A confirmation code will be generated and sent to them, which they will reply to. We will update the `confirmation_date` attribute when the user verifies their email address. So, this table has three unique keys: `user_name`, `nickname` and `email`.

Each time a user logs in, a new record is added in the `**login_history**` table. All of the attributes in this table are self-explanatory. The `logout_time` is specific. It can be NULL when the user’s current session is active or when users quit the game (without logging out) due to technical problems. In the `login_data` attribute, we’ll store login details like a player’s geographic location, IP address, and the device and browser they use.

![Alliances area](https://www.vertabelo.com/blog/mmo-games-and-database-design/alliances-area.png)

Most MMO games let us cooperate with other players. One of the standard forms of player cooperation is the alliance. Players share their in-game “private data” (online status, plans, location of their cities and colonies, etc.) with others to benefit from allied actions and for the sheer fun of it.

The `**alliance**` table stores basic information about game alliances. Each one has a unique `alliance_name` that we’ll store. We’ll also have a field, `date_founded`, that stores when the alliance was founded. If an alliance is disbanded, we’ll store that information in the `date_disbanded` attribute.

The `**alliance_member**` table relates players with alliances. Players may join and leave the same alliance more than once. Because of this, the `player_id` – `alliance_id` pair is not a unique key. We’ll keep information regarding when a player joins the alliance and when (if) they leave in the `date_from` and `date_to` fields. The `membership_type_id` attribute is a reference to the `**membership_type**` dictionary; it stores the current level of players’ rights in the alliance.

Players’ rights in an alliance can change over time. The `**membership_actions**`, `**membership_type**` and `**actions_allowed**` tables together define all possible rights for alliance members. This model doesn’t allow players to define their own levels of rights in an alliance, but that could be accomplished easily enough by adding new records in the `**membership_type**` dictionary and storing information about which alliances they are related to.

To sum up: the values stored in these tables are defined by us during the initial setup; they’ll change only if we introduce new options.

The `**membership_history**` table stores all data regarding players’ roles or rights within an alliance, including the range when these rights were valid. (For example, he could have “novice” permissions for a month, and then “full membership” from that point on.) The `date_to` attribute is NULLable because currently active rights have not ended yet.

The `**membership_actions**` dictionary contains a list of every action players can make in an alliance. Each action has its’ own `action_name` and game logic is built around these names. We can expect values like *“view members list”*, *“view members’ statuses”* and *“send message”* here.

The `**membership_type**` dictionary contains the unique names of the action groups used in the game. The `**actions_allowed**` table assigns actions to membership types. Each action can be assigned to a type only once. Therefore, the `membership_action` - `membership_type` pair forms the unique key for this table.

### Locations and Structures

![Locations and Structures area](https://www.vertabelo.com/blog/mmo-games-and-database-design/locations-and-structures-area.png)

Game locations are areas where players collect resources and build structures and units. Some games have a predefined range of possible locations, while others may allow users to define their own locations.

In a 3D space, locations can be defined with [x:y:z] coordinates. If a game has a predefined range, it may not permit players to use any location out of the range [0:1000] for all three axes, so we’re limited to a 1000 * 1000 * 1000 space.

On the other hand, maybe we want to allow players to enter the exact coordinates of their new location – e.g. [1001:2073:4] – and we want the game to process it for them.

We’ll keep a list of all locations used in an instance of our game in the `**location**` table. Each location has its own name, but the names are not unique. On the other hand, the `coordinates` attribute must contain only unique values. Location coordinates are stored as text values, so we can store coordinates for 3D games as [112:72:235]. Coordinates for 2D games can be stored as <1102:98>.

In some games, locations will have a number of squares that are used to house structures or units. We’ll keep that information in the `dimension` attribute, which is a text field. A dimension can be simply number of squares in a 2D or 3D grid. The `player_id` attribute stores information about the current owner of that location. It can be NULL when locations are predefined and players compete to occupy them.

The `**structure**` table contains a list of all structures we can build at various game locations. Structures represent improvements that allow us to produce better units, perform new types of research, produce more resources, etc. Each structure used in the game has its own unique `structure_name`. Some possible `structure_name` values are “farm”, “ore mine”, “solar plant”, and “research center”.

We can expect each structure to be upgraded multiple times, so we’ll also store information about its current level. Each upgrade improves structures’ output, so it produces more resources or allows us to use new features in the game. We can’t know the maximum level of upgrade in advance, so we’ll define all the level-related stuff (costs, upgrade time and production) with formulas. ***All formulas stored in the database are the core of the game’s mechanics, and their adjustment is crucial for game balance and gameplay in general.\***

That is also the case with the `upgrade_time_formula` attribute. An example value for this field is *“ \* 30 min”*, where represents the level we want to upgrade to.

In most cases, there are requirements that must be met before players take certain actions. Maybe we need to complete a defined amount of research before we can build new structures or vice versa. We’ll store the research level needed to build structures in the `**prerequisite_research**` table. Relationships and the structure level needed to start various researches are kept in the in the `**prerequisite_structure**` table. In both tables, the foreign keys `research_id` and `structure_id` are paired to form a unique key. The `level_required` attribute is the only value.

These two tables, `**prerequisite_research**` and `**prerequisite_structure**`, also form the core of the game.

For each structure, we’ll define a list of prerequisites: other structures and their minimum levels that players must have to begin building. We’ll store this data in the `**structure_required**` table. Here, `structure_id` represents the structure we want to build; `structure_required_id` is a reference to the prerequisite structure(s), and `level` is the level required.

The `**structure_built**` table stores information about current structure levels on a given location. The `upgrade_ongoing` attribute will be set only if an upgrade is currently ongoing, while the `upgrade_end_time` attribute will contain a timestamp once the upgrade is complete.

The `**structure_formula**` table relates structures and resources. The foreign key pair to this table forms its unique key. This table also has two text attributes containing formulas with as parameter. We’ll define these formulas, one for costs and the other for resource generation, in the database. They will be similar to the `upgrade_time_formula`. We need them because we must define the resources spent in building each structure. We also need to define resource production after upgrade, if structure generates any resources (i.e. ore mine will produce ** 20* ore per day).

### Research and Resources

Research (or technologies) in games are usually requisite to the creation of other features. Without certain levels of research, new structures or unit types can’t be built. Research also can have its own requirements. One of most common is the level of a given structure, usually called a “research lab”. Or perhaps players need to complete a certain level of research before they can start new research. All of these requirements will be handled in this section. Below, we can find the data model for Research and Resources:

![Research and Resources area](https://www.vertabelo.com/blog/mmo-games-and-database-design/research-and-resources-area.png)

The `**research**` table contains a list of all possible research actions in our game. It uses the same logic as the `**structure**` table. The `research_name` attribute is the table’s unique key, while the `upgrade_time_formula` field contains a text representation of the research time requirements formula, with as its parameter. Any resources required for upgrades are defined in the `upgrade_formula` stored in the `**research_formula**` table.

As with structures, we’ll define the list of all other researches and their levels that must be completed before we can start another type of research. We’ll store this data in the `**research_required**` table, where `research_id` represents the desired research; `research_required_id` is a reference to the prerequisite research, and `level` is the level required.

Research is related to individual players, and for each *player – resear*ch pair we must store a player’s current research level and any ongoing upgrade statuses. We’ll store this information using the `**research_level**` table in the same manner that we used the `**structure_built**` table.

Resources like wood, ore, gems, and energy are mined or collected and used later to build structures and other improvements. We’ll store a list of all in-game resources in the `**resource**` dictionary. The only attribute here is the `resource_name` field, and it is also the unique key of the table.

To keep track of the current quantity of resources on each location, we’ll use the `**resources_on_location**` table. Again, a foreign key pair (`resource_id` and `location_id`) forms the unique key of the table, while the `number` attribute stores the current resource values.

### Units and Movements

![Units area](https://www.vertabelo.com/blog/mmo-games-and-database-design/units-area.png)

Resources are used to produce units. Units can be used to transport resources, attack other players, or in general pillaging and burning.

The list of unit types used in our game is stored in the `**unit**` dictionary with only one value, `unit_name`; that attribute is the unique key of this table. Some common game units are “swordsman”, “battlecruiser”, “griffin”, “jet fighter”, “tank”, etc.

We need to describe each unit with specific characteristics. A list of all possible characteristics is stored in the `**characteristic**` dictionary. The `characteristic_name` field contains a unique value. Values in this field could include: “attack”, “defense” and “hit points”. We will assign characteristics to units using the `**unit_characteristic**` relation. The foreign key pair of `unit_id` and `characteristic_id` form the unique key of the table. We will use only one attribute, `value`, to store the desired value.

The `**research_unit**` table contains a list of all research activities that must be finished before we can start production of a given unit type. The `**unit_cost**` table defines the resources needed to produce a single unit. Both tables have unique keys composed of the foreign key pair (`research_id` or `resources_id` combined with `unit_id`) and one value field (`cost` and `level_required`).

![Units Location and Movement](https://www.vertabelo.com/blog/mmo-games-and-database-design/units-location-and-movement.png)

And now, the fun part. Production is fun, but moving units around and taking action is even better. We’ve already introduced the `**unit**` table, but we’ll keep it here because of how it relates with other tables.

Either units are stationed on a location or they are moving between locations. Adding the `player_id` field determines who owns either the location or the group that is moving between the locations.

If units are just stationed at the given location, we’ll store that location and the number of units stationed there. To do so, we’ll use the `**units_on_location**` table.

When units are not stationed, they’re moving around. We’ll need to store their departure point and their destination. In addition, we need to define possible actions during movements. All such actions are stored in the `**movement_type**` dictionary. The `type_name` attribute is unique while the `allows_wait` attribute determines if an action allows waiting at the destination point.

We can move a single unit type, but in almost every case we’ll move many units of several different unit types. That group will share common data and we’ll store them in the `**group_movement**` table. In this table, we’ll define the following items:

- the player that initiated that action
- the action type
- the starting point
- the destination point
- the `arrival_time` at the destination
- the `return_time` to the starting point
- the `wait_time` at the destination

The `return_time` attribute can be NULL if this is a one-way journey, and `wait_time` is defined by the player. Units belonging to a group are defined by values stored in the `**units_in_group**` table. The foreign key pair of `units_id` and `group_moving_id` forms the unique key of the table. The number of the units of the same type within a group is defined in the `number` attribute.

Each movement can transport resources from one location to another. Therefore, we’ll define a many-to-many relationship between the `**group_movement**` and the `**resources**` tables. Besides the primary and foreign keys, the `**resources_in_group**` table contains only the `number` attribute. This field stores the amount of resources players move from the starting point to their destination.

In most cases, players can call others to join their adventure. To support that we’ll use two tables: `**allied_movement**` and `**allied_groups**`. One player will initiate joint action, and that will create a new record in the `**allied_movement**` table. All groups of units that take part in an allied action are defined by values stored in the `**allied_groups**` table. Each group can be assigned to an allied action only once, so foreign keys form the unique key of this table.

This model gives us the basic structure needed to build an MMO strategy game. It contains the most important game features: locations, structures, resources, research, and units. It also relates them, lets us define prerequisites in the database, and stores most of the game logic in the database as well.

After these tables are populated, most of the game logic is defined and we wouldn’t expect new values to be added. Almost every table has a unique key value, either a feature name or foreign key pair. Changing units’ characteristics and production/cost formulas will allow us to change the game balance in the database layer.

How would you change this model? What do you like, and what would you do differently? Tell us in the comment section!