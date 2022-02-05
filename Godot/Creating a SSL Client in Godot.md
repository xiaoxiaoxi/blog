# 写在前面

目前还没有采用SSL方式连接，所以暂时标记记录，需要的时候再消化

# Creating a SSL Client in Godot

#### [Thomas Langford](https://bytesnsprites.com/author/thomas/)

10 Sep 2021 • 5 min read

This tutorial will cover using Godot's `StreamPeerSSL` class to create a TLS/SSL connection to a server. It builds off of my [TCP client tutorial](https://bytesnsprites.com/creating-a-tcp-client-in-godot/) where we created a TCP (non-SSL) connection. You will need the completed `client.gd` file found at the end of the Client Class section (in the aforementioned TCP client tutorial) to start from for the remainder of this tutorial.

## Disclaimer

I am *not* a security expert and claim no guarantees on the safety of using this technique. If the information and/or servers you need to protect need strong security then you should seek the advice of a professional security engineer. This tutorial is provided for informational purposes only and you are responsible for your own security.

## Versions

| Component | Version |
| :-------- | :------ |
| Godot     | 3.3     |

## SSL Client

We will take our previously created TCP client and make some modifications to upgrade the connection to a SSL connection.

**Step 1:** Change the `_stream` variable's type from `StreamPeerTCP` to `StreamPeerSSL`. The [StreamPeerSSL](https://docs.godotengine.org/en/stable/classes/class_streampeerssl.html) class provides the underlying mechanisms to create and manage the SSL connection.

```diff
- var _stream: StreamPeerTCP = StreamPeerTCP.new()
+ var _stream: StreamPeerSSL = StreamPeerSSL.new()
```

Copy

**Step 2**: The `connect_to_host` function needs to be updated to make use of the SSL stream. The StreamPeerSSL class expects to use an existing TCP connection, which it then upgrades to a SSL connection.

Create a new TCP stream peer and attempt a connection to the server using the `connect_to_host` function. We will check the return value for an error and emit the error signal if the connection failed.

Next, upgrade TCP connection to a SSL connection by passing it to the SSL stream using the `connect_to_stream` function. If this function fails, it will return an error which is printed to the console. We do not emit the error signal here because the error will be caught and emitted during the `_process` step and we do not want to emit the error twice.

The StreamPeerSSL class also uses a different set of statuses than the StreamPeerTCP class. Swap out the `STATUS_NONE` for `STATUS_DISCONNECTED`.

```diff
func connect_to_host(host: String, port: int) -> void:
	print("Connecting to %s:%d" % [host, port])
	# Reset status so we can tell if it changes to error again.
-	_status = _stream.STATUS_NONE
-	if _stream.connect_to_host(host, port) != OK:
-		print("Error connecting to host.")
-		emit_signal("error")
+	_status = _stream.STATUS_DISCONNECTED
+	var tcp: StreamPeerTCP = StreamPeerTCP.new()
+	var error: int = tcp.connect_to_host(host, port)
+	if error != OK:
+		print("Error connecting to host: ", error)
+		emit_signal("error")
+		return
+	error = _stream.connect_to_stream(tcp)
+	if error != OK:
+		print("Error upgrading connection to SSL: ", error)
```

Copy

**Step 2 (optional)**: If you need to validate the server certificate, then you will want to use the optional parameters to the `connect_to_stream` function. You can pass a boolean on whether to validate the server certificate, the valid server host name, and a valid server certificate to accept. The certificate will need to be a [X509Certificate](https://docs.godotengine.org/en/stable/classes/class_x509certificate.html) resource.

```diff
+ error = _stream.connect_to_stream(tcp, true, "server.hostname.com", server_certificate)
```

Copy

**Step 3**: Inside of the `_process` function change the `STATUS_NONE` case in the match statement to `STATUS_DISCONNECTED`. The disconnected status will be treated the same as the previous none status.

Remove the `STATUS_CONNECTING` case and add the `HANDSHAKING` and `ERROR_HOSTNAME_MISMATCH` cases as seen below. The handshaking status will print a message indicating that the handshake is currently taking place. The host name mismatch error status will print a message indicating that there is an error and emit the error signal to inform the user.

```diff
func _process(delta: float) -> void:
	var new_status: int = _stream.get_status()
	if new_status != _status:
		_status = new_status
		match _status:
-			_stream.STATUS_NONE:
+			_stream.STATUS_DISCONNECTED:
				print("Disconnected from host.")
				emit_signal("disconnected")
-			_stream.STATUS_CONNECTING:
-				print("Connecting to host.")
			_stream.STATUS_CONNECTED:
				print("Connected to host.")
				emit_signal("connected")
			_stream.STATUS_ERROR:
				print("Error with socket stream.")
				emit_signal("error")
+			_stream.STATUS_HANDSHAKING:
+				print("Performing SSL handshake with host.")
+			_stream.STATUS_ERROR_HOSTNAME_MISMATCH:
+				print("Error with socket stream: Hostname mismatch.")
+				emit_signal("error")
```

Copy

**Step 4**: Poll the `_stream` object inside of the `_process` method. This ensures that the next call to `get_available_bytes` will be accurate and that the connection will break if the server closes the connection.

```diff
	if _status == _stream.STATUS_CONNECTED:
+		# Poll the stream to ensure connection is valid and check for availalbe bytes.
+		_stream.poll()
		var available_bytes: int = _stream.get_available_bytes()
		if available_bytes > 0:
```

Copy

That's it! The final SSL client looks like the following:

```gdscript
extends Node

signal connected
signal data
signal disconnected
signal error

var _status: int = 0
var _stream: StreamPeerSSL = StreamPeerSSL.new()

func _ready() -> void:
	_status = _stream.get_status()

func _process(delta: float) -> void:
	var new_status: int = _stream.get_status()
	if new_status != _status:
		_status = new_status
		match _status:
			_stream.STATUS_DISCONNECTED:
				print("Disconnected from host.")
				emit_signal("disconnected")
			_stream.STATUS_HANDSHAKING:
				print("Performing SSL handshake with host.")
			_stream.STATUS_CONNECTED:
				print("Connected to host.")
				emit_signal("connected")
			_stream.STATUS_ERROR:
				print("Error with socket stream.")
				emit_signal("error")
			_stream.STATUS_ERROR_HOSTNAME_MISMATCH:
				print("Error with socket stream: Hostname mismatch.")
				emit_signal("error")

	if _status == _stream.STATUS_CONNECTED:
		# Poll the stream to ensure connection is valid and check for availalbe bytes.
		_stream.poll()
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
	_status = _stream.STATUS_DISCONNECTED
	var tcp: StreamPeerTCP = StreamPeerTCP.new()
	var error: int = tcp.connect_to_host(host, port)
	if error != OK:
		print("Error connecting to host: ", error)
		emit_signal("error")
		return
	error = _stream.connect_to_stream(tcp)
	if error != OK:
		print("Error upgrading connection to SSL: ", error)

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

Copy

client.gd

## Testing

We can use the same `main.gd` as from the [TCP client tutorial](https://bytesnsprites.com/creating-a-tcp-client-in-godot/). It is repeated below for convenience.

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

If you do not have a server, then you can create a simple server to test against using [Node.js](https://nodejs.org/). Make sure you have node.js installed on your system and then create a new file called server.js with the following contents.

```javascript
const tls = require('tls');
const fs = require('fs');

const options = {
   key: fs.readFileSync('test-key.pem'),
   cert: fs.readFileSync('test-cert.pem'),
};

let server = tls.createServer(options, (socket) => {
	socket.on('data', (data) => {
		console.log("Received: " + data);
	});
	console.log("Accepted connection.");
	socket.write("Hello from the server!\n");
}).listen(5000, () => console.log("Listening on 5000."));
```

Copy

server.js

Notice the options for passing in the server's key and certificate. The generation of these certificates is out of the scope of this tutorial, but if you do not already have them you can generate them with the process described [here](https://stackoverflow.com/questions/10175812/how-to-generate-a-self-signed-ssl-certificate-using-openssl).

Start the server with the `node` command by running `node server.js`. Then run your main scene. If the connection was successful, then you should get the following output.

```plaintext
Connecting to 127.0.0.1:5000
Connected to host.
Client connected to server.
available bytes: 23
Client data: Hello from the server!
```

Copy

Congratulations, now you have a client running in Godot that will connect to an external server using a SSL connection!