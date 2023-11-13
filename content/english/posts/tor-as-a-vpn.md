---
title: "Tor as a VPN"
date: 2023-11-13T13:12:48+00:00
---


# Introduction

Rather than using traditional VPNs to access region-specific websites, one could use Tor as a VPN, most easily via the Tor Browser. However, it should be noted that you reduce your security benefits from using Tor, as traffic correlation attacks likely could be easier to make, simply because there is less entropy in your traffic behaviour. 


# Tor 

[Tor](https://www.torproject.org/) itself can refer to many things, the protocol, the piece of software or the Tor network (computers running Tor). The Tor protocol is an onion routing-based anonymous communication protocol. The current stable implementation is [ctor](https://gitlab.torproject.org/tpo/core/tor) or the WIP rust implementation, [arti](https://gitlab.torproject.org/tpo/core/arti). The main special aspect of Tor connections is that they involve an additional three different hops using [onion routing](https://en.wikipedia.org/wiki/Onion_routing) so that the:

- Entry node (also known as a guard node, lists of guard relays change less frequently) - knowns the IP of the sender (you) but not the destination
- Middle node - knows nothing about the sender's original request
- Exit node - does not know who you are but knows what website you are visiting, as this node would be the one sending the final requests to the server you wanted. This will be the most relevant node for this post

For more information please see the original paper of [Tor](https://svn-archive.torproject.org/svn/projects/design-paper/tor-design.pdf) or their [support page](https://support.torproject.org/) which has some FAQ. This post can also be read from an [onion service](https://community.torproject.org/onion-services/overview/). If you simply put this article's address into the Tor Browser you should be redirected to it via the [onion location meta attribute](https://community.torproject.org/onion-services/advanced/onion-location/).




# Current Tor VPN efforts

The Tor project has a plan to create [Tor VPN Client for Android](https://gitlab.torproject.org/tpo/team/-/wikis/Sponsor%20101). They want to add support [UDP](https://en.wikipedia.org/wiki/User_Datagram_Protocol) traffic over Tor, as currently Tor only works on [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol). UDP is usually used for VPN, given that higher throughput rather than more reliability is typically desired.


# Approach

The approach to similarly using Tor as a traditional VPN to access region-specific websites is rather simple, all we have to do is specify the exit relay that we use to be in the desired country, as that is the only relay communicating with the server.


# Tor exit node distributions

This information was obtained from Tor Project's [Onionoo](https://metrics.torproject.org/onionoo.html). Below you can see the distribution of active Tor exit relays across the world. Note the gaps in certain regions.


![World Map of the number of tor exit relays per country](/images/posts/tor-as-a-vpn/exit_relays_1699881168.svg)

For a table displaying the same information, please see the [Appendix](#appendix). Interestingly, the Netherlands has the highest number of exit relays, likely because of one of the largest [relay families](https://metrics.torproject.org/rs.html#search/family:FD3419724819084AABD85033CBF7005D3C1905BC) from https://nothingtohide.nl/, they have 287 exit relays.



# Specifying exit relays

To use a specific subset of exit relays, one needs to exit their `torrc` file (the tor config file, typically located in `..TorBrowser/Data/Tor/torrc`). For example, if I only want to use US exit relays I would add the following into my `torrc` file. 

```
ExitNodes {us}
StrictNodes 1
```
The country codes are in the form of [ISO 2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). 

If for some reason the region you want an exit node that is more specific than an entire country, for example, a specific state/ISP, then you could based on the IPs of the exit relays try to find one that meets your requirements. Thereafter, one can do the following in your `torrc` file.

```
ExitNodes NodeHash
StrictNodes 1
```


# Appendix 


For the methodology of how these numbers were obtained, please see https://gist.github.com/lucasalavapena/580a96c355d06f8e3ab773e08dcc96b2 . These hopefully are accurate for the state of the Tor network on :  
`Mon Nov 13 2023 13:12:48 GMT+0000`

Table of Active Exit Relays per Country, listed in descending order

| Country      | Active Exit Relays |
|  :----:      |    :----:   |
| Netherlands      | 493       | 
| Germany      | 490       | 
| United States      | 434       | 
| Poland      | 255       | 
| Luxembourg      | 113       | 
| Austria      | 108       | 
| Romania      | 88       | 
| France      | 62       | 
| Norway      | 59       | 
| Sweden      | 54       | 
| Switzerland      | 42       | 
| Russian Federation      | 31       | 
| Iceland      | 20       | 
| Canada      | 19       | 
| Ukraine      | 18       | 
| Moldova, Republic of      | 17       | 
| Denmark      | 16       | 
| United Kingdom      | 15       | 
| Bulgaria      | 15       | 
| Czechia      | 13       | 
| Finland      | 11       | 
| Croatia      | 11       | 
| Singapore      | 7       | 
| Italy      | 5       | 
| Hungary      | 5       | 
| South Africa      | 4       | 
| Korea, Republic of      | 3       | 
| Latvia      | 3       | 
| Hong Kong      | 3       | 
| Indonesia      | 3       | 
| Costa Rica      | 3       | 
| Estonia      | 2       | 
| Viet Nam      | 2       | 
| Belgium      | 2       | 
| Kazakhstan      | 2       | 
| Chile      | 2       | 
| Brazil      | 1       | 
| Taiwan, Province of China      | 1       | 
| Peru      | 1       | 
| Australia      | 1       | 
| Japan      | 1       | 
| Ethiopia      | 1       | 
| Lithuania      | 1       | 
| Mexico      | 1       | 
| Israel      | 1       | 
| Colombia      | 1       | 
| Spain      | 1       | 
