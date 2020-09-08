---
title: How to Setup ReadyNAS Permissions
date: 2010-09-01
redirect_from:
  - /HowToSetupReadyNASPermissions/
  - /web/HowToSetupReadyNASPermissions/
  - /web/readynas/HowToSetupReadyNASPermissions/
  - /2010/09/how-to-setup-readynas-permissions_5296.html
tags:
  - Configuration
  - Permissions
---

There have been many questions on the ReadyNAS forum regarding how to setup file sharing permissions when running a NAS with User security mode.

![Lock Icon][]

I have written a short overview, below, of the key share access & permissions settings available in Frontview when setting up a share & what they do, the misunderstanding of which is commonly the reason users have permission related issues.

All of the examples posted relate to CIFS access, but the settings apply equally to AFP and FTP access.

This information was originally posted [here][original post] in response to one of the many such queries on the ReadyNAS forum.

##  Share Access Restrictions

The first options visible when configuring share settings are the "Share Access Restrictions" as shown here:

![CIFS Advanced Access Restrictions][]

It is often overlooked, but as the dialog states this only controls whether a user or host can, or cannot, access the share. It does NOT control the [permissions][permissions wiki] of any files or folders created within the share.

Using this dialog is the easiest way to grant or deny user access to a specific share. For example, a common technique is to set the share default access rights to Read-Only so that any user with an account on the NAS can read the data in the share, but to then add the names of individual users to the "Write-enabled users" section such that those specific users also have full read-write capability. Using the method does not require groups or other permissions to be specified.

##  Advanced Permissions

Once a user has been granted write access to a share as controlled by the above settings, by default the permissions of files and folders created by the user within the share are set to only be writable by the owner/creator, but readable by all users with access to the share. This can be changed via the settings that appear below "Share Access Restrictions" - for example:

![CIFS Advanced Permissions][]

Note this is the section of the share setup that actually controls the permissions of files and folders created within the share. The Group that is referred to in "Group Rights" (above) is the primary group of the owner of the file which is typically set when creating the user account:

![User Config][]

The above information can be accessed, and the Primary Group set/changed, in Frontview » Security » User & Group Accounts

## Fixing Permissions

Any changes made to the Advanced Permissions dialog will only affect files & folders created after the change has been made. This may mean that there is existing data in a share that has inappropriate permission settings. This can be rectified via the "Advanced Options" tab.

In the dialog box that appears when selecting that tab (see below) ensure the group and everyone rights are set to read/write and check the option "Set ownership and permission for existing files and folders..." Click apply and wait for the dialog to state all is fixed.

![Advanced Share Permissions][]

##  Notes

* Once fixed, the option "Set ownership and permission for existing files and folders..." will be unchecked - this is normal.
* The folder owner and group settings shown are the defaults, but largely irrelevant if "everyone rights" are being set to Read/Write as shown in the example
* The folder group  only specifies the primary group of the share which can have implications for share access. It does not determine the group of  the files and folders stored within the share unless the "Set ownership and permission for existing files and folders..." is set & applied

##  More Comprehensive Guide

The above explanation provides a basic overview of how ReadyNAS access and permissions are controlled. For a more comprehensive explanation, forum contributor [bert386][] wrote a guide on this which is available here:

* [How to Setup ReadyNAS Permissions Manual][]

Some notes about the guide:

* I emphasise that I did not write it, nor do I have access to the original editable document. Therefore I cannot correct any errors or inaccuracies in the guide which is hosted here purely as a convenience for the many users that have found it useful.
* The guide refers to a "Share Security Mode" - this is only supported on earlier Sparc based ReadyNAS and so all x86 ReadyNAS users (eg Ultra, Pro, NVX users) can ignore these references as those NAS only support User security mode.
  * Pro models do support Active Directory Integration also, but that is different topic entirely and beyond the scope of this post
* To those Sparc-based ReadyNAS users who do switch from Share Security Mode to User Security Mode as recommended in the guide, a more convenient way to do this is [described here][security mode post]

### Even more details...

If you need to get into the real low level nitty-gritty of how ReadyNAS Access and Permissions work, a detailed overview of how permissions are implemented in ReadyNAS devices, see [this post][permissions overview post]

[original post]: https://www.readynas.com/forum/viewtopic.php?f=23&t=52358 "Original Forum Post"
[bert386]: http://www.readynas.com/forum/viewtopic.php?f=23&t=33014&start=15#p197753 "Bert386"

[permissions wiki]: https://en.wikipedia.org/wiki/Filesystem_permissions "Wikipedia: Filesystem Permissions"

[security mode post]: ../how-to-migrate-to-user-security-mode "Migrate to User Security Mode"
[permissions overview post]: ../overview-of-readynas-permissions "ReadyNAS Permissions Overview"
[How to Setup ReadyNAS Permissions Manual]: ../HowToSetupReadyNASPermissions "Permissions Guide"

[Lock Icon]: /assets/images/readynas/lock-icon.png
{: .align-right}

[CIFS Advanced Access Restrictions]: /assets/images/readynas/CIFSShareAccessRestrictions.JPG
[CIFS Advanced Permissions]: /assets/images/readynas/AdvancedCIFSPermissions.JPG
[Advanced Share Permissions]: /assets/images/readynas/AdvancedSharePermissions.JPG
[User Config]: /assets/images/readynas/UserConfig.JPG
{: .align-center}


