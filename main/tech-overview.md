---
title: Tech Overview
section: main
order: 1
layout: base
updated: 19.02.2019
---

Here is short and very technical overview of the Portmaster, Gate17 and Stamp.

## Portmaster

The Portmaster is an application firewall that enforces application profiles on processes.

Being an application firewall means tightly integrating with the kernel of the underlying OS <span class="text-lighter">(via network filter APIs or kernel modules)</span> to gain needed information <span class="text-lighter">(associate network packets to processes)</span> and control <span class="text-lighter">(block or deny network connections)</span>.

Application profiles describe an application's behavior in the sense of how it interacts with the Internet: Does it connect to a fixed set of domains? Is it a peer to peer application? Does it interact with the local network? Should TLS be enforced and checked? etc.

Profiles represent an application as experienced by the user, not as defined by technology - making them easy to understand and superior to other common application classification approaches.
They can be either created by users themselves or - most of the times - obtained through Stamp <span class="text-lighter">(explained later)</span>.

## Gate17

Gate17 brings together several state of the art network technologies and gives them a new spicy twist 🌶️.  
The goal of Gate17 is to protect connection data as well as metadata from [surveillance capitalism](https://en.wikipedia.org/wiki/Surveillance_capitalism).

Adapted core concepts:

- To protect your privacy, we use newest proven encryption technology: a __double ratchet__ [^doubleratchet] based protocol to provide perfect forward and backward secrecy which can change used algorithms on demand through configuration.
- The __onion-encrypted multi-hop architecture__ [^onionrouting] protects your identity and makes you anonymous online.
- __Zero roundtrip__ connection establishment enable blazing fast connections.
- __Paid community nodes__ are highly welcome to build a huge, capable and trustless network.

The new spicy twist 🌶️:

- To protect network data and metadata as long as possible, Gate17 selects exit nodes [^exitnode] in proximity to the destination server.
- Routes are calculated for maximum speed by default and use a minimum of 3 nodes. This behavior changes based on the active security level, providing slower, but tougher routes with more nodes.
- Exit node [^exitnode] selection can be influenced up to application/domain pairs.
- Unencrypted connections are only handled by trusted nodes run by Safing. In this sense we act as a trusted anchor until all the web is encrypted. There is no room for MITM-ing [^mitm] nodes.
- As soon as the network has a good share of community nodes, routing will diversify routes by node ownership to further reduce needed trust on single parties <span class="text-lighter">(us)</span>.
- Tunnels are layer 5 [^osi] and up to reduce unnecessary metadata and improve speed <span class="text-lighter">(similar to SOCKS proxies)</span>.
- Clients always know about the full network. <span class="text-lighter">(will require improved method for better scaling at some point)</span>
- Authentication is decoupled from network nodes - they only know that someone is allowed to use the network, but not who.
- Payment via cryptocurrencies allows unblockable payment access.
- Tight integration with Portmaster ensures that no data will ever leak should a tunnel break. <span class="text-lighter">(unlike VPNs)</span>

[^doubleratchet]: [Double Ratchet Algorithm](https://en.wikipedia.org/wiki/Double_Ratchet_Algorithm)
[^onionrouting]: [Onion routing](https://en.wikipedia.org/wiki/Onion_routing)
[^exitnode]: final network node from which the connection is made to the destination server
[^mitm]: [Man-in-the-Middle Attack](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)
[^osi]: [OSI network model](https://en.wikipedia.org/wiki/OSI_model)

<span class="note-light"> A final note: You may have noted that Gate17 is, in some aspects, similar to the [Tor Project](https://www.torproject.org/). The key difference is, that Gate17 focuses on speed and usability, but does not claim to match Tor's level of security. We will provide a in-depth comparison in the future.</span>

## Stamp

Stamp is an online Community, which crowd-sources web & application intelligence. Users are rewarded with reputation for their good contributions, which in return gives them more influence on the platform. Its current main purpose is to collect data for Portmaster. Check it our [here](https://stamp.community/).

<hr>
