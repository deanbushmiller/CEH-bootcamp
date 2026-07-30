# Scanning Glossary

> Source: `CEHv11GlossaryTRIMforMM.txt`.
> Terms are deduplicated and assigned to only one category glossary.

Terms in this glossary: 24

| Term | Definition |
|---|---|
| ACK Flag Probe Scan | Attackers send TCP probe packets set with an ACK flag to a remote device, and then analyze the header information (TTL and WINDOW field) of received RST packets to determine if the port is open or closed. |
| ARP Ping Scan | Attackers send ARP request probes to target hosts, and an ARP response indicates that the host is active. |
| Egress Filtering | scans the headers of IP packets leaving a network. |
| Firewalking | technique that uses TTL values to determine gateway ACL filters and it maps networks by analyzing the IP packet responses. |
| ICMP ECHO Ping Scan | sending ICMP ECHO requests to a host. If the host is live, it will return an ICMP ECHO reply. |
| ICMP ECHO Ping Sweep | determine the live hosts from a range of IP addresses by sending ICMP ECHO requests to multiple hosts. If a host is alive, it will return an ICMP ECHO reply. |
| Inverse TCP Flag Scan | Attackers send TCP probe packets with a TCP flag (FIN, URG, PSH) set or with no flags, where no response implies that the port is open, whereas an RST response means that the port is closed. |
| IP Address Decoy | generating or manually specifying the IP addresses of decoys in order to evade an IDS or firewall. |
| Network Scanning | a set of procedures used for identifying hosts, ports, and services in a network. |
| OS Discovery/Banner Grabbing | method used to determine the operating system running on a remote target system. |
| Packet Fragmentation | the splitting of a probe packet into several smaller packets (fragments) while sending it to a network. |
| Ping of Death Attack | sending malformed or oversized packets using ICMP for denial of service |
| Port Scanning | identify open ports and the services running on these ports. |
| Protocol Anomaly Detection | built to explore anomalies in the way in which vendors deploy the TCP/IP specification. |
| Scanning | the pre-attack phase when the attacker scans the network for specific information based on information gathered during reconnaissance. |
| SCTP COOKIE ECHO Scanning | Attackers send a COOKIE ECHO chunk to the target host, and no response implies that the port is open, whereas an ABORT Chunk response means that the port is closed. |
| SCTP INIT Scanning | Attackers send an INIT chunk to the target host, and an INIT+ACK chunk response implies that the port is open, whereas an ABORT Chunk response means that the port is closed. |
| Session Splicing | technique used to bypass the IDS where an attacker splits the attack traffic into many packets such that no single packet triggers the IDS. |
| Source Port Manipulation | manipulating actual port numbers with common port numbers in order to evade an IDS or firewall. |
| Source Routing | sending a packet to the intended destination with a partially or completely specified route (without firewall-/IDS-configured routers) in order to evade an IDS or firewall. |
| Stealth Scan (Half-open Scan) | abruptly resetting the TCP connection between the client and server before the completion of three-way handshake signals, thus leaving the connection half-open. |
| Traceroute | program uses ICMP protocol and TTL field to discover routers on the path to a target host. |
| UDP Ping Scan | Attackers send UDP packets to target hosts, and a UDP response indicates that the host is active. |
| Xmas Scan | type of inverse TCP scanning technique with the FIN, URG, and PUSH flags set to send a TCP frame to a remote device. |
