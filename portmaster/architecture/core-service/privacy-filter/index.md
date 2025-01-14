---
title: Privacy Filter
layout: base
---

### Privacy Filter

{% include code_ref.html godoc_portmaster="firewall" github_portmaster="firewall/master.go" %}

The Privacy Filter is one of the most important parts of the Portmaster: It protects your privacy by blocking connections that are deemed a privacy intrusion deemed by you or the Portmaster itself.

It evaluates all connections leaving or entering your system. Filters are applied to both DNS queries as well as network connections. Every request or connection is run through a long list of checks and settings in order to protect your privacy as best possible.

In addition to rule lists and block lists, the Privacy Filter provides a big set of advanced and dynamic filtering options. It also blocks attempts to circumvent the filtering and enforces it everywhere, all the time.

---

### Connection Evaluation Stages

These are the stages which every connection goes through when being evaluated - from top to bottom:

###### Own Connections
The Portmaster checks if the connections belongs to itself. This is important in order to prevent the Portmaster from breaking itself. This in no way reduces control of the user over the Portmaster: Every feature that requires network communication can be turned off.

###### Internal Connections
Connections that come from and go to the same program/binary, even if they are different processes. These are always allowed.

###### Connection Type
Incoming or direct connections (P2P) are blocked, if configured.

###### Connection Scope
Connections are blocked according to their scope if enabled by  `Block Device-Local Connections`, `Block LAN` or `Block Internet Access`. This applies to both incoming and outgoing connections.

###### Rules
Connections are matched against the rule list:

- (1) Outgoing Rules: Rules that apply to outgoing network connections. Cannot overrule the above mentioned Connection Scopes and Connection Types.

- (2) Incoming Rules: Rules that apply to incoming network connections. Cannot overrule the above mentioned Connection Scopes and Connection Types.

_Note: The default action for incoming connections is to always block_

###### Connectivity Domains
Numerous systems and softare use a special domain in order to determine if they are online or not. The Portmaster grants special access to these domains if the Portmaster has not yet detected that the device is online. This improves network bootstrapping.

###### Bypass Prevention
Processes are prevented from bypassing the Portmaster. This includes:

- Notifying Firefox that it should not use its own DNS-over-HTTPS resolver, but fall back to plain DNS, which the Portmaster then handles.
- Blocking known domains and IPs of DoH and DoT nameservers.

###### Filter Lists
Blocks connection if the domain is listed on an activated filter list.

###### Default Action For Incoming Connections
At this point any incoming connection is blocked by default.

###### Domain Heuristics
The Portmaster applies some basic heuristics to detect malicious behaviour in the DNS system. This currently is rather primitive, but should be able to block the most obvious domains generated by malware, but also DNS tunnels.

###### Auto Permit
This a convenience feature that aims to reduce the amount of user interaction for simple applications. It checks if it can find a match between a process and the server it wants to connect to. It currently checks name similarity and will check based on signatures in the future. If there is a good enough match, the connection is permitted. Example: `Spotify` wants to connect to `spotify.com`.

###### Default Action
If nothing up to this point wanted to have a say in the decision, the default action is applied.

### Filter Lists

{% include code_ref.html godoc_portmaster="intel/filterlists" %}

The Filter Lists module is responsible for fetching the filter lists, managing them and providing lightning fast access to them.

All the lists we include, as well as our own, are managed in this [Github repo](https://github.com/safing/intel-data). The collection of sources can be found [here](https://github.com/safing/intel-data/blob/master/lists/sources.yml).

All these sources are fetched regularly and repackaged into incremental updates, which are distributed via the update system. High frequency lists are updated every hour to give you the best possible protection.

These incremental updates are then "stitched back together" in the Portmaster, as well as fed into a bloom filter in order to provide lightning fast inclusion checks.

The filter lists can be configured in the settings and can be selected by category or indiviually.

### IP Metadata

{% include code_ref.html godoc_portmaster="intel/geoip" %}

This modules provides IP address metadata. This is usually referred to as "GeoIP", but in reality there is much more important information in there than just location.

We currently build our own IP metadata database, which includes:
- Continent
- Country
- Coordinates
- ASN (Autonomous System Number)
- Owner (Organization)

The data comes from [DB-IP](https://db-ip.com/) and [IPtoASN](https://iptoasn.com/) and we merge both data sources into a new database in the `mmdb` format created by [MaxMind](https://www.maxmind.com/).

We will also add more detailed logical Internet location information from our own gathering system in the future.
