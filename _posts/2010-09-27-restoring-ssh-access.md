---
title: Restoring SSH Access
date: 2010-09-27
toc: false
excerpt: |
  One of the most powerful features of the ReadyNAS product line is the ability to enable Secure SHell (SSH) access. Via SSH, it is possible to both install additional software as well as gain secure remote access to the ReadyNAS unit.
redirect_from:
  - /restoring-ssh-access/
  - /web/readynas/restoring-ssh-access/
  - /2010/09/restoring-ssh-access_4574.html
tags:
  - Security
  - Configuration
---

![SSH Image][]

One of the most powerful features of the ReadyNAS product line is the ability to enable Secure SHell (SSH) access. Via SSH, it is possible to both install additional software as well as gain secure remote access to the ReadyNAS unit.

Once enabled, many users prefer to customise their SSH access also, particularly to increase security vs the default settings by, for instance, limiting root access or requiring public key authentication be used. To achieve this it is necessary to edit the file "`/etc/ssh/sshd_config`" file.

This however can be the source of major issues - edit the `sshd_config` file incorrectly and it is possible to prevent SSH access working correctly. But without SSH access there is no way to fix the error as a firmware reinstall will not will not revert the `sshd_config` file back to the default settings. And it is a very easy mistake to make...

Fortunately there is a way to restore the file to its default settings by following these steps:

1. Download this [SSH Configuration file][] - do NOT unzip it
2. Load Frontview and go to the menu 'System -> Config Backup'
3. Select the 'Backup' tab and perform a Config Backup (this is a precaution)
4. Select the 'Restore' tab and perform a Config Restore using the ZIP file you downloaded in step 1
5. Once the restore is complete, reboot your NAS as instructed

The uploaded file contains a default sshd_config configuration including permitting root access and login with password. Once the NAS has rebooted, SSH access will (hopefully) be restored.

And next time, make sure you keep an SSH session open while you test any changes to `sshd_config`

[SSH Configuration file]: {% link /assets/docs/restore_sshd_config.zip %} "SSH Reset Configuration File"

[SSH Image]: /assets/images/readynas/ssh1.jpg
{: .sph_img_left}
