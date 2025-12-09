# Sending and Receiving a Response from Scapy

Earlier, we introduced the `sr()` method, which allows Scapy to **send packets and immediately listen for responses.** This provides a much faster workflow compared to using `send()`, because we do not need to open a separate packet capture window—Scapy handles both sending and receiving in one step.

Let us modify our previous example to use the `sr()` method:

```
>>> packet = IP(dst = "www.securityshenanigans.com")/ICMP()/"Ping SecurityShenanigans"

>>> sr(packet)
Begin emission
..
Finished sending 1 packets
.*
Received 4 packets, got 1 answers, remaining 0 packets
(<Results: TCP:0 UDP:0 ICMP:1 Other:0>, <Unanswered: TCP:0 UDP:0 ICMP:0 Other:0>)
```

Here is what is happening:

- **Begin emission / Finished sending**

Scapy sends the packet we constructed.

- _. Received 4 packets*_

Scapy listens for replies and notes that four packets were observed during this process.

- **Got 1 answers**

One of those packets was a valid response to the ICMP request that we sent. The remaining packets are unrelated background traffic that Scapy captured while listening.

- **Remaining 0 packets**

This indicates that all outgoing packets received a response (none were left unanswered).

The `sr()` method returns a tuple containing two objects:

1. **Answered packets** — packets that received valid responses

2. **Unanswered packets** — packets that were sent but did not receive a reply

In our example:

```
(<Results: ... ICMP:1 ...>, <Unanswered: ICMP:0 ...>)
```

This shows:

- One ICMP request received an ICMP reply (successful communication)

- No packets were left unanswered

Using `sr()` provides a clean and efficient way to test packet responses without requiring parallel captures, making it especially useful for reconnaissance, crafting test probes, or validating network behaviour during penetration testing.
