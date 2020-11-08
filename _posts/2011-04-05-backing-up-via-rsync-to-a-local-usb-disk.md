---
title: Backing-up via Rsync to a local USB disk
date: 2011-04-05
toc: false
tags:
  - Backup
  - Applications
---

It is often desirable to use rsync to backup data due to the benefits it offers: true incremental backup, the ability to remove data from the backup that has been deleted in the source and rsync's support for verification of the backed-up data are just some of the advantages.

Below is an example of the backup settings needed to enable rsync to be used to backup a NAS share to a locally attached USB drive.

![Rsync Backup Source][]

![Rsync Backup Destination][]

In the above example all Home Shares are being backed-up to a USB drive called "USB_Shares" and stored in the subdirectory "home". Other shares can be backed up similarly.

**Notes:**

* It is equally valid to specify an rsync server source - using the name of the share to be backed-up in the folder dialog - and the USB drive share as the destination
* Rsync must be enabled in Frontview » Services » Standard File Protocols
* Rsync access is controlled via Frontview » Shares » Share Listing, and selecting the rsync option for the appropriate USB drive (or share if an rsync source is specified)

[Rsync Backup Source]: {% link /assets/images/readynas/HomeShareUSBBackupSrc.jpg %} "Backup Source"
{: .sph_img_ctr}

[Rsync Backup Destination]: {% link /assets/images/readynas/HomeShareUSBBackupDest.jpg %} "Backup Destination"
{: .sph_img_ctr}
