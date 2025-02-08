# Protocol Layers in Networking: Organizing Complexity

Networks are complex due to multiple components like hosts, routers, links, applications, protocols, and hardware. To manage this complexity, we use a layered approach to structure network communications.

## Why Do We Use Layers?

1. **Simplifies Network Design**: Breaking the network into layers allows each layer to handle a specific function without worrying about the entire system.
2. **Standardization**: Different devices and systems from different vendors can work together because they follow common standards (e.g., TCP/IP model).
3. **Troubleshooting & Development**: If something breaks, we can fix a specific layer instead of the entire network.

## The Layered Approach: OSI & TCP/IP Models

There are two main models for structuring network communications:

1. **OSI (Open Source Interconnection) Model (7 Layers)**: Theoretical model used for understanding networking.
2. **TCP/IP Model (4 Layers)**: Practical model used on the internet today.

| OSI Model (7 Layers) | TCP/IP Model (4 Layers)   | Function                                           |
| -------------------- | ------------------------- | -------------------------------------------------- |
| 7. Application       | 4. Application            | User interaction (Web, Email, FTP)                 |
| 6. Presentation      | (Merged with Application) | Data formatting (encryption, compression)          |
| 5. Session           | (Merged with Application) | Connection management                              |
| 4. Transport         | 3. Transport              | End-to-end communication (TCP, UDP)                |
| 3. Network           | 2. Internet               | Routing & addressing (IP, ICMP)                    |
| 2. Data Link         | 1. Network Access         | MAC addressing & error detection (Ethernet, Wi-Fi) |
| 1. Physical          | 1. Network Access         | Transmission of raw bits (Cables, Wi-Fi signals)   |

-- Seven layers

- Lower three layers are peer-to-peer
- Next four layers are end-to-end

---

- ARP: A protocol that maps IP addresses to MAC addresses within a local network to facilitate data link layer communication.

- RARP: A protocol used to map MAC addresses to IP addresses, allowing devices that don't know their IP address to obtain it. It has been largely replaced by DHCP.

---

-- When a packet is too large to be transmitted over a network link due to MTU restrictions (e.g., Ethernet has an MTU of 1500 bytes), the Network Layer (specifically the IP layer) fragments the packet into smaller parts.
-- Each fragment is sent separately over the network and contains information such as:

- Identification: A unique identifier for the original packet, so fragments can be correctly reassembled at the destination.
- Fragment Offset: Tells the receiving system where this fragment fits into the original packet.
- More Fragment (MF) flag: Indicates whether there are more fragments of the same packet.

---

Application -> Transport -> Network -> Link

message -> segment -> datagram -> frame

M ----> H | M ----> H | H | M ----> H | H | H | M

where H is header and M is actual message : each layer adds its header to the packet

---

-- Illustrative Example:
Imagine you want to send an email from your computer (Device A) to another computer (Device B) over the internet.

- **Application Layer**: You compose the email, and the email is broken into smaller pieces (segments) by the Transport Layer.
- **Network Layer (IP)**: The Transport Layer hands the email segments to the Network Layer, which adds the IP header with the source (your IP) and destination (Device B's IP) addresses. This becomes a packet.
- **Data Link Layer (Ethernet)**: The packet is handed down to the Data Link Layer, which wraps it in a frame with MAC addresses (source MAC of your device and destination MAC of the router or Device B if it's in the same network).
- **Physical Layer**: The frame is converted into electrical signals (or optical signals, depending on the medium) and sent over the physical medium (e.g., Ethernet cables or Wi-Fi).
- **Routers**: If Device B is on a different network, the packet passes through several routers. Each router strips off the Data Link Layer information (MAC address), inspects the IP address, and forwards it to the next router or the destination.
- **Destination Device (Device B)**: When the packet reaches Device B’s network, the process is reversed, and Device B’s application reconstructs the email.

## Comparison with Other Devices

| Device | Works at Layer                           | Function                                                         |
| ------ | ---------------------------------------- | ---------------------------------------------------------------- |
| Hub    | Layer 1 (Physical)                       | Broadcasts data to all devices in a network                      |
| Switch | Layer 2 (Data Link)                      | Uses MAC addresses to forward data within a network              |
| Router | Layer 3 (Network)                        | Uses IP addresses to connect different networks and forward data |
| Modem  | Layer 1 (Physical) & Layer 2 (Data Link) | Converts digital↔analog signals, handles error detection         |
| Tap    | Layer 1 (Physical)                       | Splits coaxial cable signals to multiple users                   |

## How Data Moves Through Layers

When you send a message over a network (e.g., sending an email), the data moves down through each layer, gaining extra information (headers), then is sent over the network. The receiver’s network processes it in reverse (bottom to top).

1. **Application Layer**: You write an email.
2. **Transport Layer (TCP)**: Email is broken into packets.
3. **Network Layer (IP)**: Packets are assigned IP addresses.
4. **Data Link Layer (Ethernet/Wi-Fi)**: Packets are sent as frames.
5. **Physical Layer (Fiber, Copper, Wireless)**: Data is converted to signals.
6. **Receiver**: Data reaches the receiver and is rebuilt layer by layer.

---

Note: Sockets are used evertime either TCP or UDP sockets are used for connection internammly i.e. TCP sockets or UDP sockets.

- An IP address alone is not sufficient to identify a specific process on a host.
- In combination, the IP address and the port number form a unique identifier for a process on a specific host, often called a socket (IP address + port).

## RTP Vs UDP

### UDP (User Datagram Protocol):

**Type**: Transport protocol.

**Purpose**: Provides basic, connectionless, and fast data transmission.

**Features**:

- No packet ordering or synchronization.
- No error recovery or congestion control.

  **Use**: Suitable for applications where speed is crucial and occasional data loss is acceptable (e.g., web browsing, DNS).

### RTP (Real-time Transport Protocol):

**Type**: Application-layer protocol built on top of UDP.

**Purpose**: Specifically designed for real-time audio, video, and multimedia streaming.

**Features**:

- Adds packet sequencing and timestamping.
- Provides synchronization of media streams.
- Works with other protocols (like RTCP) for error monitoring and feedback.

  **Use**: Ideal for live streaming, video calls, VoIP, where timing and ordering of packets are essential.
