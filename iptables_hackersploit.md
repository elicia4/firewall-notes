# iptables [***go back to README***](README.md)

---

These are notes on this video by HackerSploit: https://youtu.be/6Ra17Qpj68c

`iptables` can be a little bit complicated if you're unfamiliar with the
lexicon that is used in regards to tables, chains, and so on.

Things that will be discussed:

- How does `iptables` work
- Syntax
- Rules 

Netfilter is the firewall framework of Linux, `iptables` is a utility that is
used to manage and control `netfilter`. `iptables` is not only responsible of
filtering traffic on a system, it also deals with such aspects of networking as
NAT connections, the ability to modify packets, to act as a router and so on.
It can be used to filter both incoming and outgoing packets, and also route
packets on a network (as a router would do).

A table within `iptables` is a collection of chains that is responsible for
handling a certain aspect of networking. Take a look at the following table:

| FILTER TABLE | NAT TABLE | MANGLE TABLE |
| :-------: | :-------: | :-------: |
| INPUT CHAIN | OUTPUT CHAIN | INPUT CHAIN |
| OUTPUT CHAIN | PREROUTING CHAIN | OUTPUT CHAIN |
| FORWARD CHAIN | POSTROUTING CHAIN | FORWARD CHAIN |
| | | FORWARD CHAIN |
| | | PREROUTING CHAIN |
| | | POSRTROUTING CHAIN |

- The **FILTER TABLE** is responsible for filtering incoming and outgoing
  traffic. It deals with the firewall aspect. 
- The **NAT TABLE** is responsible for redirecting connections to other
  interfaces on the network.
- The **MANGLE TABLE** deals with modifying and changing various aspects of a
  packet or a connection.

We're only going to focus on the **FILTER TABLE** because it is the one 
responsible for filtering connections.

This table structure is how `iptables` deals with the complexity of networking,
by categorizing different aspects of functionality in forms of tables.

Chains can be seen as tags that define and match packets to the estate. For
example, within the **FILTER TABLE** we have the **INPUT**, **OUTPUT**, and
**FORWARD** chains. And from this we can understand what which one of them is
responsible for. Each of them is responsible for processing packets based on
their type. Into the target == **INPUT CHAIN**, out of the server == **OUTPUT
CHAIN**, packets that are being forwarded from one computer to another will be
processed by the **FORWARD** chain. We are only interested in the **INPUT** and
**OUTPUT** chains since they deal with ingress[^1] and outgress[^2]  traffic. 
[^1]: traffic coming in
[^2]: traffic coming out

