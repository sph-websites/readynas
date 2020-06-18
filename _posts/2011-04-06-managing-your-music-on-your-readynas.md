---
title: Managing your Music on your ReadyNAS
date: 2011-04-06
toc: false
tags:
  - Configuration
  - Media
---

A primary use of home NAS devices is the central storage of, and access to, a media library. For many people a large portion of that library will be music, music that is also often being accessed by multiple applications: SqueezeboxServer, DLNA servers, iTunes etc.

[![Bliss Browser Shot][]][Bliss Image]

It would of course be of great advantage if that music library could be managed directly on the NAS in a manner that all these other applications can access the same consistent metadata and cover art and I recently came across the application [bliss][BlissHQ], the aim of which is exactly this - a single web based tool for organising a music library. While it appears to be in the relatively early stages of development, with an initial early focus on Album Art management, it works very, very well and I'm keen to see how it develops.

I won't cover the functionality of bliss here, there are full detailed instructions on the [bliss website][BlissHQ], but here are some instructions specifically for installing bliss on a ReadyNAS device.

****
**Note:** as bliss is a java based application it can only be supported on x86 based NAS such as the Pro and Ultra series. Sparc based devices like the Duo & NV+ are not - and will never be - supported

**Installation**

<del>Bliss requires Java v1.6 for which there is currently no addon, but which can be installed manually - instructions are provided [here](/web/readynas/installing-java-on-x86-readynas/)</del>

<del>Once Java is installed, bliss may be installed and run via SSH - installation instructions can be found here: [http://www.blisshq.com/install-linux.html][]</del>

<del>It can be run as a regular account provided that account has write access to the media (ie root access is not required) and so I would recommend installing bliss into its own share and being run via a regular user account</del>

<del>Once installed and running, bliss can be accessed at http://nas_ip_address:3220 - see screenshot above</del>

**Addon**

_(Update: 11 June, 2011)_ I have now written a ReadyNAS addon to simplify installation - details can be found at [http://sphardy.com/web/bliss](/web/bliss)

[BlissHQ]: http://blisshq.com

[http://www.blisshq.com/install-linux.html]: http://www.blisshq.com/install-linux.html

[Bliss Browser Shot]: /assets/images/readynas/BlissBrowserShot_tn.jpg
{: .sph_img_ctr}

[Bliss Image]: /assets/images/readynas/BlissBrowserShot.jpg "Screenshot of Bliss on ReadyNAS"


