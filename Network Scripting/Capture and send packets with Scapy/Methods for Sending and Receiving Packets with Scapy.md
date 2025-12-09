# Methods for Sending and Receiving Packets with Scapy

Scapy is not only capable of capturing packets—it can also **craft**, **send**, and **receive** packets across various network layers. When sending packets to a target, we may or may not receive a response depending on the protocol, the target's configuration, and firewall behaviour. Scapy provides several methods to facilitate these different interactions.

Below is an overview of the most commonly used Scapy sending and receiving methods.

## 1. Sending Packets — `send` and `sendp`

### send()

- Sends packets at **Layer 3** (the Network Layer).

- Scapy automatically chooses the appropriate Layer 2 information (MAC addresses) when sending Layer 3 packets.

- Useful for sending IP-based packets such as TCP, UDP, or ICMP.

### sendp()

- Sends packets at **Layer 2** (the Data Link Layer).

- Allows full control over Ethernet frames, making it useful for ARP spoofing, crafting custom Ethernet packets, or working in environments where Layer 3 routing is not desired.

## 2. Sending and Receiving Packets — `sr` Family of Functions

These functions allow Scapy to transmit packets and receive responses. Depending on the specific method, Scapy may return all answers, only the first, or none.

### sr()

- Sends packets at **Layer 3** and receives responses.

- Returns two lists:

  - **answered** packets
  
  - **unanswered** packets

- Useful for tasks such as port scanning, probing hosts, and sending crafted IP packets.

### sr1()

- Sends packets at **Layer 3**, but **returns only the first** reply received.

- Often used when expecting a single response (e.g., sending one ICMP echo request).

### srp()

- Sends packets at **Layer 2** and receives responses.

- Returns both answered and unanswered packets (similar to `sr()` but at the Ethernet frame level).

- Useful for ARP scans, custom Ethernet frames, and low-level network interactions.

### srp1()

- Sends packets at **Layer 2** and returns **only the first answer**.

- Commonly used for obtaining quick ARP responses (e.g., ARP ping).

These methods allow Scapy to behave as a highly flexible packet manipulation tool, making it ideal for network discovery, security testing, and protocol experimentation.
