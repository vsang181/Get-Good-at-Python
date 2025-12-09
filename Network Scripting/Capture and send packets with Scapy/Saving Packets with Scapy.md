# Saving Packets with Scapy

Once we have captured packets with Scapy, we can save them to a `.pcap` file for later analysis. This is especially useful when we want to examine the captured traffic using external tools such as **tcpdump** or **Wireshark**.

We can save the packets by using the `wrpcap()` function.

```
>>> pkts = sniff(iface="en0", count=10, prn=lambda x: x.summary(), filter="tcp")
Ether / IP / TCP 162.159.134.234:https > 192.168.1.168:58932 PA / Raw
Ether / IP / TCP 192.168.1.168:58932 > 162.159.134.234:https A
Ether / IP / TCP 162.159.134.234:https > 192.168.1.168:58932 PA / Raw
Ether / IP / TCP 192.168.1.168:58932 > 162.159.134.234:https A
Ether / IP / TCP 162.159.134.234:https > 192.168.1.168:58932 PA / Raw
Ether / IP / TCP 192.168.1.168:58932 > 162.159.134.234:https A
Ether / IP / TCP 162.159.134.234:https > 192.168.1.168:58932 PA / Raw
Ether / IP / TCP 192.168.1.168:58932 > 162.159.134.234:https A
Ether / IP / TCP 162.159.134.234:https > 192.168.1.168:58932 PA / Raw
Ether / IP / TCP 192.168.1.168:58932 > 162.159.134.234:https A
>>> wrpcap('sniffed.pcap', pkts)
```

The `wrpcap()` function writes the list of captured packets (`pkts`) to a file named `sniffed.pcap`. Once saved, the `.pcap` file can be inspected using your preferred analysis tools.

For example, we can use **tcpdump** to read the captured packets:

```
~ % sudo tcpdump -r sniffed.pcap
reading from file sniffed.pcap, link-type EN10MB (Ethernet)
22:25:44.214290 IP 162.159.134.234.https > mac-2.powerhub.58932: Flags [P.], seq 407775002:407775080, ack 1855389358, win 16, options [nop,nop,TS val 2332139801 ecr 773534294], length 78
22:25:44.214420 IP mac-2.powerhub.58932 > 162.159.134.234.https: Flags [.], ack 78, win 9691, options [nop,nop,TS val 773537875 ecr 2332139801], length 0
22:25:44.221584 IP 162.159.134.234.https > mac-2.powerhub.58932: Flags [P.], seq 78:137, ack 1, win 16, options [nop,nop,TS val 2332139875 ecr 773534294], length 59
22:25:44.221712 IP mac-2.powerhub.58932 > 162.159.134.234.https: Flags [.], ack 137, win 9691, options [nop,nop,TS val 773537882 ecr 2332139875], length 0
22:25:44.830189 IP 162.159.134.234.https > mac-2.powerhub.58932: Flags [P.], seq 137:175, ack 1, win 16, options [nop,nop,TS val 2332140433 ecr 773537882], length 38
22:25:44.830332 IP mac-2.powerhub.58932 > 162.159.134.234.https: Flags [.], ack 175, win 9692, options [nop,nop,TS val 773538491 ecr 2332140433], length 0
22:25:45.445437 IP 162.159.134.234.https > mac-2.powerhub.58932: Flags [P.], seq 175:223, ack 1, win 16, options [nop,nop,TS val 2332141005 ecr 773538491], length 48
22:25:45.445596 IP mac-2.powerhub.58932 > 162.159.134.234.https: Flags [.], ack 223, win 9692, options [nop,nop,TS val 773539106 ecr 2332141005], length 0
22:25:47.389022 IP 162.159.134.234.https > mac-2.powerhub.58932: Flags [P.], seq 223:361, ack 1, win 16, options [nop,nop,TS val 2332143030 ecr 773539106], length 138
22:25:47.389179 IP mac-2.powerhub.58932 > 162.159.134.234.https: Flags [.], ack 361, win 9690, options [nop,nop,TS val 773541050 ecr 2332143030], length 0
```

This output demonstrates how the `.pcap` file can be read and interpreted. Each line shows metadata about the packet, including timestamps, IP addresses, port numbers, TCP flags, sequence numbers, and payload length. Because the traffic shown here is HTTPS, the actual packet contents are encrypted, but the TCP session metadata is still visible and useful for analysis.
