# Capturing Packets with Scapy

Packet capture typically requires elevated permissions. Therefore, we must run Scapy with **sudo** privileges so that it has the ability to sniff network traffic.

To begin capturing packets in Scapy, we use the `sniff()` function. This function contains several useful parameters that allow us to filter and inspect network traffic:

## Key Parameters of `sniff()`

- **iface**: Specifies the network interface from which packets should be captured (e.g., `en0`, `eth0`).

- **count**: Determines how many packets to capture. If omitted or set to `0`, Scapy will continue sniffing indefinitely until manually stopped.

- **prn**: Defines a callback function that is applied to each packet as it is captured. For example, `lambda x: x.summary()` prints a one-line summary of each packet.

- `filter`: Allows us to capture only packets of interest using Berkeley Packet Filter (BPF) syntax, the same used by tools like tcpdump and Wireshark.

## Capturing 10 TCP Packets

Let us apply these parameters to capture 10 TCP packets on the `en0` interface and print their summaries to the terminal:

```
>>> sniff(iface="en0", count=10, prn=lambda x: x.summary(), filter="tcp")
Ether / IP / TCP 162.159.134.234:https > 192.168.1.168:58932 PA / Raw
Ether / IP / TCP 192.168.1.168:58932 > 162.159.134.234:https A
Ether / IP / TCP 162.159.134.234:https > 192.168.1.168:58932 PA / Raw
Ether / IP / TCP 192.168.1.168:58932 > 162.159.134.234:https A
...
<Sniffed: TCP:10 UDP:0 ICMP:0 Other:0>
```

## Storing Captured Packets in a Variable

We can also store the results of `sniff()` in a variable. In the example below, we assign the captured packets to a variable named `pkts` and still print summaries via the callback:

```
>>> pkts = sniff(iface="en0", count=10, prn=lambda x: x.summary(), filter="tcp")
Ether / IPv6 / TCP 2a00:1450:4009:c0b::5f:https > 2a0a:ef40:eef:3e01:294e:b1d1:31c0:68fd:59173 PA / Raw
Ether / IPv6 / TCP 2a0a:ef40:eef:3e01:294e:b1d1:31c0:68fd:59173 > 2a00:1450:4009:c0b::5f:https A
...
```

Once stored, you can inspect the `pkts` list, iterate through packets, or analyse individual packet layers.

## Viewing Full Packet Details

If you want more detailed output, you can replace `x.summary()` with `x.show()`, which prints all fields and layers of the packet:

```
>>> sniff(iface="en0", count=1, prn=lambda x: x.show(), filter="tcp")
###[ Ethernet ]###
  dst       = fe:16:b6:82:6e:15
  src       = d8:d8:e5:cf:b6:69
  type      = IPv4
###[ IP ]###
     version   = 4
     ihl       = 5
     tos       = 0x2
     len       = 156
     id        = 51758
     flags     = DF
     frag      = 0
     ttl       = 55
     proto     = tcp
     chksum    = 0x8d51
     src       = 162.159.134.234
     dst       = 192.168.1.168
###[ TCP ]###
     sport     = https
     dport     = 58932
     seq       = 407708648
     ack       = 1855387401
     flags     = PA
     window    = 16
     chksum    = 0x482a
###[ Raw ]###
     load      = b'\x17\x03\x03\x00c\xb5M\x7f\xdf/Lm}"...'
<Sniffed: TCP:1 UDP:0 ICMP:0 Other:0>
```

The `.show()` output is extremely useful when analysing packet structure, identifying important fields, and understanding how protocols are layered.

