# Godot - Networking

**Pages:** 23

---

## ENetConnection

**URL:** https://docs.godotengine.org/en/stable/classes/class_enetconnection.html

**Contents:**
- ENetConnection
- Description
- Tutorials
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

A wrapper class for an ENetHost.

ENet's purpose is to provide a relatively thin, simple and robust network communication layer on top of UDP (User Datagram Protocol).

API documentation on the ENet website

bandwidth_limit(in_bandwidth: int = 0, out_bandwidth: int = 0)

broadcast(channel: int, packet: PackedByteArray, flags: int)

channel_limit(limit: int)

compress(mode: CompressionMode)

connect_to_host(address: String, port: int, channels: int = 0, data: int = 0)

create_host(max_peers: int = 32, max_channels: int = 0, in_bandwidth: int = 0, out_bandwidth: int = 0)

create_host_bound(bind_address: String, bind_port: int, max_peers: int = 32, max_channels: int = 0, in_bandwidth: int = 0, out_bandwidth: int = 0)

dtls_client_setup(hostname: String, client_options: TLSOptions = null)

dtls_server_setup(server_options: TLSOptions)

get_local_port() const

get_max_channels() const

Array[ENetPacketPeer]

pop_statistic(statistic: HostStatistic)

refuse_new_connections(refuse: bool)

service(timeout: int = 0)

socket_send(destination_address: String, destination_port: int, packet: PackedByteArray)

enum CompressionMode: 

CompressionMode COMPRESS_NONE = 0

No compression. This uses the most bandwidth, but has the upside of requiring the fewest CPU resources. This option may also be used to make network debugging using tools like Wireshark easier.

CompressionMode COMPRESS_RANGE_CODER = 1

ENet's built-in range encoding. Works well on small packets, but is not the most efficient algorithm on packets larger than 4 KB.

CompressionMode COMPRESS_FASTLZ = 2

FastLZ compression. This option uses less CPU resources compared to COMPRESS_ZLIB, at the expense of using more bandwidth.

CompressionMode COMPRESS_ZLIB = 3

Zlib compression. This option uses less bandwidth compared to COMPRESS_FASTLZ, at the expense of using more CPU resources.

CompressionMode COMPRESS_ZSTD = 4

Zstandard compression. Note that this algorithm is not very efficient on packets smaller than 4 KB. Therefore, it's recommended to use other compression algorithms in most cases.

EventType EVENT_ERROR = -1

An error occurred during service(). You will likely need to destroy() the host and recreate it.

EventType EVENT_NONE = 0

No event occurred within the specified time limit.

EventType EVENT_CONNECT = 1

A connection request initiated by enet_host_connect has completed. The array will contain the peer which successfully connected.

EventType EVENT_DISCONNECT = 2

A peer has disconnected. This event is generated on a successful completion of a disconnect initiated by ENetPacketPeer.peer_disconnect(), if a peer has timed out, or if a connection request initialized by connect_to_host() has timed out. The array will contain the peer which disconnected. The data field contains user supplied data describing the disconnection, or 0, if none is available.

EventType EVENT_RECEIVE = 3

A packet has been received from a peer. The array will contain the peer which sent the packet and the channel number upon which the packet was received. The received packet will be queued to the associated ENetPacketPeer.

enum HostStatistic: 

HostStatistic HOST_TOTAL_SENT_DATA = 0

HostStatistic HOST_TOTAL_SENT_PACKETS = 1

Total UDP packets sent.

HostStatistic HOST_TOTAL_RECEIVED_DATA = 2

HostStatistic HOST_TOTAL_RECEIVED_PACKETS = 3

Total UDP packets received.

void bandwidth_limit(in_bandwidth: int = 0, out_bandwidth: int = 0) 

Adjusts the bandwidth limits of a host.

void broadcast(channel: int, packet: PackedByteArray, flags: int) 

Queues a packet to be sent to all peers associated with the host over the specified channel. See ENetPacketPeer FLAG_* constants for available packet flags.

void channel_limit(limit: int) 

Limits the maximum allowed channels of future incoming connections.

void compress(mode: CompressionMode) 

Sets the compression method used for network packets. These have different tradeoffs of compression speed versus bandwidth, you may need to test which one works best for your use case if you use compression at all.

Note: Most games' network design involve sending many small packets frequently (smaller than 4 KB each). If in doubt, it is recommended to keep the default compression algorithm as it works best on these small packets.

Note: The compression mode must be set to the same value on both the server and all its clients. Clients will fail to connect if the compression mode set on the client differs from the one set on the server.

ENetPacketPeer connect_to_host(address: String, port: int, channels: int = 0, data: int = 0) 

Initiates a connection to a foreign address using the specified port and allocating the requested channels. Optional data can be passed during connection in the form of a 32 bit integer.

Note: You must call either create_host() or create_host_bound() on both ends before calling this method.

Error create_host(max_peers: int = 32, max_channels: int = 0, in_bandwidth: int = 0, out_bandwidth: int = 0) 

Creates an ENetHost that allows up to max_peers connected peers, each allocating up to max_channels channels, optionally limiting bandwidth to in_bandwidth and out_bandwidth (if greater than zero).

This method binds a random available dynamic UDP port on the host machine at the unspecified address. Use create_host_bound() to specify the address and port.

Note: It is necessary to create a host in both client and server in order to establish a connection.

Error create_host_bound(bind_address: String, bind_port: int, max_peers: int = 32, max_channels: int = 0, in_bandwidth: int = 0, out_bandwidth: int = 0) 

Creates an ENetHost bound to the given bind_address and bind_port that allows up to max_peers connected peers, each allocating up to max_channels channels, optionally limiting bandwidth to in_bandwidth and out_bandwidth (if greater than zero).

Note: It is necessary to create a host in both client and server in order to establish a connection.

Destroys the host and all resources associated with it.

Error dtls_client_setup(hostname: String, client_options: TLSOptions = null) 

Configure this ENetHost to use the custom Godot extension allowing DTLS encryption for ENet clients. Call this before connect_to_host() to have ENet connect using DTLS validating the server certificate against hostname. You can pass the optional client_options parameter to customize the trusted certification authorities, or disable the common name verification. See TLSOptions.client() and TLSOptions.client_unsafe().

Error dtls_server_setup(server_options: TLSOptions) 

Configure this ENetHost to use the custom Godot extension allowing DTLS encryption for ENet servers. Call this right after create_host_bound() to have ENet expect peers to connect using DTLS. See TLSOptions.server().

Sends any queued packets on the host specified to its designated peers.

int get_local_port() const 

Returns the local port to which this peer is bound.

int get_max_channels() const 

Returns the maximum number of channels allowed for connected peers.

Array[ENetPacketPeer] get_peers() 

Returns the list of peers associated with this host.

Note: This list might include some peers that are not fully connected or are still being disconnected.

float pop_statistic(statistic: HostStatistic) 

Returns and resets host statistics.

void refuse_new_connections(refuse: bool) 

Configures the DTLS server to automatically drop new connections.

Note: This method is only relevant after calling dtls_server_setup().

Array service(timeout: int = 0) 

Waits for events on this connection and shuttles packets between the host and its peers, with the given timeout (in milliseconds). The returned Array will have 4 elements. An EventType, the ENetPacketPeer which generated the event, the event associated data (if any), the event associated channel (if any). If the generated event is EVENT_RECEIVE, the received packet will be queued to the associated ENetPacketPeer.

Call this function regularly to handle connections, disconnections, and to receive new packets.

Note: This method must be called on both ends involved in the event (sending and receiving hosts).

void socket_send(destination_address: String, destination_port: int, packet: PackedByteArray) 

Sends a packet toward a destination from the address and port currently bound by this ENetConnection instance.

This is useful as it serves to establish entries in NAT routing tables on all devices between this bound instance and the public facing internet, allowing a prospective client's connection packets to be routed backward through the NAT device(s) between the public internet and this host.

This requires forward knowledge of a prospective client's address and communication port as seen by the public internet - after any NAT devices have handled their connection request. This information can be obtained by a STUN service, and must be handed off to your host by an entity that is not the prospective client. This will never work for a client behind a Symmetric NAT due to the nature of the Symmetric NAT routing algorithm, as their IP and Port cannot be known beforehand.

Please read the User-contributed notes policy before submitting a comment.

---

## ENetMultiplayerPeer

**URL:** https://docs.godotengine.org/en/stable/classes/class_enetmultiplayerpeer.html

**Contents:**
- ENetMultiplayerPeer
- Description
- Tutorials
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: MultiplayerPeer < PacketPeer < RefCounted < Object

A MultiplayerPeer implementation using the ENet library.

A MultiplayerPeer implementation that should be passed to MultiplayerAPI.multiplayer_peer after being initialized as either a client, server, or mesh. Events can then be handled by connecting to MultiplayerAPI signals. See ENetConnection for more information on the ENet library wrapper.

Note: ENet only uses UDP, not TCP. When forwarding the server port to make your server accessible on the public Internet, you only need to forward the server port in UDP. You can use the UPNP class to try to forward the server port automatically when starting the server.

High-level multiplayer

API documentation on the ENet website

add_mesh_peer(peer_id: int, host: ENetConnection)

create_client(address: String, port: int, channel_count: int = 0, in_bandwidth: int = 0, out_bandwidth: int = 0, local_port: int = 0)

create_mesh(unique_id: int)

create_server(port: int, max_clients: int = 32, max_channels: int = 0, in_bandwidth: int = 0, out_bandwidth: int = 0)

get_peer(id: int) const

set_bind_ip(ip: String)

ENetConnection host 

ENetConnection get_host()

The underlying ENetConnection created after create_client() and create_server().

Error add_mesh_peer(peer_id: int, host: ENetConnection) 

Add a new remote peer with the given peer_id connected to the given host.

Note: The host must have exactly one peer in the ENetPacketPeer.STATE_CONNECTED state.

Error create_client(address: String, port: int, channel_count: int = 0, in_bandwidth: int = 0, out_bandwidth: int = 0, local_port: int = 0) 

Create client that connects to a server at address using specified port. The given address needs to be either a fully qualified domain name (e.g. "www.example.com") or an IP address in IPv4 or IPv6 format (e.g. "192.168.1.1"). The port is the port the server is listening on. The channel_count parameter can be used to specify the number of ENet channels allocated for the connection. The in_bandwidth and out_bandwidth parameters can be used to limit the incoming and outgoing bandwidth to the given number of bytes per second. The default of 0 means unlimited bandwidth. Note that ENet will strategically drop packets on specific sides of a connection between peers to ensure the peer's bandwidth is not overwhelmed. The bandwidth parameters also determine the window size of a connection which limits the amount of reliable packets that may be in transit at any given time. Returns @GlobalScope.OK if a client was created, @GlobalScope.ERR_ALREADY_IN_USE if this ENetMultiplayerPeer instance already has an open connection (in which case you need to call MultiplayerPeer.close() first) or @GlobalScope.ERR_CANT_CREATE if the client could not be created. If local_port is specified, the client will also listen to the given port; this is useful for some NAT traversal techniques.

Error create_mesh(unique_id: int) 

Initialize this MultiplayerPeer in mesh mode. The provided unique_id will be used as the local peer network unique ID once assigned as the MultiplayerAPI.multiplayer_peer. In the mesh configuration you will need to set up each new peer manually using ENetConnection before calling add_mesh_peer(). While this technique is more advanced, it allows for better control over the connection process (e.g. when dealing with NAT punch-through) and for better distribution of the network load (which would otherwise be more taxing on the server).

Error create_server(port: int, max_clients: int = 32, max_channels: int = 0, in_bandwidth: int = 0, out_bandwidth: int = 0) 

Create server that listens to connections via port. The port needs to be an available, unused port between 0 and 65535. Note that ports below 1024 are privileged and may require elevated permissions depending on the platform. To change the interface the server listens on, use set_bind_ip(). The default IP is the wildcard "*", which listens on all available interfaces. max_clients is the maximum number of clients that are allowed at once, any number up to 4095 may be used, although the achievable number of simultaneous clients may be far lower and depends on the application. For additional details on the bandwidth parameters, see create_client(). Returns @GlobalScope.OK if a server was created, @GlobalScope.ERR_ALREADY_IN_USE if this ENetMultiplayerPeer instance already has an open connection (in which case you need to call MultiplayerPeer.close() first) or @GlobalScope.ERR_CANT_CREATE if the server could not be created.

ENetPacketPeer get_peer(id: int) const 

Returns the ENetPacketPeer associated to the given id.

void set_bind_ip(ip: String) 

The IP used when creating a server. This is set to the wildcard "*" by default, which binds to all available interfaces. The given IP needs to be in IPv4 or IPv6 address format, for example: "192.168.1.1".

Please read the User-contributed notes policy before submitting a comment.

---

## ENetPacketPeer

**URL:** https://docs.godotengine.org/en/stable/classes/class_enetpacketpeer.html

**Contents:**
- ENetPacketPeer
- Description
- Tutorials
- Methods
- Enumerations
- Constants
- Method Descriptions
- User-contributed notes

Inherits: PacketPeer < RefCounted < Object

A wrapper class for an ENetPeer.

A PacketPeer implementation representing a peer of an ENetConnection.

This class cannot be instantiated directly but can be retrieved during ENetConnection.service() or via ENetConnection.get_peers().

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

API documentation on the ENet website

get_packet_flags() const

get_remote_address() const

get_remote_port() const

get_statistic(statistic: PeerStatistic)

peer_disconnect(data: int = 0)

peer_disconnect_later(data: int = 0)

peer_disconnect_now(data: int = 0)

ping_interval(ping_interval: int)

send(channel: int, packet: PackedByteArray, flags: int)

set_timeout(timeout: int, timeout_min: int, timeout_max: int)

throttle_configure(interval: int, acceleration: int, deceleration: int)

PeerState STATE_DISCONNECTED = 0

The peer is disconnected.

PeerState STATE_CONNECTING = 1

The peer is currently attempting to connect.

PeerState STATE_ACKNOWLEDGING_CONNECT = 2

The peer has acknowledged the connection request.

PeerState STATE_CONNECTION_PENDING = 3

The peer is currently connecting.

PeerState STATE_CONNECTION_SUCCEEDED = 4

The peer has successfully connected, but is not ready to communicate with yet (STATE_CONNECTED).

PeerState STATE_CONNECTED = 5

The peer is currently connected and ready to communicate with.

PeerState STATE_DISCONNECT_LATER = 6

The peer is expected to disconnect after it has no more outgoing packets to send.

PeerState STATE_DISCONNECTING = 7

The peer is currently disconnecting.

PeerState STATE_ACKNOWLEDGING_DISCONNECT = 8

The peer has acknowledged the disconnection request.

PeerState STATE_ZOMBIE = 9

The peer has lost connection, but is not considered truly disconnected (as the peer didn't acknowledge the disconnection request).

enum PeerStatistic: 

PeerStatistic PEER_PACKET_LOSS = 0

Mean packet loss of reliable packets as a ratio with respect to the PACKET_LOSS_SCALE.

PeerStatistic PEER_PACKET_LOSS_VARIANCE = 1

Packet loss variance.

PeerStatistic PEER_PACKET_LOSS_EPOCH = 2

The time at which packet loss statistics were last updated (in milliseconds since the connection started). The interval for packet loss statistics updates is 10 seconds, and at least one packet must have been sent since the last statistics update.

PeerStatistic PEER_ROUND_TRIP_TIME = 3

Mean packet round trip time for reliable packets.

PeerStatistic PEER_ROUND_TRIP_TIME_VARIANCE = 4

Variance of the mean round trip time.

PeerStatistic PEER_LAST_ROUND_TRIP_TIME = 5

Last recorded round trip time for a reliable packet.

PeerStatistic PEER_LAST_ROUND_TRIP_TIME_VARIANCE = 6

Variance of the last trip time recorded.

PeerStatistic PEER_PACKET_THROTTLE = 7

The peer's current throttle status.

PeerStatistic PEER_PACKET_THROTTLE_LIMIT = 8

The maximum number of unreliable packets that should not be dropped. This value is always greater than or equal to 1. The initial value is equal to PACKET_THROTTLE_SCALE.

PeerStatistic PEER_PACKET_THROTTLE_COUNTER = 9

Internal value used to increment the packet throttle counter. The value is hardcoded to 7 and cannot be changed. You probably want to look at PEER_PACKET_THROTTLE_ACCELERATION instead.

PeerStatistic PEER_PACKET_THROTTLE_EPOCH = 10

The time at which throttle statistics were last updated (in milliseconds since the connection started). The interval for throttle statistics updates is PEER_PACKET_THROTTLE_INTERVAL.

PeerStatistic PEER_PACKET_THROTTLE_ACCELERATION = 11

The throttle's acceleration factor. Higher values will make ENet adapt to fluctuating network conditions faster, causing unrelaible packets to be sent more often. The default value is 2.

PeerStatistic PEER_PACKET_THROTTLE_DECELERATION = 12

The throttle's deceleration factor. Higher values will make ENet adapt to fluctuating network conditions faster, causing unrelaible packets to be sent less often. The default value is 2.

PeerStatistic PEER_PACKET_THROTTLE_INTERVAL = 13

The interval over which the lowest mean round trip time should be measured for use by the throttle mechanism (in milliseconds). The default value is 5000.

PACKET_LOSS_SCALE = 65536 

The reference scale for packet loss. See get_statistic() and PEER_PACKET_LOSS.

PACKET_THROTTLE_SCALE = 32 

The reference value for throttle configuration. The default value is 32. See throttle_configure().

Mark the packet to be sent as reliable.

FLAG_UNSEQUENCED = 2 

Mark the packet to be sent unsequenced (unreliable).

FLAG_UNRELIABLE_FRAGMENT = 8 

Mark the packet to be sent unreliable even if the packet is too big and needs fragmentation (increasing the chance of it being dropped).

int get_channels() const 

Returns the number of channels allocated for communication with peer.

int get_packet_flags() const 

Returns the ENet flags of the next packet in the received queue. See FLAG_* constants for available packet flags. Note that not all flags are replicated from the sending peer to the receiving peer.

String get_remote_address() const 

Returns the IP address of this peer.

int get_remote_port() const 

Returns the remote port of this peer.

PeerState get_state() const 

Returns the current peer state.

float get_statistic(statistic: PeerStatistic) 

Returns the requested statistic for this peer.

bool is_active() const 

Returns true if the peer is currently active (i.e. the associated ENetConnection is still valid).

void peer_disconnect(data: int = 0) 

Request a disconnection from a peer. An ENetConnection.EVENT_DISCONNECT will be generated during ENetConnection.service() once the disconnection is complete.

void peer_disconnect_later(data: int = 0) 

Request a disconnection from a peer, but only after all queued outgoing packets are sent. An ENetConnection.EVENT_DISCONNECT will be generated during ENetConnection.service() once the disconnection is complete.

void peer_disconnect_now(data: int = 0) 

Force an immediate disconnection from a peer. No ENetConnection.EVENT_DISCONNECT will be generated. The foreign peer is not guaranteed to receive the disconnect notification, and is reset immediately upon return from this function.

Sends a ping request to a peer. ENet automatically pings all connected peers at regular intervals, however, this function may be called to ensure more frequent ping requests.

void ping_interval(ping_interval: int) 

Sets the ping_interval in milliseconds at which pings will be sent to a peer. Pings are used both to monitor the liveness of the connection and also to dynamically adjust the throttle during periods of low traffic so that the throttle has reasonable responsiveness during traffic spikes. The default ping interval is 500 milliseconds.

Forcefully disconnects a peer. The foreign host represented by the peer is not notified of the disconnection and will timeout on its connection to the local host.

Error send(channel: int, packet: PackedByteArray, flags: int) 

Queues a packet to be sent over the specified channel. See FLAG_* constants for available packet flags.

void set_timeout(timeout: int, timeout_min: int, timeout_max: int) 

Sets the timeout parameters for a peer. The timeout parameters control how and when a peer will timeout from a failure to acknowledge reliable traffic. Timeout values are expressed in milliseconds.

The timeout is a factor that, multiplied by a value based on the average round trip time, will determine the timeout limit for a reliable packet. When that limit is reached, the timeout will be doubled, and the peer will be disconnected if that limit has reached timeout_min. The timeout_max parameter, on the other hand, defines a fixed timeout for which any packet must be acknowledged or the peer will be dropped.

void throttle_configure(interval: int, acceleration: int, deceleration: int) 

Configures throttle parameter for a peer.

Unreliable packets are dropped by ENet in response to the varying conditions of the Internet connection to the peer. The throttle represents a probability that an unreliable packet should not be dropped and thus sent by ENet to the peer. By measuring fluctuations in round trip times of reliable packets over the specified interval, ENet will either increase the probability by the amount specified in the acceleration parameter, or decrease it by the amount specified in the deceleration parameter (both are ratios to PACKET_THROTTLE_SCALE).

When the throttle has a value of PACKET_THROTTLE_SCALE, no unreliable packets are dropped by ENet, and so 100% of all unreliable packets will be sent.

When the throttle has a value of 0, all unreliable packets are dropped by ENet, and so 0% of all unreliable packets will be sent.

Intermediate values for the throttle represent intermediate probabilities between 0% and 100% of unreliable packets being sent. The bandwidth limits of the local and foreign hosts are taken into account to determine a sensible limit for the throttle probability above which it should not raise even in the best of conditions.

Please read the User-contributed notes policy before submitting a comment.

---

## High-level multiplayer

**URL:** https://docs.godotengine.org/en/stable/tutorials/networking/high_level_multiplayer.html

**Contents:**
- High-level multiplayer
- High-level vs low-level API
- Mid-level abstraction
- Hosting considerations
- Initializing the network
- Managing connections
- Remote procedure calls
- Channels
- Example lobby implementation
- Exporting for dedicated servers

The following explains the differences of high- and low-level networking in Godot as well as some fundamentals. If you want to jump in head-first and add networking to your first nodes, skip to Initializing the network below. But make sure to read the rest later on!

Godot always supported standard low-level networking via UDP, TCP and some higher-level protocols such as HTTP and SSL. These protocols are flexible and can be used for almost anything. However, using them to synchronize game state manually can be a large amount of work. Sometimes that work can't be avoided or is worth it, for example when working with a custom server implementation on the backend. But in most cases, it's worthwhile to consider Godot's high-level networking API, which sacrifices some of the fine-grained control of low-level networking for greater ease of use.

This is due to the inherent limitations of the low-level protocols:

TCP ensures packets will always arrive reliably and in order, but latency is generally higher due to error correction. It's also quite a complex protocol because it understands what a "connection" is, and optimizes for goals that often don't suit applications like multiplayer games. Packets are buffered to be sent in larger batches, trading less per-packet overhead for higher latency. This can be useful for things like HTTP, but generally not for games. Some of this can be configured and disabled (e.g. by disabling "Nagle's algorithm" for the TCP connection).

UDP is a simpler protocol, which only sends packets (and has no concept of a "connection"). No error correction makes it pretty quick (low latency), but packets may be lost along the way or received in the wrong order. Added to that, the MTU (maximum packet size) for UDP is generally low (only a few hundred bytes), so transmitting larger packets means splitting them, reorganizing them and retrying if a part fails.

In general, TCP can be thought of as reliable, ordered, and slow; UDP as unreliable, unordered and fast. Because of the large difference in performance, it often makes sense to re-build the parts of TCP wanted for games (optional reliability and packet order), while avoiding the unwanted parts (congestion/traffic control features, Nagle's algorithm, etc). Due to this, most game engines come with such an implementation, and Godot is no exception.

In summary, you can use the low-level networking API for maximum control and implement everything on top of bare network protocols or use the high-level API based on SceneTree that does most of the heavy lifting behind the scenes in a generally optimized way.

Most of Godot's supported platforms offer all or most of the mentioned high- and low-level networking features. As networking is always largely hardware and operating system dependent, however, some features may change or not be available on some target platforms. Most notably, the HTML5 platform currently offers WebSockets and WebRTC support but lacks some of the higher-level features, as well as raw access to low-level protocols like TCP and UDP.

More about TCP/IP, UDP, and networking: https://gafferongames.com/post/udp_vs_tcp/

Gaffer On Games has a lot of useful articles about networking in Games (here), including the comprehensive introduction to networking models in games.

Adding networking to your game comes with some responsibility. It can make your application vulnerable if done wrong and may lead to cheats or exploits. It may even allow an attacker to compromise the machines your application runs on and use your servers to send spam, attack others or steal your users' data if they play your game.

This is always the case when networking is involved and has nothing to do with Godot. You can of course experiment, but when you release a networked application, always take care of any possible security concerns.

Before going into how we would like to synchronize a game across the network, it can be helpful to understand how the base network API for synchronization works.

Godot uses a mid-level object MultiplayerPeer. This object is not meant to be created directly, but is designed so that several C++ implementations can provide it.

This object extends from PacketPeer, so it inherits all the useful methods for serializing, sending and receiving data. On top of that, it adds methods to set a peer, transfer mode, etc. It also includes signals that will let you know when peers connect or disconnect.

This class interface can abstract most types of network layers, topologies and libraries. By default, Godot provides an implementation based on ENet (ENetMultiplayerPeer), one based on WebRTC (WebRTCMultiplayerPeer), and one based on WebSocket (WebSocketPeer), but this could be used to implement mobile APIs (for ad hoc WiFi, Bluetooth) or custom device/console-specific networking APIs.

For most common cases, using this object directly is discouraged, as Godot provides even higher level networking facilities. This object is still made available in case a game has specific needs for a lower-level API.

When hosting a server, clients on your LAN can connect using the internal IP address which is usually of the form 192.168.*.*. This internal IP address is not reachable by non-LAN/Internet clients.

On Windows, you can find your internal IP address by opening a command prompt and entering ipconfig. On macOS, open a Terminal and enter ifconfig. On Linux, open a terminal and enter ip addr.

If you're hosting a server on your own machine and want non-LAN clients to connect to it, you'll probably have to forward the server port on your router. This is required to make your server reachable from the Internet since most residential connections use a NAT. Godot's high-level multiplayer API only uses UDP, so you must forward the port in UDP, not just TCP.

After forwarding a UDP port and making sure your server uses that port, you can use this website to find your public IP address. Then give this public IP address to any Internet clients that wish to connect to your server.

Godot's high-level multiplayer API uses a modified version of ENet which allows for full IPv6 support.

High-level networking in Godot is managed by the SceneTree.

Each node has a multiplayer property, which is a reference to the MultiplayerAPI instance configured for it by the scene tree. Initially, every node is configured with the same default MultiplayerAPI object.

It is possible to create a new MultiplayerAPI object and assign it to a NodePath in the scene tree, which will override multiplayer for the node at that path and all of its descendants. This allows sibling nodes to be configured with different peers, which makes it possible to run a server and a client simultaneously in one instance of Godot.

To initialize networking, a MultiplayerPeer object must be created, initialized as a server or client, and passed to the MultiplayerAPI.

To terminate networking:

When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

Every peer is assigned a unique ID. The server's ID is always 1, and clients are assigned a random positive integer.

Responding to connections or disconnections is possible by connecting to MultiplayerAPI's signals:

peer_connected(id: int) This signal is emitted with the newly connected peer's ID on each other peer, and on the new peer multiple times, once with each other peer's ID.

peer_disconnected(id: int) This signal is emitted on every remaining peer when one disconnects.

The rest are only emitted on clients:

connected_to_server()

server_disconnected()

To get the unique ID of the associated peer:

To check whether the peer is server or client:

Remote procedure calls, or RPCs, are functions that can be called on other peers. To create one, use the @rpc annotation before a function definition. To call an RPC, use Callable's method rpc() to call in every peer, or rpc_id() to call in a specific peer.

RPCs will not serialize objects or callables.

For a remote call to be successful, the sending and receiving node need to have the same NodePath, which means they must have the same name. When using add_child() for nodes which are expected to use RPCs, set the argument force_readable_name to true.

If a function is annotated with @rpc on the client script (resp. server script), then this function must also be declared on the server script (resp. client script). Both RPCs must have the same signature which is evaluated with a checksum of all RPCs. All RPCs in a script are checked at once, and all RPCs must be declared on both the client scripts and the server scripts, even functions that are currently not in use.

The signature of the RPC includes the @rpc() declaration, the function, return type, and the NodePath. If an RPC resides in a script attached to /root/Main/Node1, then it must reside in precisely the same path and node on both the client script and the server script. Function arguments are not checked for matching between the server and client code (example: func sendstuff(): and func sendstuff(arg1, arg2): will pass signature matching).

If these conditions are not met (if all RPCs do not pass signature matching), the script may print an error or cause unwanted behavior. The error message may be unrelated to the RPC function you are currently building and testing.

See further explanation and troubleshooting on this post.

The annotation can take a number of arguments, which have default values. @rpc is equivalent to:

The parameters and their functions are as follows:

"authority": Only the multiplayer authority can call remotely. The authority is the server by default, but can be changed per-node using Node.set_multiplayer_authority.

"any_peer": Clients are allowed to call remotely. Useful for transferring user input.

"call_remote": The function will not be called on the local peer.

"call_local": The function can be called on the local peer. Useful when the server is also a player.

"unreliable" Packets are not acknowledged, can be lost, and can arrive at any order.

"unreliable_ordered" Packets are received in the order they were sent in. This is achieved by ignoring packets that arrive later if another that was sent after them has already been received. Can cause packet loss if used incorrectly.

"reliable" Resend attempts are sent until packets are acknowledged, and their order is preserved. Has a significant performance penalty.

transfer_channel is the channel index.

The first 3 can be passed in any order, but transfer_channel must always be last.

The function multiplayer.get_remote_sender_id() can be used to get the unique id of an rpc sender, when used within the function called by rpc.

Modern networking protocols support channels, which are separate connections within the connection. This allows for multiple streams of packets that do not interfere with each other.

For example, game chat related messages and some of the core gameplay messages should all be sent reliably, but a gameplay message should not wait for a chat message to be acknowledged. This can be achieved by using different channels.

Channels are also useful when used with the unreliable ordered transfer mode. Sending packets of variable size with this transfer mode can cause packet loss, since packets which are slower to arrive are ignored. Separating them into multiple streams of homogeneous packets by using channels allows ordered transfer with little packet loss, and without the latency penalty caused by reliable mode.

The default channel with index 0 is actually three different channels - one for each transfer mode.

This is an example lobby that can handle peers joining and leaving, notify UI scenes through signals, and start the game after all clients have loaded the game scene.

The game scene's root node should be named Game. In the script attached to it:

Once you've made a multiplayer game, you may want to export it to run it on a dedicated server with no GPU available. See Exporting for dedicated servers for more information.

The code samples on this page aren't designed to run on a dedicated server. You'll have to modify them so the server isn't considered to be a player. You'll also have to modify the game starting mechanism so that the first player who joins can start the game.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (markdown):
```markdown
# By default, these expressions are interchangeable.
multiplayer # Get the MultiplayerAPI object configured for this node.
get_tree().get_multiplayer() # Get the default MultiplayerAPI object.
```

Example 2 (unknown):
```unknown
// By default, these expressions are interchangeable.
Multiplayer; // Get the MultiplayerAPI object configured for this node.
GetTree().GetMultiplayer(); // Get the default MultiplayerAPI object.
```

Example 3 (gdscript):
```gdscript
# Create client.
var peer = ENetMultiplayerPeer.new()
peer.create_client(IP_ADDRESS, PORT)
multiplayer.multiplayer_peer = peer

# Create server.
var peer = ENetMultiplayerPeer.new()
peer.create_server(PORT, MAX_CLIENTS)
multiplayer.multiplayer_peer = peer
```

Example 4 (gdscript):
```gdscript
// Create client.
var peer = new ENetMultiplayerPeer();
peer.CreateClient(IPAddress, Port);
Multiplayer.MultiplayerPeer = peer;

// Create server.
var peer = new ENetMultiplayerPeer();
peer.CreateServer(Port, MaxClients);
Multiplayer.MultiplayerPeer = peer;
```

---

## HTTP client class

**URL:** https://docs.godotengine.org/en/stable/tutorials/networking/http_client_class.html

**Contents:**
- HTTP client class
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

HTTPClient provides low-level access to HTTP communication. For a higher-level interface, you may want to take a look at HTTPRequest first, which has a tutorial available here.

When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

Here's an example of using the HTTPClient class. It's just a script, so it can be run by executing:

It will connect and fetch a website.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (yaml):
```yaml
c:\godot> godot -s http_test.gd
```

Example 2 (yaml):
```yaml
c:\godot> godot -s HTTPTest.cs
```

Example 3 (gdscript):
```gdscript
extends SceneTree

# HTTPClient demo
# This simple class can do HTTP requests; it will not block, but it needs to be polled.

func _init():
    var err = 0
    var http = HTTPClient.new() # Create the Client.

    err = http.connect_to_host("www.php.net", 80) # Connect to host/port.
    assert(err == OK) # Make sure connection is OK.

    # Wait until resolved and connected.
    while http.get_status() == HTTPClient.STATUS_CONNECTING or http.get_status() == HTTPClient.STATUS_RESOLVING:
        http.poll()
        print("Connecting...")
        await get_tree().process_frame

    assert(http.get_status() == HTTPClient.STATUS_CONNECTED) # Check if the connection was made successfully.

    # Some headers
    var headers = [
        "User-Agent: Pirulo/1.0 (Godot)",
        "Accept: */*"
    ]

    err = http.request(HTTPClient.METHOD_GET, "/ChangeLog-5.php", headers) # Request a page from the site (this one was chunked..)
    assert(err == OK) # Make sure all is OK.

    while http.get_status() == HTTPClient.STATUS_REQUESTING:
        # Keep polling for as long as the request is being processed.
        http.poll()
        print("Requesting...")
        await get_tree().process_frame

    assert(http.get_status() == HTTPClient.STATUS_BODY or http.get_status() == HTTPClient.STATUS_CONNECTED) # Make sure request finished well.

    print("response? ", http.has_response()) # Site might not have a response.

    if http.has_response():
        # If there is a response...

        headers = http.get_response_headers_as_dictionary() # Get response headers.
        print("code: ", http.get_response_code()) # Show response code.
        print("**headers:\\n", headers) # Show headers.

        # Getting the HTTP Body

        if http.is_response_chunked():
            # Does it use chunks?
            print("Response is Chunked!")
        else:
            # Or just plain Content-Length
            var bl = http.get_response_body_length()
            print("Response Length: ", bl)

        # This method works for both anyway

        var rb = PackedByteArray() # Array that will hold the data.

        while http.get_status() == HTTPClient.STATUS_BODY:
            # While there is body left to be read
            http.poll()
            # Get a chunk.
            var chunk = http.read_response_body_chunk()
            if chunk.size() == 0:
                await get_tree().process_frame
            else:
                rb = rb + chunk # Append to read buffer.
        # Done!

        print("bytes got: ", rb.size())
        var text = rb.get_string_from_ascii()
        print("Text: ", text)

    quit()
```

Example 4 (swift):
```swift
using Godot;

public partial class HTTPTest : SceneTree
{
    // HTTPClient demo.
    // This simple class can make HTTP requests; it will not block, but it needs to be polled.
    public override async void _Initialize()
    {
        Error err;
        HTTPClient http = new HTTPClient(); // Create the client.

        err = http.ConnectToHost("www.php.net", 80); // Connect to host/port.
        Debug.Assert(err == Error.Ok); // Make sure the connection is OK.

        // Wait until resolved and connected.
        while (http.GetStatus() == HTTPClient.Status.Connecting || http.GetStatus() == HTTPClient.Status.Resolving)
        {
            http.Poll();
            GD.Print("Connecting...");
            OS.DelayMsec(500);
        }

        Debug.Assert(http.GetStatus() == HTTPClient.Status.Connected); // Check if the connection was made successfully.

        // Some headers.
        string[] headers =
        [
            "User-Agent: Pirulo/1.0 (Godot)",
            "Accept: */*",
        ];

        err = http.Request(HTTPClient.Method.Get, "/ChangeLog-5.php", headers); // Request a page from the site.
        Debug.Assert(err == Error.Ok); // Make sure all is OK.

        // Keep polling for as long as the request is being processed.
        while (http.GetStatus() == HTTPClient.Status.Requesting)
        {
            http.Poll();
            GD.Print("Requesting...");
            if (OS.HasFeature("web"))
            {
                // Synchronous HTTP requests are not supported on the web,
                // so wait for the next main loop iteration.
                await ToSignal(Engine.GetMainLoop(), "idle_frame");
            }
            else
            {
                OS.DelayMsec(500);
            }
        }

        Debug.Assert(http.GetStatus() == HTTPClient.Status.Body || http.GetStatus() == HTTPClient.Status.Connected); // Make sure the request finished well.

        GD.Print("Response? ", http.HasResponse()); // The site might not have a response.

        // If there is a response...
        if (http.HasResponse())
        {
            headers = http.GetResponseHeaders(); // Get response headers.
            GD.Print("Code: ", http.GetResponseCode()); // Show response code.
            GD.Print("Headers:");
            foreach (string header in headers)
            {
                // Show headers.
                GD.Print(header);
            }

            if (http.IsResponseChunked())
            {
                // Does it use chunks?
                GD.Print("Response is Chunked!");
            }
            else
            {
                // Or just Content-Length.
                GD.Print("Response Length: ", http.GetResponseBodyLength());
            }

            // This method works for both anyways.
            List<byte> rb = new List<byte>(); // List that will hold the data.

            // While there is data left to be read...
            while (http.GetStatus() == HTTPClient.Status.Body)
            {
                http.Poll();
                byte[] chunk = http.ReadResponseBodyChunk(); // Read a chunk.
                if (chunk.Length == 0)
                {
                    // If nothing was read, wait for the buffer to fill.
                    OS.DelayMsec(500);
                }
                else
                {
                    // Append the chunk to the read buffer.
                    rb.AddRange(chunk);
                }
            }

            // Done!
            GD.Print("Bytes Downloaded: ", rb.Count);
            string text = Encoding.ASCII.GetString(rb.ToArray());
            GD.Print(text);
        }
        Quit();
    }
}
```

---

## JSONRPC

**URL:** https://docs.godotengine.org/en/stable/classes/class_jsonrpc.html

**Contents:**
- JSONRPC
- Description
- Methods
- Enumerations
- Method Descriptions
- User-contributed notes

A helper to handle dictionaries which look like JSONRPC documents.

JSON-RPC is a standard which wraps a method call in a JSON object. The object has a particular structure and identifies which method is called, the parameters to that function, and carries an ID to keep track of responses. This class implements that standard on top of Dictionary; you will have to convert between a Dictionary and JSON with other functions.

make_notification(method: String, params: Variant)

make_request(method: String, params: Variant, id: Variant)

make_response(result: Variant, id: Variant)

make_response_error(code: int, message: String, id: Variant = null) const

process_action(action: Variant, recurse: bool = false)

process_string(action: String)

set_method(name: String, callback: Callable)

ErrorCode PARSE_ERROR = -32700

The request could not be parsed as it was not valid by JSON standard (JSON.parse() failed).

ErrorCode INVALID_REQUEST = -32600

A method call was requested but the request's format is not valid.

ErrorCode METHOD_NOT_FOUND = -32601

A method call was requested but no function of that name existed in the JSONRPC subclass.

ErrorCode INVALID_PARAMS = -32602

A method call was requested but the given method parameters are not valid. Not used by the built-in JSONRPC.

ErrorCode INTERNAL_ERROR = -32603

An internal error occurred while processing the request. Not used by the built-in JSONRPC.

Dictionary make_notification(method: String, params: Variant) 

Returns a dictionary in the form of a JSON-RPC notification. Notifications are one-shot messages which do not expect a response.

method: Name of the method being called.

params: An array or dictionary of parameters being passed to the method.

Dictionary make_request(method: String, params: Variant, id: Variant) 

Returns a dictionary in the form of a JSON-RPC request. Requests are sent to a server with the expectation of a response. The ID field is used for the server to specify which exact request it is responding to.

method: Name of the method being called.

params: An array or dictionary of parameters being passed to the method.

id: Uniquely identifies this request. The server is expected to send a response with the same ID.

Dictionary make_response(result: Variant, id: Variant) 

When a server has received and processed a request, it is expected to send a response. If you did not want a response then you need to have sent a Notification instead.

result: The return value of the function which was called.

id: The ID of the request this response is targeted to.

Dictionary make_response_error(code: int, message: String, id: Variant = null) const 

Creates a response which indicates a previous reply has failed in some way.

code: The error code corresponding to what kind of error this is. See the ErrorCode constants.

message: A custom message about this error.

id: The request this error is a response to.

Variant process_action(action: Variant, recurse: bool = false) 

Given a Dictionary which takes the form of a JSON-RPC request: unpack the request and run it. Methods are resolved by looking at the field called "method" and looking for an equivalently named function in the JSONRPC object. If one is found that method is called.

To add new supported methods extend the JSONRPC class and call process_action() on your subclass.

action: The action to be run, as a Dictionary in the form of a JSON-RPC request or notification.

String process_string(action: String) 

There is currently no description for this method. Please help us by contributing one!

void set_method(name: String, callback: Callable) 

Registers a callback for the given method name.

name The name that clients can use to access the callback.

callback The callback which will handle the specific method.

Please read the User-contributed notes policy before submitting a comment.

---

## Making HTTP requests

**URL:** https://docs.godotengine.org/en/stable/tutorials/networking/http_request_class.html

**Contents:**
- Making HTTP requests
- Why use HTTP?
- HTTP requests in Godot
- Preparing the scene
- Scripting the request
- Sending data to the server
- Setting custom HTTP headers
- User-contributed notes

HTTP requests are useful to communicate with web servers and other non-Godot programs.

Compared to Godot's other networking features (like High-level multiplayer), HTTP requests have more overhead and take more time to get going, so they aren't suited for real-time communication, and aren't great to send lots of small updates as is common for multiplayer gameplay.

HTTP, however, offers interoperability with external web resources and is great at sending and receiving large amounts of data, for example to transfer files like game assets. These assets can then be loaded using runtime file loading and saving.

So HTTP may be useful for your game's login system, lobby browser, to retrieve some information from the web or to download game assets.

The HTTPRequest node is the easiest way to make HTTP requests in Godot. It is backed by the more low-level HTTPClient, for which a tutorial is available here.

For this example, we will make an HTTP request to GitHub to retrieve the name of the latest Godot release.

When exporting to Android, make sure to enable the Internet permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by the Android OS.

Create a new empty scene, add a root Node and add a script to it. Then add an HTTPRequest node as a child.

When the project is started (so in _ready()), we're going to send an HTTP request to Github using our HTTPRequest node, and once the request completes, we're going to parse the returned JSON data, look for the name field and print that to console.

Save the script and the scene, and run the project. The name of the most recent Godot release on Github should be printed to the output log. For more information on parsing JSON, see the class references for JSON.

Note that you may want to check whether the result equals RESULT_SUCCESS and whether a JSON parsing error occurred, see the JSON class reference and HTTPRequest for more.

You have to wait for a request to finish before sending another one. Making multiple request at once requires you to have one node per request. A common strategy is to create and delete HTTPRequest nodes at runtime as necessary.

Until now, we have limited ourselves to requesting data from a server. But what if you need to send data to the server? Here is a common way of doing it:

Of course, you can also set custom HTTP headers. These are given as a string array, with each string containing a header in the format "header: value". For example, to set a custom user agent (the HTTP User-Agent header) you could use the following:

Be aware that someone might analyse and decompile your released application and thus may gain access to any embedded authorization information like tokens, usernames or passwords. That means it is usually not a good idea to embed things such as database access credentials inside your game. Avoid providing information useful to an attacker whenever possible.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node

func _ready():
    $HTTPRequest.request_completed.connect(_on_request_completed)
    $HTTPRequest.request("https://api.github.com/repos/godotengine/godot/releases/latest")

func _on_request_completed(result, response_code, headers, body):
    var json = JSON.parse_string(body.get_string_from_utf8())
    print(json["name"])
```

Example 2 (swift):
```swift
using Godot;
using System.Text;

public partial class MyNode : Node
{
    public override void _Ready()
    {
        HttpRequest httpRequest = GetNode<HttpRequest>("HTTPRequest");
        httpRequest.RequestCompleted += OnRequestCompleted;
        httpRequest.Request("https://api.github.com/repos/godotengine/godot/releases/latest");
    }

    private void OnRequestCompleted(long result, long responseCode, string[] headers, byte[] body)
    {
        Godot.Collections.Dictionary json = Json.ParseString(Encoding.UTF8.GetString(body)).AsGodotDictionary();
        GD.Print(json["name"]);
    }
}
```

Example 3 (gdscript):
```gdscript
var json = JSON.stringify(data_to_send)
var headers = ["Content-Type: application/json"]
$HTTPRequest.request(url, headers, HTTPClient.METHOD_POST, json)
```

Example 4 (csharp):
```csharp
string json = Json.Stringify(dataToSend);
string[] headers = ["Content-Type: application/json"];
HttpRequest httpRequest = GetNode<HttpRequest>("HTTPRequest");
httpRequest.Request(url, headers, HttpClient.Method.Post, json);
```

---

## MultiplayerAPIExtension

**URL:** https://docs.godotengine.org/en/stable/classes/class_multiplayerapiextension.html

**Contents:**
- MultiplayerAPIExtension
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: MultiplayerAPI < RefCounted < Object

Base class used for extending the MultiplayerAPI.

This class can be used to extend or replace the default MultiplayerAPI implementation via script or extensions.

The following example extend the default implementation (SceneMultiplayer) by logging every RPC being made, and every object being configured for replication.

Then in your main scene or in an autoload call SceneTree.set_multiplayer() to start using your custom MultiplayerAPI:

Native extensions can alternatively use the MultiplayerAPI.set_default_interface() method during initialization to configure themselves as the default implementation.

_get_multiplayer_peer() virtual

_get_peer_ids() virtual const

_get_remote_sender_id() virtual const

_get_unique_id() virtual const

_object_configuration_add(object: Object, configuration: Variant) virtual

_object_configuration_remove(object: Object, configuration: Variant) virtual

_rpc(peer: int, object: Object, method: StringName, args: Array) virtual

_set_multiplayer_peer(multiplayer_peer: MultiplayerPeer) virtual

MultiplayerPeer _get_multiplayer_peer() virtual 

Called when the MultiplayerAPI.multiplayer_peer is retrieved.

PackedInt32Array _get_peer_ids() virtual const 

Callback for MultiplayerAPI.get_peers().

int _get_remote_sender_id() virtual const 

Callback for MultiplayerAPI.get_remote_sender_id().

int _get_unique_id() virtual const 

Callback for MultiplayerAPI.get_unique_id().

Error _object_configuration_add(object: Object, configuration: Variant) virtual 

Callback for MultiplayerAPI.object_configuration_add().

Error _object_configuration_remove(object: Object, configuration: Variant) virtual 

Callback for MultiplayerAPI.object_configuration_remove().

Error _poll() virtual 

Callback for MultiplayerAPI.poll().

Error _rpc(peer: int, object: Object, method: StringName, args: Array) virtual 

Callback for MultiplayerAPI.rpc().

void _set_multiplayer_peer(multiplayer_peer: MultiplayerPeer) virtual 

Called when the MultiplayerAPI.multiplayer_peer is set.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends MultiplayerAPIExtension
class_name LogMultiplayer

# We want to extend the default SceneMultiplayer.
var base_multiplayer = SceneMultiplayer.new()

func _init():
    # Just passthrough base signals (copied to var to avoid cyclic reference)
    var cts = connected_to_server
    var cf = connection_failed
    var sd = server_disconnected
    var pc = peer_connected
    var pd = peer_disconnected
    base_multiplayer.connected_to_server.connect(func(): cts.emit())
    base_multiplayer.connection_failed.connect(func(): cf.emit())
    base_multiplayer.server_disconnected.connect(func(): sd.emit())
    base_multiplayer.peer_connected.connect(func(id): pc.emit(id))
    base_multiplayer.peer_disconnected.connect(func(id): pd.emit(id))

func _poll():
    return base_multiplayer.poll()

# Log RPC being made and forward it to the default multiplayer.
func _rpc(peer: int, object: Object, method: StringName, args: Array) -> Error:
    print("Got RPC for %d: %s::%s(%s)" % [peer, object, method, args])
    return base_multiplayer.rpc(peer, object, method, args)

# Log configuration add. E.g. root path (nullptr, NodePath), replication (Node, Spawner|Synchronizer), custom.
func _object_configuration_add(object, config: Variant) -> Error:
    if config is MultiplayerSynchronizer:
        print("Adding synchronization configuration for %s. Synchronizer: %s" % [object, config])
    elif config is MultiplayerSpawner:
        print("Adding node %s to the spawn list. Spawner: %s" % [object, config])
    return base_multiplayer.object_configuration_add(object, config)

# Log configuration remove. E.g. root path (nullptr, NodePath), replication (Node, Spawner|Synchronizer), custom.
func _object_configuration_remove(object, config: Variant) -> Error:
    if config is MultiplayerSynchronizer:
        print("Removing synchronization configuration for %s. Synchronizer: %s" % [object, config])
    elif config is MultiplayerSpawner:
        print("Removing node %s from the spawn list. Spawner: %s" % [object, config])
    return base_multiplayer.object_configuration_remove(object, config)

# These can be optional, but in our case we want to extend SceneMultiplayer, so forward everything.
func _set_multiplayer_peer(p_peer: MultiplayerPeer):
    base_multiplayer.multiplayer_peer = p_peer

func _get_multiplayer_peer() -> MultiplayerPeer:
    return base_multiplayer.multiplayer_peer

func _get_unique_id() -> int:
    return base_multiplayer.get_unique_id()

func _get_remote_sender_id() -> int:
    return base_multiplayer.get_remote_sender_id()

func _get_peer_ids() -> PackedInt32Array:
    return base_multiplayer.get_peers()
```

Example 2 (go):
```go
# autoload.gd
func _enter_tree():
    # Sets our custom multiplayer as the main one in SceneTree.
    get_tree().set_multiplayer(LogMultiplayer.new())
```

---

## MultiplayerAPI

**URL:** https://docs.godotengine.org/en/stable/classes/class_multiplayerapi.html

**Contents:**
- MultiplayerAPI
- Description
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Inherited By: MultiplayerAPIExtension, SceneMultiplayer

High-level multiplayer API interface.

Base class for high-level multiplayer API implementations. See also MultiplayerPeer.

By default, SceneTree has a reference to an implementation of this class and uses it to provide multiplayer capabilities (i.e. RPCs) across the whole scene.

It is possible to override the MultiplayerAPI instance used by specific tree branches by calling the SceneTree.set_multiplayer() method, effectively allowing to run both client and server in the same scene.

It is also possible to extend or replace the default implementation via scripting or native extensions. See MultiplayerAPIExtension for details about extensions, SceneMultiplayer for the details about the default implementation.

create_default_interface() static

get_default_interface() static

get_remote_sender_id()

has_multiplayer_peer()

object_configuration_add(object: Object, configuration: Variant)

object_configuration_remove(object: Object, configuration: Variant)

rpc(peer: int, object: Object, method: StringName, arguments: Array = [])

set_default_interface(interface_name: StringName) static

connected_to_server() 

Emitted when this MultiplayerAPI's multiplayer_peer successfully connected to a server. Only emitted on clients.

connection_failed() 

Emitted when this MultiplayerAPI's multiplayer_peer fails to establish a connection to a server. Only emitted on clients.

peer_connected(id: int) 

Emitted when this MultiplayerAPI's multiplayer_peer connects with a new peer. ID is the peer ID of the new peer. Clients get notified when other clients connect to the same server. Upon connecting to a server, a client also receives this signal for the server (with ID being 1).

peer_disconnected(id: int) 

Emitted when this MultiplayerAPI's multiplayer_peer disconnects from a peer. Clients get notified when other clients disconnect from the same server.

server_disconnected() 

Emitted when this MultiplayerAPI's multiplayer_peer disconnects from server. Only emitted on clients.

RPCMode RPC_MODE_DISABLED = 0

Used with Node.rpc_config() to disable a method or property for all RPC calls, making it unavailable. Default for all methods.

RPCMode RPC_MODE_ANY_PEER = 1

Used with Node.rpc_config() to set a method to be callable remotely by any peer. Analogous to the @rpc("any_peer") annotation. Calls are accepted from all remote peers, no matter if they are node's authority or not.

RPCMode RPC_MODE_AUTHORITY = 2

Used with Node.rpc_config() to set a method to be callable remotely only by the current multiplayer authority (which is the server by default). Analogous to the @rpc("authority") annotation. See Node.set_multiplayer_authority().

MultiplayerPeer multiplayer_peer 

void set_multiplayer_peer(value: MultiplayerPeer)

MultiplayerPeer get_multiplayer_peer()

The peer object to handle the RPC system (effectively enabling networking when set). Depending on the peer itself, the MultiplayerAPI will become a network server (check with is_server()) and will set root node's network mode to authority, or it will become a regular client peer. All child nodes are set to inherit the network mode by default. Handling of networking-related events (connection, disconnection, new clients) is done by connecting to MultiplayerAPI's signals.

MultiplayerAPI create_default_interface() static 

Returns a new instance of the default MultiplayerAPI.

StringName get_default_interface() static 

Returns the default MultiplayerAPI implementation class name. This is usually "SceneMultiplayer" when SceneMultiplayer is available. See set_default_interface().

PackedInt32Array get_peers() 

Returns the peer IDs of all connected peers of this MultiplayerAPI's multiplayer_peer.

int get_remote_sender_id() 

Returns the sender's peer ID for the RPC currently being executed.

Note: This method returns 0 when called outside of an RPC. As such, the original peer ID may be lost when code execution is delayed (such as with GDScript's await keyword).

int get_unique_id() 

Returns the unique peer ID of this MultiplayerAPI's multiplayer_peer.

bool has_multiplayer_peer() 

Returns true if there is a multiplayer_peer set.

Returns true if this MultiplayerAPI's multiplayer_peer is valid and in server mode (listening for connections).

Error object_configuration_add(object: Object, configuration: Variant) 

Notifies the MultiplayerAPI of a new configuration for the given object. This method is used internally by SceneTree to configure the root path for this MultiplayerAPI (passing null and a valid NodePath as configuration). This method can be further used by MultiplayerAPI implementations to provide additional features, refer to specific implementation (e.g. SceneMultiplayer) for details on how they use it.

Note: This method is mostly relevant when extending or overriding the MultiplayerAPI behavior via MultiplayerAPIExtension.

Error object_configuration_remove(object: Object, configuration: Variant) 

Notifies the MultiplayerAPI to remove a configuration for the given object. This method is used internally by SceneTree to configure the root path for this MultiplayerAPI (passing null and an empty NodePath as configuration). This method can be further used by MultiplayerAPI implementations to provide additional features, refer to specific implementation (e.g. SceneMultiplayer) for details on how they use it.

Note: This method is mostly relevant when extending or overriding the MultiplayerAPI behavior via MultiplayerAPIExtension.

Method used for polling the MultiplayerAPI. You only need to worry about this if you set SceneTree.multiplayer_poll to false. By default, SceneTree will poll its MultiplayerAPI(s) for you.

Note: This method results in RPCs being called, so they will be executed in the same context of this function (e.g. _process, physics, Thread).

Error rpc(peer: int, object: Object, method: StringName, arguments: Array = []) 

Sends an RPC to the target peer. The given method will be called on the remote object with the provided arguments. The RPC may also be called locally depending on the implementation and RPC configuration. See Node.rpc() and Node.rpc_config().

Note: Prefer using Node.rpc(), Node.rpc_id(), or my_method.rpc(peer, arg1, arg2, ...) (in GDScript), since they are faster. This method is mostly useful in conjunction with MultiplayerAPIExtension when extending or replacing the multiplayer capabilities.

void set_default_interface(interface_name: StringName) static 

Sets the default MultiplayerAPI implementation class. This method can be used by modules and extensions to configure which implementation will be used by SceneTree when the engine starts.

Please read the User-contributed notes policy before submitting a comment.

---

## MultiplayerPeerExtension

**URL:** https://docs.godotengine.org/en/stable/classes/class_multiplayerpeerextension.html

**Contents:**
- MultiplayerPeerExtension
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: MultiplayerPeer < PacketPeer < RefCounted < Object

Class that can be inherited to implement custom multiplayer API networking layers via GDExtension.

This class is designed to be inherited from a GDExtension plugin to implement custom networking layers for the multiplayer API (such as WebRTC). All the methods below must be implemented to have a working custom multiplayer implementation. See also MultiplayerAPI.

_close() virtual required

_disconnect_peer(p_peer: int, p_force: bool) virtual required

_get_available_packet_count() virtual required const

_get_connection_status() virtual required const

_get_max_packet_size() virtual required const

_get_packet(r_buffer: const uint8_t **, r_buffer_size: int32_t*) virtual

_get_packet_channel() virtual required const

_get_packet_mode() virtual required const

_get_packet_peer() virtual required const

_get_packet_script() virtual

_get_transfer_channel() virtual required const

_get_transfer_mode() virtual required const

_get_unique_id() virtual required const

_is_refusing_new_connections() virtual const

_is_server() virtual required const

_is_server_relay_supported() virtual const

_poll() virtual required

_put_packet(p_buffer: const uint8_t*, p_buffer_size: int) virtual

_put_packet_script(p_buffer: PackedByteArray) virtual

_set_refuse_new_connections(p_enable: bool) virtual

_set_target_peer(p_peer: int) virtual required

_set_transfer_channel(p_channel: int) virtual required

_set_transfer_mode(p_mode: TransferMode) virtual required

void _close() virtual required 

Called when the multiplayer peer should be immediately closed (see MultiplayerPeer.close()).

void _disconnect_peer(p_peer: int, p_force: bool) virtual required 

Called when the connected p_peer should be forcibly disconnected (see MultiplayerPeer.disconnect_peer()).

int _get_available_packet_count() virtual required const 

Called when the available packet count is internally requested by the MultiplayerAPI.

ConnectionStatus _get_connection_status() virtual required const 

Called when the connection status is requested on the MultiplayerPeer (see MultiplayerPeer.get_connection_status()).

int _get_max_packet_size() virtual required const 

Called when the maximum allowed packet size (in bytes) is requested by the MultiplayerAPI.

Error _get_packet(r_buffer: const uint8_t **, r_buffer_size: int32_t*) virtual 

Called when a packet needs to be received by the MultiplayerAPI, with r_buffer_size being the size of the binary r_buffer in bytes.

int _get_packet_channel() virtual required const 

Called to get the channel over which the next available packet was received. See MultiplayerPeer.get_packet_channel().

TransferMode _get_packet_mode() virtual required const 

Called to get the transfer mode the remote peer used to send the next available packet. See MultiplayerPeer.get_packet_mode().

int _get_packet_peer() virtual required const 

Called when the ID of the MultiplayerPeer who sent the most recent packet is requested (see MultiplayerPeer.get_packet_peer()).

PackedByteArray _get_packet_script() virtual 

Called when a packet needs to be received by the MultiplayerAPI, if _get_packet() isn't implemented. Use this when extending this class via GDScript.

int _get_transfer_channel() virtual required const 

Called when the transfer channel to use is read on this MultiplayerPeer (see MultiplayerPeer.transfer_channel).

TransferMode _get_transfer_mode() virtual required const 

Called when the transfer mode to use is read on this MultiplayerPeer (see MultiplayerPeer.transfer_mode).

int _get_unique_id() virtual required const 

Called when the unique ID of this MultiplayerPeer is requested (see MultiplayerPeer.get_unique_id()). The value must be between 1 and 2147483647.

bool _is_refusing_new_connections() virtual const 

Called when the "refuse new connections" status is requested on this MultiplayerPeer (see MultiplayerPeer.refuse_new_connections).

bool _is_server() virtual required const 

Called when the "is server" status is requested on the MultiplayerAPI. See MultiplayerAPI.is_server().

bool _is_server_relay_supported() virtual const 

Called to check if the server can act as a relay in the current configuration. See MultiplayerPeer.is_server_relay_supported().

void _poll() virtual required 

Called when the MultiplayerAPI is polled. See MultiplayerAPI.poll().

Error _put_packet(p_buffer: const uint8_t*, p_buffer_size: int) virtual 

Called when a packet needs to be sent by the MultiplayerAPI, with p_buffer_size being the size of the binary p_buffer in bytes.

Error _put_packet_script(p_buffer: PackedByteArray) virtual 

Called when a packet needs to be sent by the MultiplayerAPI, if _put_packet() isn't implemented. Use this when extending this class via GDScript.

void _set_refuse_new_connections(p_enable: bool) virtual 

Called when the "refuse new connections" status is set on this MultiplayerPeer (see MultiplayerPeer.refuse_new_connections).

void _set_target_peer(p_peer: int) virtual required 

Called when the target peer to use is set for this MultiplayerPeer (see MultiplayerPeer.set_target_peer()).

void _set_transfer_channel(p_channel: int) virtual required 

Called when the channel to use is set for this MultiplayerPeer (see MultiplayerPeer.transfer_channel).

void _set_transfer_mode(p_mode: TransferMode) virtual required 

Called when the transfer mode is set on this MultiplayerPeer (see MultiplayerPeer.transfer_mode).

Please read the User-contributed notes policy before submitting a comment.

---

## MultiplayerPeer

**URL:** https://docs.godotengine.org/en/stable/classes/class_multiplayerpeer.html

**Contents:**
- MultiplayerPeer
- Description
- Tutorials
- Properties
- Methods
- Signals
- Enumerations
- Constants
- Property Descriptions
- Method Descriptions

Inherits: PacketPeer < RefCounted < Object

Inherited By: ENetMultiplayerPeer, MultiplayerPeerExtension, OfflineMultiplayerPeer, WebRTCMultiplayerPeer, WebSocketMultiplayerPeer

Abstract class for specialized PacketPeers used by the MultiplayerAPI.

Manages the connection with one or more remote peers acting as server or client and assigning unique IDs to each of them. See also MultiplayerAPI.

Note: The MultiplayerAPI protocol is an implementation detail and isn't meant to be used by non-Godot servers. It may change without notice.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

High-level multiplayer

refuse_new_connections

disconnect_peer(peer: int, force: bool = false)

generate_unique_id() const

get_connection_status() const

get_packet_channel() const

get_packet_mode() const

get_packet_peer() const

get_unique_id() const

is_server_relay_supported() const

set_target_peer(id: int)

peer_connected(id: int) 

Emitted when a remote peer connects.

peer_disconnected(id: int) 

Emitted when a remote peer has disconnected.

enum ConnectionStatus: 

ConnectionStatus CONNECTION_DISCONNECTED = 0

The MultiplayerPeer is disconnected.

ConnectionStatus CONNECTION_CONNECTING = 1

The MultiplayerPeer is currently connecting to a server.

ConnectionStatus CONNECTION_CONNECTED = 2

This MultiplayerPeer is connected.

TransferMode TRANSFER_MODE_UNRELIABLE = 0

Packets are not acknowledged, no resend attempts are made for lost packets. Packets may arrive in any order. Potentially faster than TRANSFER_MODE_UNRELIABLE_ORDERED. Use for non-critical data, and always consider whether the order matters.

TransferMode TRANSFER_MODE_UNRELIABLE_ORDERED = 1

Packets are not acknowledged, no resend attempts are made for lost packets. Packets are received in the order they were sent in. Potentially faster than TRANSFER_MODE_RELIABLE. Use for non-critical data or data that would be outdated if received late due to resend attempt(s) anyway, for example movement and positional data.

TransferMode TRANSFER_MODE_RELIABLE = 2

Packets must be received and resend attempts should be made until the packets are acknowledged. Packets must be received in the order they were sent in. Most reliable transfer mode, but potentially the slowest due to the overhead. Use for critical data that must be transmitted and arrive in order, for example an ability being triggered or a chat message. Consider carefully if the information really is critical, and use sparingly.

TARGET_PEER_BROADCAST = 0 

Packets are sent to all connected peers.

TARGET_PEER_SERVER = 1 

Packets are sent to the remote peer acting as server.

bool refuse_new_connections = false 

void set_refuse_new_connections(value: bool)

bool is_refusing_new_connections()

If true, this MultiplayerPeer refuses new connections.

int transfer_channel = 0 

void set_transfer_channel(value: int)

int get_transfer_channel()

The channel to use to send packets. Many network APIs such as ENet and WebRTC allow the creation of multiple independent channels which behaves, in a way, like separate connections. This means that reliable data will only block delivery of other packets on that channel, and ordering will only be in respect to the channel the packet is being sent on. Using different channels to send different and independent state updates is a common way to optimize network usage and decrease latency in fast-paced games.

Note: The default channel (0) actually works as 3 separate channels (one for each TransferMode) so that TRANSFER_MODE_RELIABLE and TRANSFER_MODE_UNRELIABLE_ORDERED does not interact with each other by default. Refer to the specific network API documentation (e.g. ENet or WebRTC) to learn how to set up channels correctly.

TransferMode transfer_mode = 2 

void set_transfer_mode(value: TransferMode)

TransferMode get_transfer_mode()

The manner in which to send packets to the target peer. See the set_target_peer() method.

Immediately close the multiplayer peer returning to the state CONNECTION_DISCONNECTED. Connected peers will be dropped without emitting peer_disconnected.

void disconnect_peer(peer: int, force: bool = false) 

Disconnects the given peer from this host. If force is true the peer_disconnected signal will not be emitted for this peer.

int generate_unique_id() const 

Returns a randomly generated integer that can be used as a network unique ID.

ConnectionStatus get_connection_status() const 

Returns the current state of the connection.

int get_packet_channel() const 

Returns the channel over which the next available packet was received. See PacketPeer.get_available_packet_count().

TransferMode get_packet_mode() const 

Returns the transfer mode the remote peer used to send the next available packet. See PacketPeer.get_available_packet_count().

int get_packet_peer() const 

Returns the ID of the MultiplayerPeer who sent the next available packet. See PacketPeer.get_available_packet_count().

int get_unique_id() const 

Returns the ID of this MultiplayerPeer.

bool is_server_relay_supported() const 

Returns true if the server can act as a relay in the current configuration. That is, if the higher level MultiplayerAPI should notify connected clients of other peers, and implement a relay protocol to allow communication between them.

Waits up to 1 second to receive a new network event.

void set_target_peer(id: int) 

Sets the peer to which packets will be sent.

The id can be one of: TARGET_PEER_BROADCAST to send to all connected peers, TARGET_PEER_SERVER to send to the peer acting as server, a valid peer ID to send to that specific peer, a negative peer ID to send to all peers except that one. By default, the target peer is TARGET_PEER_BROADCAST.

Please read the User-contributed notes policy before submitting a comment.

---

## MultiplayerSynchronizer

**URL:** https://docs.godotengine.org/en/stable/classes/class_multiplayersynchronizer.html

**Contents:**
- MultiplayerSynchronizer
- Description
- Properties
- Methods
- Signals
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: Node < Object

Synchronizes properties from the multiplayer authority to the remote peers.

By default, MultiplayerSynchronizer synchronizes configured properties to all peers.

Visibility can be handled directly with set_visibility_for() or as-needed with add_visibility_filter() and update_visibility().

MultiplayerSpawners will handle nodes according to visibility of synchronizers as long as the node at root_path was spawned by one.

Internally, MultiplayerSynchronizer uses MultiplayerAPI.object_configuration_add() to notify synchronization start passing the Node at root_path as the object and itself as the configuration, and uses MultiplayerAPI.object_configuration_remove() to notify synchronization end in a similar way.

Note: Synchronization is not supported for Object type properties, like Resource. Properties that are unique to each peer, like the instance IDs of Objects (see Object.get_instance_id()) or RIDs, will also not work in synchronization.

SceneReplicationConfig

visibility_update_mode

add_visibility_filter(filter: Callable)

get_visibility_for(peer: int) const

remove_visibility_filter(filter: Callable)

set_visibility_for(peer: int, visible: bool)

update_visibility(for_peer: int = 0)

delta_synchronized() 

Emitted when a new delta synchronization state is received by this synchronizer after the properties have been updated.

Emitted when a new synchronization state is received by this synchronizer after the properties have been updated.

visibility_changed(for_peer: int) 

Emitted when visibility of for_peer is updated. See update_visibility().

enum VisibilityUpdateMode: 

VisibilityUpdateMode VISIBILITY_PROCESS_IDLE = 0

Visibility filters are updated during process frames (see Node.NOTIFICATION_INTERNAL_PROCESS).

VisibilityUpdateMode VISIBILITY_PROCESS_PHYSICS = 1

Visibility filters are updated during physics frames (see Node.NOTIFICATION_INTERNAL_PHYSICS_PROCESS).

VisibilityUpdateMode VISIBILITY_PROCESS_NONE = 2

Visibility filters are not updated automatically, and must be updated manually by calling update_visibility().

float delta_interval = 0.0 

void set_delta_interval(value: float)

float get_delta_interval()

Time interval between delta synchronizations. Used when the replication is set to SceneReplicationConfig.REPLICATION_MODE_ON_CHANGE. If set to 0.0 (the default), delta synchronizations happen every network process frame.

bool public_visibility = true 

void set_visibility_public(value: bool)

bool is_visibility_public()

Whether synchronization should be visible to all peers by default. See set_visibility_for() and add_visibility_filter() for ways of configuring fine-grained visibility options.

SceneReplicationConfig replication_config 

void set_replication_config(value: SceneReplicationConfig)

SceneReplicationConfig get_replication_config()

Resource containing which properties to synchronize.

float replication_interval = 0.0 

void set_replication_interval(value: float)

float get_replication_interval()

Time interval between synchronizations. Used when the replication is set to SceneReplicationConfig.REPLICATION_MODE_ALWAYS. If set to 0.0 (the default), synchronizations happen every network process frame.

NodePath root_path = NodePath("..") 

void set_root_path(value: NodePath)

NodePath get_root_path()

Node path that replicated properties are relative to.

If root_path was spawned by a MultiplayerSpawner, the node will be also be spawned and despawned based on this synchronizer visibility options.

VisibilityUpdateMode visibility_update_mode = 0 

void set_visibility_update_mode(value: VisibilityUpdateMode)

VisibilityUpdateMode get_visibility_update_mode()

Specifies when visibility filters are updated.

void add_visibility_filter(filter: Callable) 

Adds a peer visibility filter for this synchronizer.

filter should take a peer ID int and return a bool.

bool get_visibility_for(peer: int) const 

Queries the current visibility for peer peer.

void remove_visibility_filter(filter: Callable) 

Removes a peer visibility filter from this synchronizer.

void set_visibility_for(peer: int, visible: bool) 

Sets the visibility of peer to visible. If peer is 0, the value of public_visibility will be updated instead.

void update_visibility(for_peer: int = 0) 

Updates the visibility of for_peer according to visibility filters. If for_peer is 0 (the default), all peers' visibilties are updated.

Please read the User-contributed notes policy before submitting a comment.

---

## Networking

**URL:** https://docs.godotengine.org/en/stable/tutorials/networking/index.html

**Contents:**
- Networking

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

---

## OfflineMultiplayerPeer

**URL:** https://docs.godotengine.org/en/stable/classes/class_offlinemultiplayerpeer.html

**Contents:**
- OfflineMultiplayerPeer
- Description
- User-contributed notes

Inherits: MultiplayerPeer < PacketPeer < RefCounted < Object

A MultiplayerPeer which is always connected and acts as a server.

This is the default MultiplayerAPI.multiplayer_peer for the Node.multiplayer. It mimics the behavior of a server with no peers connected.

This means that the SceneTree will act as the multiplayer authority by default. Calls to MultiplayerAPI.is_server() will return true, and calls to MultiplayerAPI.get_unique_id() will return MultiplayerPeer.TARGET_PEER_SERVER.

Please read the User-contributed notes policy before submitting a comment.

---

## PacketPeer

**URL:** https://docs.godotengine.org/en/stable/classes/class_packetpeer.html

**Contents:**
- PacketPeer
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: RefCounted < Object

Inherited By: ENetPacketPeer, MultiplayerPeer, PacketPeerDTLS, PacketPeerExtension, PacketPeerStream, PacketPeerUDP, WebRTCDataChannel, WebSocketPeer

Abstraction and base class for packet-based protocols.

PacketPeer is an abstraction and base class for packet-based protocols (such as UDP). It provides an API for sending and receiving packets both as raw data or variables. This makes it easy to transfer data over a protocol, without having to encode data as low-level bytes or having to worry about network ordering.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

encode_buffer_max_size

get_available_packet_count() const

get_packet_error() const

get_var(allow_objects: bool = false)

put_packet(buffer: PackedByteArray)

put_var(var: Variant, full_objects: bool = false)

int encode_buffer_max_size = 8388608 

void set_encode_buffer_max_size(value: int)

int get_encode_buffer_max_size()

Maximum buffer size allowed when encoding Variants. Raise this value to support heavier memory allocations.

The put_var() method allocates memory on the stack, and the buffer used will grow automatically to the closest power of two to match the size of the Variant. If the Variant is bigger than encode_buffer_max_size, the method will error out with @GlobalScope.ERR_OUT_OF_MEMORY.

int get_available_packet_count() const 

Returns the number of packets currently available in the ring-buffer.

PackedByteArray get_packet() 

Error get_packet_error() const 

Returns the error state of the last packet received (via get_packet() and get_var()).

Variant get_var(allow_objects: bool = false) 

Gets a Variant. If allow_objects is true, decoding objects is allowed.

Internally, this uses the same decoding mechanism as the @GlobalScope.bytes_to_var() method.

Warning: Deserialized objects can contain code which gets executed. Do not use this option if the serialized object comes from untrusted sources to avoid potential security threats such as remote code execution.

Error put_packet(buffer: PackedByteArray) 

Error put_var(var: Variant, full_objects: bool = false) 

Sends a Variant as a packet. If full_objects is true, encoding objects is allowed (and can potentially include code).

Internally, this uses the same encoding mechanism as the @GlobalScope.var_to_bytes() method.

Please read the User-contributed notes policy before submitting a comment.

---

## SceneMultiplayer

**URL:** https://docs.godotengine.org/en/stable/classes/class_scenemultiplayer.html

**Contents:**
- SceneMultiplayer
- Description
- Properties
- Methods
- Signals
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: MultiplayerAPI < RefCounted < Object

High-level multiplayer API implementation.

This class is the default implementation of MultiplayerAPI, used to provide multiplayer functionalities in Godot Engine.

This implementation supports RPCs via Node.rpc() and Node.rpc_id() and requires MultiplayerAPI.rpc() to be passed a Node (it will fail for other object types).

This implementation additionally provide SceneTree replication via the MultiplayerSpawner and MultiplayerSynchronizer nodes, and the SceneReplicationConfig resource.

Note: The high-level multiplayer API protocol is an implementation detail and isn't meant to be used by non-Godot servers. It may change without notice.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

allow_object_decoding

max_delta_packet_size

refuse_new_connections

complete_auth(id: int)

disconnect_peer(id: int)

get_authenticating_peers()

send_auth(id: int, data: PackedByteArray)

send_bytes(bytes: PackedByteArray, id: int = 0, mode: TransferMode = 2, channel: int = 0)

peer_authenticating(id: int) 

Emitted when this MultiplayerAPI's MultiplayerAPI.multiplayer_peer connects to a new peer and a valid auth_callback is set. In this case, the MultiplayerAPI.peer_connected will not be emitted until complete_auth() is called with given peer id. While in this state, the peer will not be included in the list returned by MultiplayerAPI.get_peers() (but in the one returned by get_authenticating_peers()), and only authentication data will be sent or received. See send_auth() for sending authentication data.

peer_authentication_failed(id: int) 

Emitted when this MultiplayerAPI's MultiplayerAPI.multiplayer_peer disconnects from a peer for which authentication had not yet completed. See peer_authenticating.

peer_packet(id: int, packet: PackedByteArray) 

Emitted when this MultiplayerAPI's MultiplayerAPI.multiplayer_peer receives a packet with custom data (see send_bytes()). ID is the peer ID of the peer that sent the packet.

bool allow_object_decoding = false 

void set_allow_object_decoding(value: bool)

bool is_object_decoding_allowed()

If true, the MultiplayerAPI will allow encoding and decoding of object during RPCs.

Warning: Deserialized objects can contain code which gets executed. Do not use this option if the serialized object comes from untrusted sources to avoid potential security threat such as remote code execution.

Callable auth_callback = Callable() 

void set_auth_callback(value: Callable)

Callable get_auth_callback()

The callback to execute when receiving authentication data sent via send_auth(). If the Callable is empty (default), peers will be automatically accepted as soon as they connect.

float auth_timeout = 3.0 

void set_auth_timeout(value: float)

float get_auth_timeout()

If set to a value greater than 0.0, the maximum duration in seconds peers can stay in the authenticating state, after which the authentication will automatically fail. See the peer_authenticating and peer_authentication_failed signals.

int max_delta_packet_size = 65535 

void set_max_delta_packet_size(value: int)

int get_max_delta_packet_size()

Maximum size of each delta packet. Higher values increase the chance of receiving full updates in a single frame, but also the chance of causing networking congestion (higher latency, disconnections). See MultiplayerSynchronizer.

int max_sync_packet_size = 1350 

void set_max_sync_packet_size(value: int)

int get_max_sync_packet_size()

Maximum size of each synchronization packet. Higher values increase the chance of receiving full updates in a single frame, but also the chance of packet loss. See MultiplayerSynchronizer.

bool refuse_new_connections = false 

void set_refuse_new_connections(value: bool)

bool is_refusing_new_connections()

If true, the MultiplayerAPI's MultiplayerAPI.multiplayer_peer refuses new incoming connections.

NodePath root_path = NodePath("") 

void set_root_path(value: NodePath)

NodePath get_root_path()

The root path to use for RPCs and replication. Instead of an absolute path, a relative path will be used to find the node upon which the RPC should be executed.

This effectively allows to have different branches of the scene tree to be managed by different MultiplayerAPI, allowing for example to run both client and server in the same scene.

bool server_relay = true 

void set_server_relay_enabled(value: bool)

bool is_server_relay_enabled()

Enable or disable the server feature that notifies clients of other peers' connection/disconnection, and relays messages between them. When this option is false, clients won't be automatically notified of other peers and won't be able to send them packets through the server.

Note: Changing this option while other peers are connected may lead to unexpected behaviors.

Note: Support for this feature may depend on the current MultiplayerPeer configuration. See MultiplayerPeer.is_server_relay_supported().

Clears the current SceneMultiplayer network state (you shouldn't call this unless you know what you are doing).

Error complete_auth(id: int) 

Mark the authentication step as completed for the remote peer identified by id. The MultiplayerAPI.peer_connected signal will be emitted for this peer once the remote side also completes the authentication. No further authentication messages are expected to be received from this peer.

If a peer disconnects before completing authentication, either due to a network issue, the auth_timeout expiring, or manually calling disconnect_peer(), the peer_authentication_failed signal will be emitted instead of MultiplayerAPI.peer_disconnected.

void disconnect_peer(id: int) 

Disconnects the peer identified by id, removing it from the list of connected peers, and closing the underlying connection with it.

PackedInt32Array get_authenticating_peers() 

Returns the IDs of the peers currently trying to authenticate with this MultiplayerAPI.

Error send_auth(id: int, data: PackedByteArray) 

Sends the specified data to the remote peer identified by id as part of an authentication message. This can be used to authenticate peers, and control when MultiplayerAPI.peer_connected is emitted (and the remote peer accepted as one of the connected peers).

Error send_bytes(bytes: PackedByteArray, id: int = 0, mode: TransferMode = 2, channel: int = 0) 

Sends the given raw bytes to a specific peer identified by id (see MultiplayerPeer.set_target_peer()). Default ID is 0, i.e. broadcast to all peers.

Please read the User-contributed notes policy before submitting a comment.

---

## SceneTreeTimer

**URL:** https://docs.godotengine.org/en/stable/classes/class_scenetreetimer.html

**Contents:**
- SceneTreeTimer
- Description
- Properties
- Signals
- Property Descriptions
- User-contributed notes

Inherits: RefCounted < Object

A one-shot timer managed by the scene tree, which emits timeout on completion. See also SceneTree.create_timer().

As opposed to Timer, it does not require the instantiation of a node. Commonly used to create a one-shot delay timer as in the following example:

The timer will be dereferenced after its time elapses. To preserve the timer, you can keep a reference to it. See RefCounted.

Note: The timer is processed after all of the nodes in the current frame, i.e. node's Node._process() method would be called before the timer (or Node._physics_process() if process_in_physics in SceneTree.create_timer() has been set to true).

Emitted when the timer reaches 0.

void set_time_left(value: float)

float get_time_left()

The time remaining (in seconds).

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (swift):
```swift
func some_function():
    print("Timer started.")
    await get_tree().create_timer(1.0).timeout
    print("Timer ended.")
```

Example 2 (swift):
```swift
public async Task SomeFunction()
{
    GD.Print("Timer started.");
    await ToSignal(GetTree().CreateTimer(1.0f), SceneTreeTimer.SignalName.Timeout);
    GD.Print("Timer ended.");
}
```

---

## TLS/SSL certificates

**URL:** https://docs.godotengine.org/en/stable/tutorials/networking/ssl_certificates.html

**Contents:**
- TLS/SSL certificates
- Introduction
- Obtain a certificate from a certificate authority
- Generate a self-signed certificate
- User-contributed notes

It is often desired to use TLS connections (also known as SSL connections) for communications to avoid "man in the middle" attacks. Godot has a connection wrapper, StreamPeerTLS, which can take a regular connection and add security around it. The HTTPClient and HTTPRequest classes also support HTTPS using this same wrapper.

Godot will try to use the TLS certificate bundle provided by the operating system, but also includes the TLS certificate bundle from Mozilla as a fallback.

You can alternatively force your own certificate bundle in the Project Settings:

Setting the TLS certificate bundle override project setting

When set, this file overrides the operating system provided bundle by default. This file should contain any number of public certificates in PEM format.

There are two ways to obtain certificates:

The main approach to getting a certificate is to use a certificate authority (CA) such as Let's Encrypt. This is a more cumbersome process than a self-signed certificate, but it's more "official" and ensures your identity is clearly represented. The resulting certificate is also trusted by applications such as web browsers, unlike a self-signed certificate which requires additional configuration on the client side before it's considered trusted.

These certificates do not require any configuration on the client to work, since Godot already bundles the Mozilla certificate bundle in the editor and exported projects.

For most use cases, it's recommended to go through certificate authority as the process is free with certificate authorities such as Let's Encrypt. However, if using a certificate authority is not an option, then you can generate a self-signed certificate and tell the client to consider your self-signed certificate as trusted.

To create a self-signed certificate, generate a private and public key pair and add the public key (in PEM format) to the CRT file specified in the Project Settings.

The private key should only go to your server. The client must not have access to it: otherwise, the security of the certificate will be compromised.

When specifying a self-signed certificate as TLS bundle in the project settings, normal domain name validation is enforced via the certificate CN and alternative names. See TLSOptions to customize domain name validation.

For development purposes Godot can generate self-signed certificates via Crypto.generate_self_signed_certificate.

Alternatively, OpenSSL has some documentation about generating keys and certificates.

Please read the User-contributed notes policy before submitting a comment.

---

## Using WebSockets

**URL:** https://docs.godotengine.org/en/stable/tutorials/networking/websocket.html

**Contents:**
- Using WebSockets
- HTML5 and WebSocket
- Using WebSocket in Godot
  - Minimal client example
  - Minimal server example
  - Advanced chat demo
- User-contributed notes

The WebSocket protocol was standardized in 2011 with the original goal of allowing browsers to create stable and bidirectional connections with a server. Before that, browsers used to only support HTTP requests, which aren't well-suited for bidirectional communication.

The protocol is message-based and a very powerful tool to send push notifications to browsers. It has been used to implement chats, turn-based games, and more. It still uses a TCP connection, which is good for reliability but not for latency, so it's not good for real-time applications like VoIP and fast-paced games (see WebRTC for those use cases).

Due to its simplicity, its wide compatibility, and being easier to use than a raw TCP connection, WebSocket started to spread outside the browsers, in native applications as a mean to communicate with network servers.

Godot supports WebSocket in both native and web exports.

WebSocket is implemented in Godot via WebSocketPeer. The WebSocket implementation is compatible with the High-Level Multiplayer. See section on high-level multiplayer for more details.

When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

This example will show you how to create a WebSocket connection to a remote server, and how to send and receive data.

This will print something similar to:

This example will show you how to create a WebSocket server that listens for remote connections, and how to send and receive data.

When a client connects, this will print something similar to this:

A more advanced chat demo which optionally uses the multiplayer mid-level abstraction and a high-level multiplayer demo are available in the godot demo projects under networking/websocket_chat and networking/websocket_multiplayer.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node

# The URL we will connect to.
# Use "ws://localhost:9080" if testing with the minimal server example below.
# `wss://` is used for secure connections,
# while `ws://` is used for plain text (insecure) connections.
@export var websocket_url = "wss://echo.websocket.org"

# Our WebSocketClient instance.
var socket = WebSocketPeer.new()


func _ready():
    # Initiate connection to the given URL.
    var err = socket.connect_to_url(websocket_url)
    if err == OK:
        print("Connecting to %s..." % websocket_url)
        # Wait for the socket to connect.
        await get_tree().create_timer(2).timeout

        # Send data.
        print("> Sending test packet.")
        socket.send_text("Test packet")
    else:
        push_error("Unable to connect.")
        set_process(false)


func _process(_delta):
    # Call this in `_process()` or `_physics_process()`.
    # Data transfer and state updates will only happen when calling this function.
    socket.poll()

    # get_ready_state() tells you what state the socket is in.
    var state = socket.get_ready_state()

    # `WebSocketPeer.STATE_OPEN` means the socket is connected and ready
    # to send and receive data.
    if state == WebSocketPeer.STATE_OPEN:
        while socket.get_available_packet_count():
            var packet = socket.get_packet()
            if socket.was_string_packet():
                var packet_text = packet.get_string_from_utf8()
                print("< Got text data from server: %s" % packet_text)
            else:
                print("< Got binary data from server: %d bytes" % packet.size())

    # `WebSocketPeer.STATE_CLOSING` means the socket is closing.
    # It is important to keep polling for a clean close.
    elif state == WebSocketPeer.STATE_CLOSING:
        pass

    # `WebSocketPeer.STATE_CLOSED` means the connection has fully closed.
    # It is now safe to stop polling.
    elif state == WebSocketPeer.STATE_CLOSED:
        # The code will be `-1` if the disconnection was not properly notified by the remote peer.
        var code = socket.get_close_code()
        print("WebSocket closed with code: %d. Clean: %s" % [code, code != -1])
        set_process(false) # Stop processing.
```

Example 2 (sql):
```sql
Connecting to wss://echo.websocket.org...
< Got text data from server: Request served by 7811941c69e658
> Sending test packet.
< Got text data from server: Test packet
```

Example 3 (gdscript):
```gdscript
extends Node

# The port we will listen to.
const PORT = 9080

# Our TCP Server instance.
var _tcp_server = TCPServer.new()

# Our connected peers list.
var _peers: Dictionary[int, WebSocketPeer] = {}

var last_peer_id := 1


func _ready():
    # Start listening on the given port.
    var err = _tcp_server.listen(PORT)
    if err == OK:
        print("Server started.")
    else:
        push_error("Unable to start server.")
        set_process(false)


func _process(_delta):
    while _tcp_server.is_connection_available():
        last_peer_id += 1
        print("+ Peer %d connected." % last_peer_id)
        var ws = WebSocketPeer.new()
        ws.accept_stream(_tcp_server.take_connection())
        _peers[last_peer_id] = ws

    # Iterate over all connected peers using "keys()" so we can erase in the loop
    for peer_id in _peers.keys():
        var peer = _peers[peer_id]

        peer.poll()

        var peer_state = peer.get_ready_state()
        if peer_state == WebSocketPeer.STATE_OPEN:
            while peer.get_available_packet_count():
                var packet = peer.get_packet()
                if peer.was_string_packet():
                    var packet_text = packet.get_string_from_utf8()
                    print("< Got text data from peer %d: %s ... echoing" % [peer_id, packet_text])
                    # Echo the packet back.
                    peer.send_text(packet_text)
                else:
                    print("< Got binary data from peer %d: %d ... echoing" % [peer_id, packet.size()])
                    # Echo the packet back.
                    peer.send(packet)
        elif peer_state == WebSocketPeer.STATE_CLOSED:
            # Remove the disconnected peer.
            _peers.erase(peer_id)
            var code = peer.get_close_code()
            var reason = peer.get_close_reason()
            print("- Peer %s closed with code: %d, reason %s. Clean: %s" % [peer_id, code, reason, code != -1])
```

Example 4 (sql):
```sql
Server started.
+ Peer 2 connected.
< Got text data from peer 2: Test packet ... echoing
```

---

## WebRTCMultiplayerPeer

**URL:** https://docs.godotengine.org/en/stable/classes/class_webrtcmultiplayerpeer.html

**Contents:**
- WebRTCMultiplayerPeer
- Description
- Methods
- Method Descriptions
- User-contributed notes

Inherits: MultiplayerPeer < PacketPeer < RefCounted < Object

A simple interface to create a peer-to-peer mesh network composed of WebRTCPeerConnection that is compatible with the MultiplayerAPI.

This class constructs a full mesh of WebRTCPeerConnection (one connection for each peer) that can be used as a MultiplayerAPI.multiplayer_peer.

You can add each WebRTCPeerConnection via add_peer() or remove them via remove_peer(). Peers must be added in WebRTCPeerConnection.STATE_NEW state to allow it to create the appropriate channels. This class will not create offers nor set descriptions, it will only poll them, and notify connections and disconnections.

When creating the peer via create_client() or create_server() the MultiplayerPeer.is_server_relay_supported() method will return true enabling peer exchange and packet relaying when supported by the MultiplayerAPI implementation.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

add_peer(peer: WebRTCPeerConnection, peer_id: int, unreliable_lifetime: int = 1)

create_client(peer_id: int, channels_config: Array = [])

create_mesh(peer_id: int, channels_config: Array = [])

create_server(channels_config: Array = [])

get_peer(peer_id: int)

has_peer(peer_id: int)

remove_peer(peer_id: int)

Error add_peer(peer: WebRTCPeerConnection, peer_id: int, unreliable_lifetime: int = 1) 

Add a new peer to the mesh with the given peer_id. The WebRTCPeerConnection must be in state WebRTCPeerConnection.STATE_NEW.

Three channels will be created for reliable, unreliable, and ordered transport. The value of unreliable_lifetime will be passed to the "maxPacketLifetime" option when creating unreliable and ordered channels (see WebRTCPeerConnection.create_data_channel()).

Error create_client(peer_id: int, channels_config: Array = []) 

Initialize the multiplayer peer as a client with the given peer_id (must be between 2 and 2147483647). In this mode, you should only call add_peer() once and with peer_id of 1. This mode enables MultiplayerPeer.is_server_relay_supported(), allowing the upper MultiplayerAPI layer to perform peer exchange and packet relaying.

You can optionally specify a channels_config array of TransferMode which will be used to create extra channels (WebRTC only supports one transfer mode per channel).

Error create_mesh(peer_id: int, channels_config: Array = []) 

Initialize the multiplayer peer as a mesh (i.e. all peers connect to each other) with the given peer_id (must be between 1 and 2147483647).

Error create_server(channels_config: Array = []) 

Initialize the multiplayer peer as a server (with unique ID of 1). This mode enables MultiplayerPeer.is_server_relay_supported(), allowing the upper MultiplayerAPI layer to perform peer exchange and packet relaying.

You can optionally specify a channels_config array of TransferMode which will be used to create extra channels (WebRTC only supports one transfer mode per channel).

Dictionary get_peer(peer_id: int) 

Returns a dictionary representation of the peer with given peer_id with three keys. "connection" containing the WebRTCPeerConnection to this peer, "channels" an array of three WebRTCDataChannel, and "connected" a boolean representing if the peer connection is currently connected (all three channels are open).

Dictionary get_peers() 

Returns a dictionary which keys are the peer ids and values the peer representation as in get_peer().

bool has_peer(peer_id: int) 

Returns true if the given peer_id is in the peers map (it might not be connected though).

void remove_peer(peer_id: int) 

Remove the peer with given peer_id from the mesh. If the peer was connected, and MultiplayerPeer.peer_connected was emitted for it, then MultiplayerPeer.peer_disconnected will be emitted.

Please read the User-contributed notes policy before submitting a comment.

---

## WebRTC

**URL:** https://docs.godotengine.org/en/stable/tutorials/networking/webrtc.html

**Contents:**
- WebRTC
- HTML5, WebSocket, WebRTC
  - WebSocket
  - WebRTC
- Using WebRTC in Godot
  - Minimal connection example
  - Local signaling example
  - Remote signaling with WebSocket
- User-contributed notes

The content of this page was not yet updated for Godot 4.5 and may be outdated. If you know how to improve this page or you can confirm that it's up to date, feel free to open a pull request.

One of Godot's great features is its ability to export to the HTML5/WebAssembly platform, allowing your game to run directly in the browser when a user visit your webpage.

This is a great opportunity for both demos and full games, but used to come with some limitations. In the area of networking, browsers used to support only HTTPRequests until recently, when first WebSocket and then WebRTC were proposed as standards.

When the WebSocket protocol was standardized in December 2011, it allowed browsers to create stable and bidirectional connections to a WebSocket server. The protocol is a very powerful tool to send push notifications to browsers, and has been used to implement chats, turn-based games, etc.

WebSockets, though, still use a TCP connection, which is good for reliability but not for latency, so not good for real-time applications like VoIP and fast-paced games.

For this reason, since 2010, Google started working on a new technology called WebRTC, which later on, in 2017, became a W3C candidate recommendation. WebRTC is a much more complex set of specifications, and relies on many other technologies behind the scenes (ICE, DTLS, SDP) to provide fast, real-time, and secure communication between two peers.

The idea is to find the fastest route between the two peers and establish whenever possible a direct communication (i.e. try to avoid a relaying server).

However, this comes at a price, which is that some media information must be exchanged between the two peers before the communication can start (in the form of Session Description Protocol - SDP strings). This usually takes the form of a so-called WebRTC Signaling Server.

Peers connect to a signaling server (for example a WebSocket server) and send their media information. The server then relays this information to other peers, allowing them to establish the desired direct communication. Once this step is done, peers can disconnect from the signaling server and keep the direct Peer-to-Peer (P2P) connection open.

WebRTC is implemented in Godot via two main classes WebRTCPeerConnection and WebRTCDataChannel, plus the multiplayer API implementation WebRTCMultiplayerPeer. See section on high-level multiplayer for more details.

These classes are available automatically in HTML5, but require an external GDExtension plugin on native (non-HTML5) platforms. Check out the webrtc-native plugin repository for instructions and to get the latest release.

When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

This example will show you how to create a WebRTC connection between two peers in the same application. This is not very useful in real life, but will give you a good overview of how a WebRTC connection is set up.

This example expands on the previous one, separating the peers in two different scenes, and using a singleton as a signaling server.

And now for the local signaling server:

This local signaling server is supposed to be used as a singleton to connect two peers in the same scene.

Then you can use it like this:

This will print something similar to this:

A more advanced demo using WebSocket for signaling peers and WebRTCMultiplayerPeer is available in the godot demo projects under networking/webrtc_signaling.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node

# Create the two peers
var p1 = WebRTCPeerConnection.new()
var p2 = WebRTCPeerConnection.new()
# And a negotiated channel for each each peer
var ch1 = p1.create_data_channel("chat", {"id": 1, "negotiated": true})
var ch2 = p2.create_data_channel("chat", {"id": 1, "negotiated": true})

func _ready():
    # Connect P1 session created to itself to set local description.
    p1.session_description_created.connect(p1.set_local_description)
    # Connect P1 session and ICE created to p2 set remote description and candidates.
    p1.session_description_created.connect(p2.set_remote_description)
    p1.ice_candidate_created.connect(p2.add_ice_candidate)

    # Same for P2
    p2.session_description_created.connect(p2.set_local_description)
    p2.session_description_created.connect(p1.set_remote_description)
    p2.ice_candidate_created.connect(p1.add_ice_candidate)

    # Let P1 create the offer
    p1.create_offer()

    # Wait a second and send message from P1.
    await get_tree().create_timer(1).timeout
    ch1.put_packet("Hi from P1".to_utf8_buffer())

    # Wait a second and send message from P2.
    await get_tree().create_timer(1).timeout
    ch2.put_packet("Hi from P2".to_utf8_buffer())

func _process(_delta):
    # Poll connections
    p1.poll()
    p2.poll()

    # Check for messages
    if ch1.get_ready_state() == ch1.STATE_OPEN and ch1.get_available_packet_count() > 0:
        print("P1 received: ", ch1.get_packet().get_string_from_utf8())
    if ch2.get_ready_state() == ch2.STATE_OPEN and ch2.get_available_packet_count() > 0:
        print("P2 received: ", ch2.get_packet().get_string_from_utf8())
```

Example 2 (sql):
```sql
P1 received: Hi from P1
P2 received: Hi from P2
```

Example 3 (gdscript):
```gdscript
extends Node
# An example p2p chat client.

var peer = WebRTCPeerConnection.new()

# Create negotiated data channel.
var channel = peer.create_data_channel("chat", {"negotiated": true, "id": 1})

func _ready():
    # Connect all functions.
    peer.ice_candidate_created.connect(self._on_ice_candidate)
    peer.session_description_created.connect(self._on_session)

    # Register to the local signaling server (see below for the implementation).
    Signaling.register(String(get_path()))


func _on_ice_candidate(mid, index, sdp):
    # Send the ICE candidate to the other peer via signaling server.
    Signaling.send_candidate(String(get_path()), mid, index, sdp)


func _on_session(type, sdp):
    # Send the session to other peer via signaling server.
    Signaling.send_session(String(get_path()), type, sdp)
    # Set generated description as local.
    peer.set_local_description(type, sdp)


func _process(delta):
    # Always poll the connection frequently.
    peer.poll()
    if channel.get_ready_state() == WebRTCDataChannel.STATE_OPEN:
        while channel.get_available_packet_count() > 0:
            print(String(get_path()), " received: ", channel.get_packet().get_string_from_utf8())


func send_message(message):
    channel.put_packet(message.to_utf8_buffer())
```

Example 4 (gdscript):
```gdscript
# A local signaling server. Add this to autoloads with name "Signaling" (/root/Signaling)
extends Node

# We will store the two peers here
var peers = []

func register(path):
    assert(peers.size() < 2)
    peers.append(path)
    if peers.size() == 2:
        get_node(peers[0]).peer.create_offer()


func _find_other(path):
    # Find the other registered peer.
    for p in peers:
        if p != path:
            return p
    return ""


func send_session(path, type, sdp):
    var other = _find_other(path)
    assert(other != "")
    get_node(other).peer.set_remote_description(type, sdp)


func send_candidate(path, mid, index, sdp):
    var other = _find_other(path)
    assert(other != "")
    get_node(other).peer.add_ice_candidate(mid, index, sdp)
```

---

## WebSocketMultiplayerPeer

**URL:** https://docs.godotengine.org/en/stable/classes/class_websocketmultiplayerpeer.html

**Contents:**
- WebSocketMultiplayerPeer
- Description
- Properties
- Methods
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: MultiplayerPeer < PacketPeer < RefCounted < Object

Base class for WebSocket server and client.

Base class for WebSocket server and client, allowing them to be used as multiplayer peer for the MultiplayerAPI.

Note: When exporting to Android, make sure to enable the INTERNET permission in the Android export preset before exporting the project or using one-click deploy. Otherwise, network communication of any kind will be blocked by Android.

create_client(url: String, tls_client_options: TLSOptions = null)

create_server(port: int, bind_address: String = "*", tls_server_options: TLSOptions = null)

get_peer(peer_id: int) const

get_peer_address(id: int) const

get_peer_port(id: int) const

PackedStringArray handshake_headers = PackedStringArray() 

void set_handshake_headers(value: PackedStringArray)

PackedStringArray get_handshake_headers()

The extra headers to use during handshake. See WebSocketPeer.handshake_headers for more details.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedStringArray for more details.

float handshake_timeout = 3.0 

void set_handshake_timeout(value: float)

float get_handshake_timeout()

The maximum time each peer can stay in a connecting state before being dropped.

int inbound_buffer_size = 65535 

void set_inbound_buffer_size(value: int)

int get_inbound_buffer_size()

The inbound buffer size for connected peers. See WebSocketPeer.inbound_buffer_size for more details.

int max_queued_packets = 4096 

void set_max_queued_packets(value: int)

int get_max_queued_packets()

The maximum number of queued packets for connected peers. See WebSocketPeer.max_queued_packets for more details.

int outbound_buffer_size = 65535 

void set_outbound_buffer_size(value: int)

int get_outbound_buffer_size()

The outbound buffer size for connected peers. See WebSocketPeer.outbound_buffer_size for more details.

PackedStringArray supported_protocols = PackedStringArray() 

void set_supported_protocols(value: PackedStringArray)

PackedStringArray get_supported_protocols()

The supported WebSocket sub-protocols. See WebSocketPeer.supported_protocols for more details.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedStringArray for more details.

Error create_client(url: String, tls_client_options: TLSOptions = null) 

Starts a new multiplayer client connecting to the given url. TLS certificates will be verified against the hostname when connecting using the wss:// protocol. You can pass the optional tls_client_options parameter to customize the trusted certification authorities, or disable the common name verification. See TLSOptions.client() and TLSOptions.client_unsafe().

Note: It is recommended to specify the scheme part of the URL, i.e. the url should start with either ws:// or wss://.

Error create_server(port: int, bind_address: String = "*", tls_server_options: TLSOptions = null) 

Starts a new multiplayer server listening on the given port. You can optionally specify a bind_address, and provide valid tls_server_options to use TLS. See TLSOptions.server().

WebSocketPeer get_peer(peer_id: int) const 

Returns the WebSocketPeer associated to the given peer_id.

String get_peer_address(id: int) const 

Returns the IP address of the given peer.

int get_peer_port(id: int) const 

Returns the remote port of the given peer.

Please read the User-contributed notes policy before submitting a comment.

---

## WebSocketPeer

**URL:** https://docs.godotengine.org/en/stable/classes/class_websocketpeer.html

**Contents:**
- WebSocketPeer
- Description
- Properties
- Methods
- Enumerations
- Property Descriptions
- Method Descriptions
- User-contributed notes

Inherits: PacketPeer < RefCounted < Object

A WebSocket connection.

This class represents WebSocket connection, and can be used as a WebSocket client (RFC 6455-compliant) or as a remote peer of a WebSocket server.

You can send WebSocket binary frames using PacketPeer.put_packet(), and WebSocket text frames using send() (prefer text frames when interacting with text-based API). You can check the frame type of the last packet via was_string_packet().

To start a WebSocket client, first call connect_to_url(), then regularly call poll() (e.g. during Node process). You can query the socket state via get_ready_state(), get the number of pending packets using PacketPeer.get_available_packet_count(), and retrieve them via PacketPeer.get_packet().

To use the peer as part of a WebSocket server refer to accept_stream() and the online tutorial.

accept_stream(stream: StreamPeer)

close(code: int = 1000, reason: String = "")

connect_to_url(url: String, tls_client_options: TLSOptions = null)

get_close_code() const

get_close_reason() const

get_connected_host() const

get_connected_port() const

get_current_outbound_buffered_amount() const

get_ready_state() const

get_requested_url() const

get_selected_protocol() const

send(message: PackedByteArray, write_mode: WriteMode = 1)

send_text(message: String)

set_no_delay(enabled: bool)

was_string_packet() const

WriteMode WRITE_MODE_TEXT = 0

Specifies that WebSockets messages should be transferred as text payload (only valid UTF-8 is allowed).

WriteMode WRITE_MODE_BINARY = 1

Specifies that WebSockets messages should be transferred as binary payload (any byte combination is allowed).

State STATE_CONNECTING = 0

Socket has been created. The connection is not yet open.

The connection is open and ready to communicate.

State STATE_CLOSING = 2

The connection is in the process of closing. This means a close request has been sent to the remote peer but confirmation has not been received.

State STATE_CLOSED = 3

The connection is closed or couldn't be opened.

PackedStringArray handshake_headers = PackedStringArray() 

void set_handshake_headers(value: PackedStringArray)

PackedStringArray get_handshake_headers()

The extra HTTP headers to be sent during the WebSocket handshake.

Note: Not supported in Web exports due to browsers' restrictions.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedStringArray for more details.

float heartbeat_interval = 0.0 

void set_heartbeat_interval(value: float)

float get_heartbeat_interval()

The interval (in seconds) at which the peer will automatically send WebSocket "ping" control frames. When set to 0, no "ping" control frames will be sent.

Note: Has no effect in Web exports due to browser restrictions.

int inbound_buffer_size = 65535 

void set_inbound_buffer_size(value: int)

int get_inbound_buffer_size()

The size of the input buffer in bytes (roughly the maximum amount of memory that will be allocated for the inbound packets).

int max_queued_packets = 4096 

void set_max_queued_packets(value: int)

int get_max_queued_packets()

The maximum amount of packets that will be allowed in the queues (both inbound and outbound).

int outbound_buffer_size = 65535 

void set_outbound_buffer_size(value: int)

int get_outbound_buffer_size()

The size of the input buffer in bytes (roughly the maximum amount of memory that will be allocated for the outbound packets).

PackedStringArray supported_protocols = PackedStringArray() 

void set_supported_protocols(value: PackedStringArray)

PackedStringArray get_supported_protocols()

The WebSocket sub-protocols allowed during the WebSocket handshake.

Note: The returned array is copied and any changes to it will not update the original property value. See PackedStringArray for more details.

Error accept_stream(stream: StreamPeer) 

Accepts a peer connection performing the HTTP handshake as a WebSocket server. The stream must be a valid TCP stream retrieved via TCPServer.take_connection(), or a TLS stream accepted via StreamPeerTLS.accept_stream().

Note: Not supported in Web exports due to browsers' restrictions.

void close(code: int = 1000, reason: String = "") 

Closes this WebSocket connection. code is the status code for the closure (see RFC 6455 section 7.4 for a list of valid status codes). reason is the human readable reason for closing the connection (can be any UTF-8 string that's smaller than 123 bytes). If code is negative, the connection will be closed immediately without notifying the remote peer.

Note: To achieve a clean close, you will need to keep polling until STATE_CLOSED is reached.

Note: The Web export might not support all status codes. Please refer to browser-specific documentation for more details.

Error connect_to_url(url: String, tls_client_options: TLSOptions = null) 

Connects to the given URL. TLS certificates will be verified against the hostname when connecting using the wss:// protocol. You can pass the optional tls_client_options parameter to customize the trusted certification authorities, or disable the common name verification. See TLSOptions.client() and TLSOptions.client_unsafe().

Note: This method is non-blocking, and will return @GlobalScope.OK before the connection is established as long as the provided parameters are valid and the peer is not in an invalid state (e.g. already connected). Regularly call poll() (e.g. during Node process) and check the result of get_ready_state() to know whether the connection succeeds or fails.

Note: To avoid mixed content warnings or errors in Web, you may have to use a url that starts with wss:// (secure) instead of ws://. When doing so, make sure to use the fully qualified domain name that matches the one defined in the server's TLS certificate. Do not connect directly via the IP address for wss:// connections, as it won't match with the TLS certificate.

int get_close_code() const 

Returns the received WebSocket close frame status code, or -1 when the connection was not cleanly closed. Only call this method when get_ready_state() returns STATE_CLOSED.

String get_close_reason() const 

Returns the received WebSocket close frame status reason string. Only call this method when get_ready_state() returns STATE_CLOSED.

String get_connected_host() const 

Returns the IP address of the connected peer.

Note: Not available in the Web export.

int get_connected_port() const 

Returns the remote port of the connected peer.

Note: Not available in the Web export.

int get_current_outbound_buffered_amount() const 

Returns the current amount of data in the outbound websocket buffer. Note: Web exports use WebSocket.bufferedAmount, while other platforms use an internal buffer.

State get_ready_state() const 

Returns the ready state of the connection.

String get_requested_url() const 

Returns the URL requested by this peer. The URL is derived from the url passed to connect_to_url() or from the HTTP headers when acting as server (i.e. when using accept_stream()).

String get_selected_protocol() const 

Returns the selected WebSocket sub-protocol for this connection or an empty string if the sub-protocol has not been selected yet.

Updates the connection state and receive incoming packets. Call this function regularly to keep it in a clean state.

Error send(message: PackedByteArray, write_mode: WriteMode = 1) 

Sends the given message using the desired write_mode. When sending a String, prefer using send_text().

Error send_text(message: String) 

Sends the given message using WebSocket text mode. Prefer this method over PacketPeer.put_packet() when interacting with third-party text-based API (e.g. when using JSON formatted messages).

void set_no_delay(enabled: bool) 

Disable Nagle's algorithm on the underlying TCP socket (default). See StreamPeerTCP.set_no_delay() for more information.

Note: Not available in the Web export.

bool was_string_packet() const 

Returns true if the last received packet was sent as a text payload. See WriteMode.

Please read the User-contributed notes policy before submitting a comment.

**Examples:**

Example 1 (gdscript):
```gdscript
extends Node

var socket = WebSocketPeer.new()

func _ready():
    socket.connect_to_url("wss://example.com")

func _process(delta):
    socket.poll()
    var state = socket.get_ready_state()
    if state == WebSocketPeer.STATE_OPEN:
        while socket.get_available_packet_count():
            print("Packet: ", socket.get_packet())
    elif state == WebSocketPeer.STATE_CLOSING:
        # Keep polling to achieve proper close.
        pass
    elif state == WebSocketPeer.STATE_CLOSED:
        var code = socket.get_close_code()
        var reason = socket.get_close_reason()
        print("WebSocket closed with code: %d, reason %s. Clean: %s" % [code, reason, code != -1])
        set_process(false) # Stop processing.
```

---
