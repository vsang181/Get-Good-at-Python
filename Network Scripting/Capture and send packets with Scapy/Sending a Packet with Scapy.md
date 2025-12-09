# Sending a Packet with Scapy

To send a packet to a target using Scapy, we must first **construct** the packet. Scapy allows us to build packets layer by layer using a simple and intuitive syntax.

Let us begin by creating a basic IP packet:

```
>>> packet = IP(dst = "www.securityshenanigans.com")
```

This command creates an IP-layer packet whose destination is www.securityshenanigans.com. However, sending an empty IP packet is rarely useful, so let us make our packet more structured and meaningful.

```
>>> packet = IP(dst = "www.securityshenanigans.com")/ICMP()/"Ping SecurityShenanigans"
```

In this version:

- The **IP layer** specifies the destination host.

- The **ICMP layer** creates a standard ICMP message (e.g., echo-request).

- The **raw payload** `"Ping SecurityShenanigans"` is appended so that the destination receives our custom message.

Before sending the packet, we can inspect its structure using Scapy’s `show()` method:

```
>>> packet.show
<bound method Packet.show of <IP  frag=0 proto=icmp dst=Net("www.securityshenanigans.com/32") |<ICMP  |<Raw  load=b'Ping SecurityShenanigans' |>>>> 
```

This output confirms the structure and contents of the packet that Scapy will send.

Once satisfied with its configuration, we can transmit the packet with the `send()` function:

```
>>> send(packet)
.
Sent 1 packets.
```

Scapy informs us that the packet has been successfully transmitted. However, Scapy’s `send()` function **does not display the response**—it only sends the packet.

To observe the response, we must run a **packet capture** in a separate terminal window. Using Scapy’s `sniff()` function, we can listen for ICMP packets:

```
>>> capture=sniff(filter="icmp", iface="en0", count=2, prn=lambda x:x.summary())
```

Now return to the original Scapy terminal and resend the packet:

```
>>> send(packet)
```

The listening Scapy instance will detect both the outgoing echo-request and the incoming echo-reply:

```
>>> capture=sniff(filter="icmp", iface="en0", count=2, prn=lambda x:x.summary())
Ether / IP / ICMP 192.168.1.168 > 34.120.137.41 echo-request 0 / Raw
Ether / IP / ICMP 34.120.137.41 > 192.168.1.168 echo-reply 0 / Raw
```

This demonstrates a complete round trip: the packet was sent to the destination, and the destination responded.

## NOTE: Packet Spoofing

Packet spoofing occurs when a sender **falsifies the source IP address** in a packet. This causes the receiver to believe the packet originated from a different host. Attackers may spoof packets to obscure their true location or impersonate another system. Scapy fully supports crafting spoofed packets, which is powerful for testing—but also potentially dangerous when misused.
