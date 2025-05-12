# Common Terminologies

### The Internet

The global network connecting devices.

### The WWW

A service running on the internet that provides web content.

| Feature        | World Wide Web (WWW)                                                            | Internet                                                                      |
| -------------- | ------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Definition     | A system of interlinked web pages and resources accessed via browsers.          | A global network of interconnected computers and servers.                     |
| Purpose        | Enables users to access and share web pages, images, videos, and other content. | Provides the infrastructure for communication, data transfer, and networking. |
| Components     | Web pages, hyperlinks, browsers, HTTP, HTML, URLs.                              | Routers, switches, servers, ISPs, protocols (TCP/IP).                         |
| Protocols Used | Uses HTTP/HTTPS for web browsing.                                               | Uses multiple protocols (TCP/IP, FTP, SMTP, DNS, etc.).                       |
| Dependency     | Depends on the internet to function.                                            | Can exist without the web (e.g., email, file sharing).                        |
| Example        | Browsing Facebook, YouTube, or Wikipedia.                                       | Sending an email, using WhatsApp, online gaming, video calls.                 |

### Connection-Oriented Service (Virtual Circuit)

**Definition:** A communication service where a connection is established between sender and receiver before any data is transferred, much like a telephone call.

**Protocol Example:** TCP (Transmission Control Protocol)

**Key Features:**

- A virtual circuit is established (logical path).
- Data arrives in order.
- Reliable: guarantees delivery, error checking, and flow control.
- Connection must be set up and closed explicitly.

**Analogy:** Like a phone call—you dial, connect, talk, and then hang up.

---

### Connectionless Service (Datagram)

**Definition:** A communication service where each message (datagram) is sent independently without establishing a connection.

**Protocol Example:** UDP (User Datagram Protocol)

**Key Features:**

- No setup phase (no connection).
- Each packet (datagram) is routed independently.
- Unreliable: packets may arrive out of order, be duplicated, or lost.
- Lower overhead and faster for simple tasks.

**Analogy:** Like sending postcards—each one is sent individually and may arrive out of order or not at all.

---

Note : Both VC and Datagram are similar to TCP/UDP but not same VC and Datagram work at Network layer.
