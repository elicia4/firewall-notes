# iptables
[***go back to README***](README.md)

---

These are notes on this video by HackerSploit:
https://youtu.be/6Ra17Qpj68c

iptables can be a little bit complicated if you're unfamiliar with the lexicon
that is used in regards to tables, chains, and so on.

Things that will be discussed:

- How does `iptables` work
- Syntax
- Rules 

Netfilter is the firewall framework of Linux, iptables is a utility that is used
to manage and control netfilter. iptables is not only responsible of filtering
traffic on a system, it also deals with such aspects of networking as NAT
connections, the ability to modify packets, to act as a router and so on. It can
be used to filter both incoming and outgoing packets, and also route packets on
a network (as a router would do).

A table within iptables is a collection of chains that is responsible for
handling a certain aspect of networking. Imagine you have this table:

*IPTABLES*
| FILTER TABLE | NAT TABLE | MANGLE TABLE |
| :-------: | :-------: | :-------: |
| INPUT CHAIN | OUTPUT CHAIN | INPUT CHAIN |
| OUTPUT CHAIN | PREROUTING CHAIN | OUTPUT CHAIN |
| FORWARD CHAIN | POSTROUTING CHAIN | FORWARD CHAIN |
| | | FORWARD CHAIN |
| | | PREROUTING CHAIN |
| | | POSRTROUTING CHAIN |

