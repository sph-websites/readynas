---
title: My ReadyNAS Wishlist
toc_label: My Wishlist
date: 2011-05-04
tags:
  - General
---

After using ReadyNAS devices for a few years now, I have a number of features that I would like to see in future products and software. None are earth-shattering enhancements - many would address the tweaks documented on this blog for instance. But some are already supported on competitor products and could address many of the more common ease of use issues we ReadyNAS users often encounter.

Whether you believe these ideas are 'right' or 'wrong', worthwhile or  not, I thought I'd take the time to list them and track when (or if) any of them are addressed, if only for my own benefit. I may well also add other items as they occur to me.

The list is in no particular order other than to try and categorise the requests in some limited way.

Note: I fully appreciate there are security implications to some of these requests, but i consider that is only reason to fully document those risks not decline support of the feature as to great a risk.

## General

* Software Documentation
  * I'd like some... For example
    * A FAQ that is actually up to date (for instance actually mentioning ReadyNAS Ultra, ReadyDLNA or iSCSI)
    * A user guide for ReadyDLNA - that includes how to debug when scanning fails, what file formats are supported etc
    * A user guide for iSCSI
    * A user guide (and privacy policy) for ReadyNAS Photos
    * Full specifications for products (eg what Processor does each NAS use?)
    * Publishing a [Guide to setting up share access & permissions][] would substantially reduce the number of hits this site gets...
* **eSATA**
  * My one & only Hardware-specific feature request. For most home users, external drives are the only economical way to back up their NAS data - and despite the many discussions of eSATA vs USB on the ReadyNAS forums, I find the lack of eSATA ports on new ReadyNAS products absolutely nonsensical. Couple that with the addition of USB3 that has happened to the Ultra-2, which a year after release still does not appear to be working properly with USB3 disks hardly vindicates Netgear's decision that this a better alternative.
  * This will certainly be a key decision criteria for me when I upgrade my NAS storage in future
* Solid Media Streaming Support
  * ReadyNAS devices provide DLNA, Squeezebox Server and iTunes Music Streaming support "out of the box" and have done for many years. But how and when will this capability develop?
    * Itunes Server is now so limited as to be useless to many users
    * There is no Netgear support for mobile devices,
    * 3rd party support is announced and then dropped (Orb)
    * No documentation provided
  * The reliance on 3rd parties suggests that this is not a focus for the ReadyNAS team despite advertising otherwise
* Photos Application Support without the 3rd Party server requirements
  * No application running on my NAS should cause me to be reliant on a 3rd party server just to enable operation
* Stop relying on the community
  * The ReadyNAS community has a very strong reputation and is a primary reason for many users to choose Netgear - myself included. However Netgear appear to be relying on the community to provide advertised features - for example Torrent Support. If a feature is claimed as supported, then it should be supported & provided by Netgear

## Backup & Restore

* Ability to Name Backup Jobs
  * Backup jobs are numbered. If a job fails I get the informative message that _"Backup Job 013 has encountered an error"_. I would like to name rather than just number my jobs so that such messages are meaningful at a glance
* Rsync Access to Home Shares
  * I backup all my data to a USB drives using rsync, but also to a second NAS by pulling the data from my primary NAS via Rsync. This works great except for home shares - rsync access is not allowed. This is a pain to deal with.
* Controlled NFS access to home shares
  * Similar to lack of rsync access, NFS access cannot be customised to allow root privileges like other shares, meaning that backup and restore of home shares is needlessly difficult.
  * The inability to control access via host name/address to home shares also means these shares are open to all network users - an unnecessary security hole
* iSCSI Backup/Replication
  * As stated elsewhere on this blog, I feel the addition of iSCSI to consumer NAS is one of the best enhancements recently made to ReadyNAS devices. But iSCSI comes with its own challenges - particularly in the area of backup. I would like to see Netgear address iSCSI LUN backup/replication in some way for users like myself.

## Web Server Configuration

* SSL Certificate install
  * Like many people I wish to access my NAS remotely, for instance setting up this website. I also want access to be secure and ReadyNAS does fully support HTTPS and FTPS, but only with self-signed certificates that generate warnings that are unfamiliar to non-technical users. As posted [here][ssl] it is possible to support commercial SSL certificates but requires hacking to make it work, rather than there being a simple install facility in Frontview.
* Virtual Host Support
  * Yes - I would have liked to have setup this site to be "readynas.sphardy.com", but again while such support for Virtualhosts is possible and not difficult, it requires more hacking, and in this case changes that will be overwritten each time the firmware is updated.

## Maintenance & Management

* A User Interface for the 21st Century
  * Compare [Frontview][] to [Synology DSM][] (user: admin, Password: synology) - enough said
* UI Improvements for large/small screens
  * My primary client has a screen with resolution 1920x1200 - and yet I still need to scroll around in Frontview to access most options. Equally, I have and iPhone & iPad that I would like to use to manage the NAS - Frontview is hardly 'tuned' for such screens.
* GUI to view logs
  * One of the most common problem solving steps is to review the NAS logs, of which there are many available purely as text files. How about a GUI that both provides some kind of context/organisation to the reports (do you expect DLNA errors to be found in the UPNP-av.log?)  as well as assistance in looking at those logs (eg highlighting of errors). For the average user this is simply not a debugging step they can undertake.
  * This idea may of course become redundant if a new approach to presenting logs is taken, instead of just dumping individual logs per linux process eg as part of an updated interface.
* Vol Maintenance NOW option
  * It is possible to schedule both online Volume checks and RAID scrubbing - why is there not a "Do this NOW" button?
* iSCSI LUN management
  * The current iSCSI management within Frontview is extremely limited. I want the ability to be able to delete and move individual LUNs, assign LUNs to different targets, manage backup & restores, all via drag and drop and/or some other simply step-by-step wizard.
* Access to the 'C' volume over AFP / NFS
  * Why do CIFS users get all the perks? Admin access to the C volume via NFS and [AFP][] should be enabled
* NAS Status monitoring
  * Thanks to forum members like Super-Poussin and WhoCares? there are numerous ways to monitor the status of your NAS. But should this really require a 3rd party solution? At the very least a customisable status update could be generated & emailed on a user defined schedule. To the other extreme I'd like to see a Netgear-implemented & supported monitoring capability rather than have to use a bunch of addons.
* Snapshot Resizing
  * Will this ability ever return or should the statement _"Snapshot resizing is disabled in the release. We will re-enable this feature in a future update"_ that has been published in the release notes for many firmware releases now be changed?

## Share Access

* True Builtin Web-based File Manager
  * The current HTTP file manager is very primitive and incompatible with WebDAV access. Again, addons exist to address this - I personally use Ajaxplorer - but a novice user should not have to go to such effort to enable simple, GUI based, drag & drop style remote access to shares.
  * Develop this instead of the awful ReadyNAS Remote Product which:
    * Needs the user to install a client and so is instantly less attractive
    * Is overly complex causing client networking issues and restricts bandwidth
    * Relies on 3rd party servers to work (which they often don't seem to)
    * Is sporadically updated (or not at all for Mac users)
    * Is not supported at all under Linux
* FTPS only support without hacking
  * FTP is supported. FTPS is supported. But you either get both or none and not the 3rd, more secure, option of only enabling FTPS. Easily "hackable" - but should not be necessary
* FTP HideFiles Support
  * Again CIFS users get all the perks. The built-in CIFS server is configured so that system files generated by other protocols remain hidden from users, presumeably to prevent problems by users altering those files and/or to improve ease of use (Hide what the user doesn't need to see). So why not enable the same for FTP users? The server does support this via the "HideFiles" directive - it would be useful to have this both automaticially configured to hide common system files, but also customisable by the user.
* Simultaneous Anonymous & User authenticated FTP
  * As documented [here][ftp], FTP authentication is either Anonymous OR User based - it is not possible to have both, though the fix is relatively simple
* SFTP with 'chroot' support
  * I fully appreciate that SFTP is unlikely to be formally supported due to the implications of opening up SSH access. But for those of us that are willing to 'go it alone', a version of OpenSSH that implemented SFTP with 'chroot' support doesn't seem an unreasonable request.


[Guide to setting up share access & permissions]: {% link _posts/2010-09-01-how-to-setup-readynas-permissions.md %}

[ssl]: {% link _posts/2010-10-12-installing-an-ssl-certificate-on-your-readynas.md %} "Install and SSL Certificate"
[afp]: {% link _posts/2010-10-20-enabling-admin-access-to-the-c-volume-over-afp.md %} "Admin Access over AFP"
[ftp]: {% link _posts/2011-03-23-enabling-user-anonymous-ftp-access.md %} "Enable Anonymous FTP"

[Frontview]: https://frontview.readynas.com/admin/
[Synology DSM]: http://demo.synology.com:5000/
