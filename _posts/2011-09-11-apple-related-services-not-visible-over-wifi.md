---
title: Apple Related Services not Visible over WiFi
date: 2011-09-10
redirect_from: /2011/09/apple-related-services-not-visible-over_8538.html
toc: false
tags:
  - Networking
---

Apple products primarily rely on a technology called [mDNS][] to advertise and discover the availability of services, the Apple implementation commonly known as [Bonjour][]. ReadyNAS products implement the  Linux application [Avahi][] to provide mDNS support for Mac users.

Unfortunately however, a number of Wireless routers do not properly support mDNS over a wireless connection, and as a consequence it can appear that a ReadyNAS device is not working correctly when in reality the issue is caused by the router effectively blocking the necessary advertisements.

Typical symptoms include:

* ReadyNAS devices do not appear in (or sporadically disappear from) the OSX Finder sidebar, preventing access to shares
* ReadyNAS devices are not discoverable in Time Machine,
* The iTunes Server shared library does not appear in the iTunes sidebar - for Windows or OSX users

To test if the your router is suffering this issue, temporarily connect your client via a wired ethernet connection - if the ReadyNAS is then visible you can be pretty sure the router is at fault

Below is a list of the routers that appear to demonstrate this issue:

* Thomson routers in general, but specifically:
  * BT Home Hub (Seems to be the worst affected as may also exhibit this issue over a wired connection!)
  * O2 provided Router
  * Telia Home Gateway
* Netgear Wireless-G routers in general, but specifically:
  * WGT624 v3, DGN2000, RangeMax WPN824
* Home Box from TDC (Sagem F@ast 3464)
* Billion modem/router
* Belkin Playmax F7D 4401
* Belkin Play
* Tiscali Siemens router
* Trendnet TEW-639GR

Note that D-Link routers can also suffer this issue, but this can typically be corrected by enabling Multicast support for the wireless connection within the router setup

Please post below if you find other routers that experience this issue and I shall add them to the list.

[mDNS]:    http://en.wikipedia.org/wiki/Multicast_DNS "mDNS"
[Bonjour]: http://www.apple.com/support/bonjour/ "Bonjour"
[Avahi]:   http://avahi.org/ "Avahi"
