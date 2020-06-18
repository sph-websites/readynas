---
title: How to Direct Connect to your ReadyNAS
tagline: ""
date: 2010-09-17
toc_label: "How to connect"
redirect_from:
  - /web/directconnect
  - /2010/09/how-to-direct-connect-to-your-readynas_1197.html
---

When encountering a problem with a ReadyNAS device, it is often useful during the process of diagnosing that problem to eliminate the network to which the ReadyNAS is connected to determine if the issue is truly with the ReadyNAS, or due to the network to which it is connected.

Any ReadyNAS device can be connected directly to a client via a standard ethernet cable - there is no requirement for a cross-over cable as the ReadyNAS ethernet ports are autosensing. Therefore, to make the direct connection work, it is simply a matter of ensuring the client is configured with an appropriate IP address and subnet mask.

##  Via Static IP addresses

In the case where the ReadyNAS device has already been configured with a static IP address, a direct connection can be established by setting the client to have an IP address on the same subnet, and a subnet mask of `255.255.255.0`. For example:

If the ReadyNAS device has a static address of 192.168.0.**100**, configure the client to have an address 192.168.0.**xxx** - where **xxx** can be any integer between 1 and 250 (except, in this case, 100 which is the IP address of the ReadyNAS) Google "changing IPv4 settings" for your client if you are unfamiliar with doing this.

Once done, directly connect the client to the ReadyNAS device with a standard cable and it should be immediately available to the client

##  Via Dynamically Assigned IP addresses

If the ReadyNAS device is setup to obtain its IP address from a DHCP server, then additional steps are required to direct connect to it.

1. Power off the ReadyNAS device

2. Configure the client with any IP address on the subnet 192.168.168.xxx, (where xxx is any number between 1 and 250, except 168) - eg `192.168.168.100` - and subnetmask `255.255.255.0`. Google "changing IPv4 settings" for your client. if you are unfamiliar with doing this.

3. Connect the client to the ReadyNAS device with an ethernet cable

4. Power on the ReadyNAS device
In the absence of a DHCP server, once booted the ReadyNAS device will default to the IP address 192.168.168.168 at which point the connection should be established.

While it should not be necessary to reboot the ReadyNAS to ensure it resets its IP address to the default once directly connected to a client, this is suggested as a precaution.

##  Accessing the ReadyNAS Device

Once the connection is configured and made, Frontview should be immediately available at `https://<nas_ip_address>/admin` - in the above examples at either `https://192.168.0.100/admin` or `https://192.168.168.168/admin`.

If for any reason Frontview cannot be accessed, it is recommended to install & run [RAIDar][] to verify that the ReadyNAS device has properly booted and is available, and also that the IP address is as expected.

If, after verifying the NAS has booted and the IP addresses being used are correct, it is still not possible to direct connect, first try a new ethernet cable. While it is rare for cables to simply 'break' there may be issues due to a slightly damaged connector or a broken wire within the cable.

If the connection still fails, then it would be advisable to contact Netgear Technical Support

[RAIDar]: https://kb.netgear.com/23651/What-is-RAIDar-and-how-do-I-use-it-to-discover-my-ReadyDATA-storage-system "RAIDar"
