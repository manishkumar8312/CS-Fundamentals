# Chapter 12: Important Interview Topics

This chapter covers fundamental networking and protocol concepts frequently discussed in technical interviews. Each topic is presented with concise explanations, key differences, and practical insights.

## 1. TCP vs UDP

Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) are core transport layer protocols.

| Feature          | TCP                                           | UDP                                           |
|------------------|-----------------------------------------------|-----------------------------------------------|
| Connection       | Connection-oriented (handshake)               | Connectionless                                |
| Reliability      | Acknowledgment, retransmission, sequencing    | No guarantees                                 |
| Flow Control     | Yes (sliding window)                          | No                                            |
| Congestion Control | Yes                                         | No                                            |
| Ordering         | Preserves packet order                        | No ordering                                   |
| Overhead         | Higher (20 byte header)                       | Lower (8 byte header)                         |
| Speed            | Slower                                        | Faster                                        |
| Usage            | HTTP, HTTPS, FTP, SSH, email                  | DNS, VoIP, streaming, gaming, DHCP           |

**Key takeaway**: Use TCP when data integrity and order matter; use UDP when speed and low latency are critical, and occasional loss is acceptable.

## 2. OSI vs TCP/IP Models

Both models describe network protocol stacks but differ in layer granularity and historical origin.

**OSI Model (7 layers)**:
1. Physical
2. Data Link
3. Network
4. Transport
5. Session
6. Presentation
7. Application

**TCP/IP Model (4 layers)**:
1. Network Interface (combines OSI 1-2)
2. Internet (OSI 3)
3. Transport (OSI 4)
4. Application (OSI 5-7)

| OSI Layer          | TCP/IP Layer        | Example Protocols          |
|--------------------|---------------------|----------------------------|
| Application        | Application         | HTTP, FTP, DNS, SMTP       |
| Presentation       | Application         | TLS/SSL (partly), JPEG     |
| Session            | Application         | NetBIOS, RPC               |
| Transport          | Transport           | TCP, UDP                   |
| Network            | Internet            | IP, ICMP, ARP              |
| Data Link          | Network Interface   | Ethernet, Wi-Fi, PPP       |
| Physical           | Network Interface   | RJ45, fiber, radio         |

**Key takeaway**: OSI is a theoretical reference model; TCP/IP is the practical model of the internet.

## 3. HTTP vs HTTPS

| Feature          | HTTP                                | HTTPS                                           |
|------------------|-------------------------------------|-------------------------------------------------|
| Full form        | HyperText Transfer Protocol         | HyperText Transfer Protocol Secure              |
| Encryption       | None (plain text)                   | TLS/SSL encryption                              |
| Port             | 80                                  | 443                                             |
| Security         | Vulnerable to eavesdropping, MITM   | Confidentiality, integrity, authentication     |
| Performance      | Slightly faster (no crypto overhead)| Slightly slower due to handshake + encryption  |
| SEO impact       | Negative (browsers mark as unsafe)  | Positive (ranking boost, trust indicators)     |
| Certificate      | Not required                        | Requires CA-signed certificate                 |

**How HTTPS works**:
- Server presents a digital certificate.
- Client verifies certificate against trusted CAs.
- A symmetric session key is negotiated via asymmetric encryption (TLS handshake).
- All subsequent data is encrypted with that session key.

**Key takeaway**: Always use HTTPS for production websites to protect user data and build trust.

## 4. DNS Working (Domain Name System)

DNS translates human-readable domain names (e.g., `example.com`) to IP addresses.

**Resolution steps (recursive query)**:
1. Browser checks local cache (OS + browser).
2. If not found, query sent to **Recursive Resolver** (usually ISP or public DNS like 8.8.8.8).
3. Resolver queries a **Root nameserver** → returns TLD nameserver address.
4. Resolver queries **TLD nameserver** (e.g., for .com) → returns authoritative nameserver for domain.
5. Resolver queries **Authoritative nameserver** → receives the IP address (A or AAAA record).
6. Resolver returns IP to client; client caches result (TTL governs lifetime).

**Record types**:
- A     : IPv4 address
- AAAA  : IPv6 address
- CNAME : Canonical name (alias)
- MX    : Mail exchange
- TXT   : Text (e.g., SPF, DKIM)
- NS    : Nameserver

**Key takeaway**: DNS is a distributed, hierarchical database with caching at every level to reduce latency.

## 5. 3-Way Handshake & 4-Way Termination

These are the connection establishment and teardown procedures in TCP.

**3-Way Handshake (SYN, SYN-ACK, ACK)**:

1. Client → Server: `SYN` (seq=x)
   - Client sends a TCP segment with SYN flag set, choosing an initial sequence number.
2. Server → Client: `SYN-ACK` (seq=y, ack=x+1)
   - Server acknowledges the SYN and sends its own SYN with a different sequence number.
3. Client → Server: `ACK` (ack=y+1)
   - Client acknowledges the server's SYN. Connection is now established (ESTABLISHED state).

**State transitions**:
- Client: CLOSED → SYN_SENT → ESTABLISHED
- Server: LISTEN → SYN_RCVD → ESTABLISHED

**4-Way Termination (FIN, ACK, FIN, ACK)**:

Either side can initiate termination. Assume client initiates:

1. Client → Server: `FIN` (seq=u)
   - Client says "I have no more data to send."
2. Server → Client: `ACK` (ack=u+1)
   - Server acknowledges the FIN. Server may continue sending data (half-closed state).
3. Server → Client: `FIN` (seq=v, ack=u+1)
   - Server finishes sending its data and sends its own FIN.
4. Client → Server: `ACK` (ack=v+1)
   - Client acknowledges the FIN. After a wait (TIME_WAIT), client closes.

**Key takeaway**: The three-way handshake establishes reliable, ordered connections; the four-way termination ensures both sides agree to close without data loss.

## 6. NAT Working (Network Address Translation)

NAT allows multiple devices on a private network to share a single public IPv4 address.

**Types**:
- **Static NAT**   : One-to-one mapping (private IP ↔ public IP). Used for servers.
- **Dynamic NAT**  : Pool of public IPs assigned to private IPs as needed.
- **PAT (NAPT)**   : Many-to-one mapping using port numbers. Most common in home routers.

**How PAT works**:
- Private device (192.168.1.10:12345) sends packet to destination.
- Router replaces source IP with its public IP and assigns a unique source port (e.g., 55001).
- Router maintains a **NAT table** mapping `(private IP:port) ↔ (public IP:port, dest IP:port)`.
- Return packets are matched based on destination port and translated back.

**Key benefits**:
- Conserves IPv4 addresses.
- Hides internal network topology (basic firewall).

**Drawbacks**:
- Breaks end-to-end connectivity (some protocols like IPsec or FTP need ALGs).
- Adds latency and processing overhead.

**NAT traversal techniques**: STUN, TURN, ICE (used in VoIP, gaming, WebRTC).

## 7. Difference Between Hub, Switch, and Router

These are network devices operating at different layers of the OSI model.

| Feature          | Hub (Layer 1)                | Switch (Layer 2)             | Router (Layer 3)               |
|------------------|------------------------------|------------------------------|--------------------------------|
| OSI Layer        | Physical                     | Data Link                    | Network                        |
| Intelligence     | None (dumb repeater)         | Learns MAC addresses         | Routes between networks        |
| Traffic handling | Broadcasts to all ports      | Forwards only to destination port | Uses IP routing table      |
| Collision domain | Single (all ports share)     | Each port separate           | Each interface separate        |
| Broadcast domain | Single                       | Single (by default, unless VLAN) | Boundaries broadcast         |
| Address type     | None (electrical signals)    | MAC addresses                | IP addresses                   |
| Performance      | Low (collisions degrade)     | High (full duplex)           | Varies (depends on routing)    |
| Typical use      | Obsolete; lab/legacy only    | Connecting devices inside a LAN | Connecting LAN to WAN/Internet |

**Illustrative traffic flow**:
- Hub: Packet from A to B goes to all ports (C, D, E see it).
- Switch: After learning, A→B goes only to B's port.
- Router: Forwards between different IP subnets (e.g., LAN to Internet).

**Key takeaway**: Use switches for internal LAN efficiency, routers for inter-network connectivity; hubs are deprecated.

## References

I have revised the references section to include direct, hyperlinked URLs for each resource, making it easier for readers to access the original source material directly.

---

## References

### 1. TCP vs UDP
*   **RFC 793 (Original TCP Specification)**: A plain text version is available [here](https://packetstormsecurity.com/files/30270/rfc793.txt.html).
*   **RFC 9293 (Current TCP Standard, obsoletes RFC 793)**: Access the updated specification on the IETF website [here](https://www.rfc-editor.org/info/rfc9293).
*   **RFC 768 (UDP Specification)**: Read the complete text [here](https://www.tuhs.org/Usenet/comp.sources.unix/1985-January/000439.html).
*   **TCP/IP Illustrated, Volume 1 (Book)**: The 2nd edition can be purchased from the publisher [here](https://www.informit.com/store/tcp-ip-illustrated-volume-1-the-protocols-9780132808187).

### 2. OSI vs TCP/IP
*   **OSI Reference Model Paper (Zimmermann, 1980)**: Find it on IEEE Xplore [here](https://ieeexplore.ieee.org/document/1095638). An entry is also on Semantic Scholar [here](https://www.semanticscholar.org/paper/OSI-Reference-Model-The-ISO-Model-of-Architecture-Zimmermann/fe0a5962074aa92c59fddad527ba0a5283962de7).
*   **RFC 1122 (Requirements for Internet Hosts)**: View the document [here](https://www.ietf.org/ietf-ftp/rfc/rfc1122.html).

### 3. HTTP vs HTTPS
*   **RFC 9110 (HTTP Semantics)**: Read the official specification [here](https://datatracker.ietf.org/doc/html/rfc9110). An alternative link is [here](https://httpwg.org/specs/rfc9110.html).
*   **RFC 8446 (TLS 1.3)**: Access the full specification [here](https://www.rfc-editor.org/info/rfc8446).
*   **Let's Encrypt Documentation**: Learn how it works [here](https://letsencrypt.org/how-it-works/).

### 4. DNS Working
*   **RFC 1034 (DNS Concepts)**: Read the document [here](https://www.ietf.org/rfc/beta/errata/rfc1034.html).
*   **RFC 1035 (DNS Implementation)**: A helpful blog post discussing implementation can be found [here](https://blog.apnic.net/2024/06/12/lessons-learned-when-building-my-dns-resolver/).
*   **DNS and BIND (Book)**: Access the O'Reilly catalog page for the 4th edition [here](http://www.oreilly.com/catalog/dns4/). The copyright page is [here](http://users.softlab.ntua.gr/~sivann/books/OReilly%20Bookshelf/tcpip/dns/copyrght.htm).

### 5. 3-Way Handshake & 4-Way Termination
*   **RFC 793 (Original TCP Specification)**: See the link in section 1.
*   **RFC 9293 (Current TCP Standard)**: See the link in section 1.

### 6. NAT Working
*   **RFC 2663 (NAT Terminology)**: Read the document [here](https://www.rfc-editor.org/rfc/rfc2663).
*   **RFC 3022 (Traditional NAT)**: Access the specification [here](https://datatracker.ietf.org/doc/rfc3022/).
*   **RFC 5389 (STUN)**: Find the document [here](https://datatracker.ietf.org/doc/rfc5389/).
*   **RFC 5766 (TURN)**: Read the official information [here](https://www.rfc-editor.org/info/rfc5766).
*   **RFC 8445 (ICE)**: Access the protocol document [here](https://www.rfc-editor.org/info/rfc8445).

### 7. Hub, Switch, Router
*   **Computer Networks (Book)**: The publisher's page is [here](https://www.pearson.com/en-us/subject-catalog/p/computer-networks/P200000003157).

For further hands-on study, use `tcpdump`, `Wireshark`, `dig`, `nslookup`, and emulate networks with tools like `mininet` or Cisco Packet Tracer.
