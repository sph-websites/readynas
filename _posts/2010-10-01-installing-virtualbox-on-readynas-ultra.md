---
title: Installing VirtualBox on the ReadyNAS Ultra
date: 2010-10-01
toc: false
excerpt: |
  Here are the steps I used to install the 64 bit version of VB 3.2.8 under RAIDiator 4.2.13 - all worked perfectly first time (though hope I haven't forgotten to copy/paste something)
tags:
  - Applications
---

![Vbox Icon][]

So - I finally got around to reinstalling VB on my Ultra-4.

Here are the steps I used to install the 64 bit version of VB 3.2.8 under RAIDiator 4.2.13 - all worked perfectly first time (though hope I haven't forgotten to copy/paste something)

```shell
cd /c/backup
apt-get update
apt-get install build-essential amd64-libs lib64stdc++6 bzip2 lib64z1 lzma
apt-get --reinstall install libc6-amd64
wget -q http://www.readynas.com/download/GPL/RNDP6xxx_4.2.13_WW_src.zip
unzip -q RNDP6xxx_4.2.13_WW_src.zip -d ./GPL cd GPL/linux-2.6.33.6
make ARCH=x86_64 make prepare
ln -s /c/backup/GPL/linux-2.6.33.6 /usr/src/linux
export KERN_DIR=/usr/src/linux
wget -q http://download.virtualbox.org/virtualbox/3.2.8/VirtualBox-3.2.8-64453-Linux_amd64.run
chmod 755 VirtualBox-3.2.8-64453-Linux_amd64.run
./VirtualBox-3.2.8-64453-Linux_amd64.run
/etc/init.d/vboxdrv start
```

Note: I've also posted these steps in the [ReadyNAS Developers Forum] - I'm posting them again here before they get lost in yet more pages of posts

**Update 17-Oct-2010:**

VirtualBox 3.2.10 working fine on RAIDiator 4.2.15, though a kernel recompilation is needed for upgrading

[ReadyNAS Developers Forum]: http://www.readynas.com/forum/viewtopic.php?f=35&t=26468&start=225#p258406

[Vbox Icon]: /assets/images/readynas/virtualbox-icon.png
{: .sph_img_left}
