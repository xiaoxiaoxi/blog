# 写在前面

非常不错的教程而且完整，可以直接整合到自己的代码中。

# Creating a TCP Client in Godot

#### [Thomas Langford](https://bytesnsprites.com/author/thomas/)

08 Aug 2021 • 5 min read

Godot has excellent networking support with a fully implemented [high level networking API](https://docs.godotengine.org/en/stable/tutorials/networking/high_level_multiplayer.html) to make creating networked multiplayer games easy. Occasionally though, it's desirable to have a direct TCP connection to a server to be able to send or receive some information. This tutorial will walk you through using Godot's [StreamPeerTCP](https://docs.godotengine.org/en/stable/classes/class_streampeertcp.html) class to create a client than can connect to a TCP server.

## Versions

| Component | Version |
| :-------- | :------ |
| Godot     | 3.3     |

## Setup

First [create a new Godot project](https://bytesnsprites.com/creating-a-new-godot-project/).

## Client Class

Now we will create our client script that will be responsible for making the TCP connection. This node will be responsible for managing the TCP connection, sending messages, receiving messages, and providing notifications via signals of important events.

Create a new script called `client.gd` that extends from `Node` and defines the following signals.

```gdscript
extends Node

signal connected      # Connected to server
signal data           # Received data from server
signal disconnected   # Disconnected from server
signal error          # Error with connection to server
```

We will need a TCP steam for the TCP connection and a variable to save the stream's status. The status will be initialized in the `_ready` function and will be used to detect when the stream's status has changed during the process step.

```gdscript
var _status: int = 0
var _stream: StreamPeerTCP = StreamPeerTCP.new()

func _ready() -> void:
	_status = _stream.get_status()
```

For the user to be able to start the connection, create a new function called `connect_to_host` with the following content. This function will take the server's host and port and attempt to make a connection using the stream's `connect_to_host` function. It will emit the error signal if the connection fails.

```gdscript
func connect_to_host(host: String, port: int) -> void:
	print("Connecting to %s:%d" % [host, port])
	# Reset status so we can tell if it changes to error again.
	_status = _stream.STATUS_NONE
	if _stream.connect_to_host(host, port) != OK:
		print("Error connecting to host.")
		emit_signal("error")
```

Copy

Next we need a way for the user to send a message to the server. Create a new function called `send` with the following content. This function takes a `PoolByteArray` which will contain the data to send to the server. If the stream is not connected to the server or cannot send the data, then the function returns false to let the user know it failed to send.

```gdscript
func send(data: PoolByteArray) -> bool:
	if _status != _stream.STATUS_CONNECTED:
		print("Error: Stream is not currently connected.")
		return false
	var error: int = _stream.put_data(data)
	if error != OK:
		print("Error writing to stream: ", error)
		return false
	return true
```

Finally, we need a way for the client to be able to read data from the server and notify the user of any messages. We will use the built in `_process` method to constantly monitor the status of the stream and inform the user via signals of any important event such as connection, disconnection, or error. While the status is connected, we will attempt to read from the stream when there are bytes available and notify the user of any data via the data signal.

```gdscript
func _process(delta: float) -> void:
	var new_status: int = _stream.get_status()
	if new_status != _status:
		_status = new_status
		match _status:
			_stream.STATUS_NONE:
				print("Disconnected from host.")
				emit_signal("disconnected")
			_stream.STATUS_CONNECTING:
				print("Connecting to host.")
			_stream.STATUS_CONNECTED:
				print("Connected to host.")
				emit_signal("connected")
			_stream.STATUS_ERROR:
				print("Error with socket stream.")
				emit_signal("error")

	if _status == _stream.STATUS_CONNECTED:
		var available_bytes: int = _stream.get_available_bytes()
		if available_bytes > 0:
			print("available bytes: ", available_bytes)
			var data: Array = _stream.get_partial_data(available_bytes)
			# Check for read error.
			if data[0] != OK:
				print("Error getting data from stream: ", data[0])
				emit_signal("error")
			else:
				emit_signal("data", data[1])
```

The final client looks like the following.

```gdscript
extends Node

signal connected
signal data
signal disconnected
signal error

var _status: int = 0
var _stream: StreamPeerTCP = StreamPeerTCP.new()

func _ready() -> void:
	_status = _stream.get_status()

func _process(delta: float) -> void:
	var new_status: int = _stream.get_status()
	if new_status != _status:
		_status = new_status
		match _status:
			_stream.STATUS_NONE:
				print("Disconnected from host.")
				emit_signal("disconnected")
			_stream.STATUS_CONNECTING:
				print("Connecting to host.")
			_stream.STATUS_CONNECTED:
				print("Connected to host.")
				emit_signal("connected")
			_stream.STATUS_ERROR:
				print("Error with socket stream.")
				emit_signal("error")

	if _status == _stream.STATUS_CONNECTED:
		var available_bytes: int = _stream.get_available_bytes()
		if available_bytes > 0:
			print("available bytes: ", available_bytes)
			var data: Array = _stream.get_partial_data(available_bytes)
			# Check for read error.
			if data[0] != OK:
				print("Error getting data from stream: ", data[0])
				emit_signal("error")
			else:
				emit_signal("data", data[1])

func connect_to_host(host: String, port: int) -> void:
	print("Connecting to %s:%d" % [host, port])
	# Reset status so we can tell if it changes to error again.
	_status = _stream.STATUS_NONE
	if _stream.connect_to_host(host, port) != OK:
		print("Error connecting to host.")
		emit_signal("error")

func send(data: PoolByteArray) -> bool:
	if _status != _stream.STATUS_CONNECTED:
		print("Error: Stream is not currently connected.")
		return false
	var error: int = _stream.put_data(data)
	if error != OK:
		print("Error writing to stream: ", error)
		return false
	return true
```

client.gd

## Testing

To test our client class we need two things. First is a script that will make use of our client class. Second is a server for the client to connect to.

Create a new node in your scene of type `Node` and attach a script with the following contents. This script creates an instance of our client class, connects to its signals, and handles each event reported by the client. When it receives data it prints it to the console and will respond to the server with the string "ack". If the client is disconnected or encounters an error it will attempt to reconnect to the server every 3 seconds.

```gdscript
extends Node

const HOST: String = "127.0.0.1"
const PORT: int = 5000
const RECONNECT_TIMEOUT: float = 3.0

const Client = preload("res://client.gd")
var _client: Client = Client.new()

func _ready() -> void:
	_client.connect("connected", self, "_handle_client_connected")
	_client.connect("disconnected", self, "_handle_client_disconnected")
	_client.connect("error", self, "_handle_client_error")
	_client.connect("data", self, "_handle_client_data")
	add_child(_client)
	_client.connect_to_host(HOST, PORT)

func _connect_after_timeout(timeout: float) -> void:
	yield(get_tree().create_timer(timeout), "timeout") # Delay for timeout
	_client.connect_to_host(HOST, PORT)

func _handle_client_connected() -> void:
	print("Client connected to server.")

func _handle_client_data(data: PoolByteArray) -> void:
	print("Client data: ", data.get_string_from_utf8())
	var message: PoolByteArray = [97, 99, 107] # Bytes for "ack" in ASCII
	_client.send(message)

func _handle_client_disconnected() -> void:
	print("Client disconnected from server.")
	_connect_after_timeout(RECONNECT_TIMEOUT) # Try to reconnect after 3 seconds

func _handle_client_error() -> void:
	print("Client error.")
	_connect_after_timeout(RECONNECT_TIMEOUT) # Try to reconnect after 3 seconds
```

Copy

main.gd

If you already have a server to connect to, then you can run your scene and you should see "Client connected to server." printed on a successful connection. Make sure you change the host and port to that of your server!

If you do not have a server, then you can create a simple TCP server to test against using [Node.js](https://nodejs.org/). Make sure you have node.js installed on your system and then create a new file called `server.js` with the following contents.

```javascript
const net = require('net');

let server = net.createServer((socket) => {
	socket.on('data', (data) => {
		console.log("Received: " + data);
	});
	console.log("Accepted connection.");
	socket.write("Hello from the server!\n");
}).listen(5000, () => console.log("Listening on 5000."));
```

Copy

server.js

Start the server with the `node` command by running `node server.js`. Then run your main scene. If the connection was successful, then you should get the following output.

```text
Connecting to 127.0.0.1:5000
Connected to host.
Client connected to server.
available bytes: 23
Client data: Hello from the server!
```

Copy

Congratulations, now you have a client running in Godot that will connect to an external server!

If you want to add a layer of security, then check out my next tutorial on creating a [SSL client](https://bytesnsprites.com/creating-a-ssl-client-in-godot/).