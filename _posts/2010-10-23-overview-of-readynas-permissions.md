---
title: Overview of ReadyNAS Permissions
date: 2010-10-23
tags:
  - Permissions
---

![NV+][] Setting up share & file permissions on ReadyNAS devices can generate a substantial number of questions and problems. In most cases, these questions & problems are due to either a lack of understanding by the user of how permissions are designed to work, or a user having incorrect expectations of how permissions work - particularly when more familiar with Windows systems.

This post aims to provide a simplified overview of how permissions work on ReadyNAS devices and what must be considered when configuring them.

**Some notes before we start:**

1. The ReadyNAS Frontview interface is restrictive in the control of permissions it allows vs. what is possible through the underlying Linux OS. (I expect this may be an attempt by Netgear to simply control). Therefore this post describes only what is possible via Frontview. "Power users" looking to hack their permissions via SSH - this post is not for you.

2. This is not intended to be a guide of how to setup permissions for any arbitrary need. For that, check out the "[How to setup ReadyNAS Permissions][]" guide by bert386 from the ReadyNAS forums.

3. I shall focus on CIFS, AFP and FTP protocols as these are the most popular methods of ReadyNAS access. HTTP access will be discussed briefly, but is not the focus of this post

4. I do not consider Access Control Lists (ACLs), a further permissions refinement available via CIFS. Such permissions are primarily used in Windows Domain setups and so beyond the scope of this post.

##  Advanced Share Permissions (Already?)

All ReadyNAS devices run Linux. Therefore, the fundamental permissions system used by the devices are Linux permissions as controlled by the underlying OS. User access via CIFS, AFP, FTP and HTTP is then granted by special services running on the ReadyNAS that also provide an additional level of permission control, but always subject to the underlying Linux permissions system. So while it might seem backwards, it is useful to first have an understanding of the "Advanced Share Permissions" options that are available for each share which reflect those basic Linux permissions. As we'll find, these "Advanced" options are anything but - rather they are the basic settings that need to first be setup correctly to ensure proper permissions based access

The following tab can be accessed in Frontview by going to Frontview » Shares » Share Listing, and selecting a protocol (eg AFP or CIFS) for the share concerned. Then selecting the "Advanced Options" tab in the sub-window that appears:

![Advanced Share Permissions][]

Each Share has 3 sets of permissions: Owner, Group & Everyone. These work as follows:

**Owner:** As the name suggests, this user owns the share. As a consequence that user gets certain additional privileges related to data contained within the share in addition to full read/write access always being enabled. As a consequence I would recommend that the share owner always be set to the admin user unless you have specific reason not to. Note that while this user owns the share, s/he does not own the files or folders within the share, and so may have limited access to files created in the share by other users. This will be highlighted later.

(As an aside, it is interesting to note that Frontview does NOT assign the admin user as the default share owner due to legacy issues related to the "share mode" security mechanism supported on older Sparc based NAS. However, factory default your x86 based NAS and the 2 default shares - media & backup - will be owned by admin. )

**Group:** All users are members of a primary group and by default, on ReadyNAS devices, all users are made primary members of the group "users". Groups are useful in managing permissions of files that will be accessed by a subset of users. If the user accessing the share is not the owner and is not a member of the specified group, then access will be denied (unless over-ridden by the Everyone" permissions - see next section on 'Everyone' share permissions)

Group permissions can be set as:

* None - ie only the owner can access the share
* Read Only - group members can view the shared content, but not make changes
* Read / Write - group members have full access

By default, Frontview sets "nogroup" as the group, and Read/Write as the permissions. "nogroup" is a special group used by the ReadyNAS and which only has the guest user as a primary user. In effect, this disables the group permissions functionality of the share for everyone except the guest user, which is not usually the desired setting.

I would recommend that the group setting should be set to the primary group of the users accessing the share - in most cases this would be "users" - with Read/Write access, as this allows easier group based administration of the share. Doing this however means that care must be taken when granting guest access - again see the next section on 'Everyone' share permissions

Additional groups can be setup in Frontview at: Frontview » Security » User & Group Accounts

**Everyone:** These permissions control if the share can be accessed by a user that neither owns the share nor is a member of the share group (ie the default configuration of any new share). The available options are again  None, Read Only or Read/Write.

By default, Frontview sets the share Everyone permissions to Read/Write which helps avoid many permissions related issues in granting access to the share, in particular the granting of guest access as mentioned previously.

As the default owner & group settings do not enable user access to a share, this default setting  should not be changed without a proper understanding of the consequences and having setup the group & owner permissions first. It should not just assumed that granting Everyone "Read/Write" access to be a security risk that should be closed by setting to "None". In most practical cases, users accessing shares via CIFS or AFP should set the Everyone permissions to "Read/Write" and then use the protocol related share permissions settings to finely control share access. (See ['Controlling Share Access'](#controlling-share-access-per-protocol) later in this post)

##  Granting Rename & Delete Privileges

The Advanced Share Options tab also offers the following:

![Advanced Share Options][]

By default the option "Grant rename and delete privileges to non-owner of files" is enabled.  When enabled, the ability to rename or delete files is dictated by a users write permissions of the parent folder (not the write permissions of the actual file which controls if a file can be modified). Therefore if the share or a folder is accessible as read/write then all files within that folder can be deleted or renamed. If this option is disabled however, only the superuser (see section below on 'admin' user)  or the owner of the share or folder containing the file can delete & rename files and folders that they do not own, though if a file has appropriate write permissions it can still be modified.

Having this option disabled is one of the most frequent reasons for users having difficulties with permissions - while it is enabled by default for new shares, the media & backup shares created during a factory default have this option disabled which many users understandably overlook.

(For Linux users - this latter option controls the 'sticky' bit)

In the above dialog is also the option "Set ownership and permission for existing files and folders..." - this option will revert the permissions of all files and folders in the share to those defined in the upper part of the dialog. To use it, check the box and then press apply and Frontview will update the files/folders in the share - which can take time for large datasets. Note that once the operation is complete the checkbox will no longer be checked - it is not "sticky" as it is there simply to enable a one time operation. Use this option with care as while it can help fix a multitude of permissions problems, it can also create problems if the new permissions are inappropriate.

##  File & Folder Permissions

The previous section described permissions related to the share. Permissions of files and folders within a share are set at the time of the creation of the file/folder. (Here "file creation" means both creating a new file in a share, but also copying files to a share)

Like a share, there are 3 sets of permission assigned to a file/folder: Owner, Group & Everyone, in exactly the same way as the permissions are assigned to a share - not surprising as a Share is in reality a folder on the ReadyNAS device but is special in that it can be mounted over a network.

**Owner:** The user creating the file is always assigned as the owner and granted full Read/Write access to the file.

**Group:** The group of the file will be the primary group to which the user is assigned in Frontview » Security » User & Group Accounts and **not** the group to which the share belongs

Note: This behaviour can be changed such that the share group is always the assigned group of files/folders within the share, which in my experience is an extremely useful capability that facilitates easier file sharing amongst a group of users. However this is an advanced topic that would require SSH access to your NAS to implement and will be covered in a separate post. (Linux users - this refers to controlling the SGID bit)

**Everyone:** This will define if users who are not members of the group to which the file/folder is assigned will have Read and/or Write access. The default Everyone setting is Read-Only. (Note this is not the same as default Everyone permissions for the Share, which is Read/Write)

##  Consequences of Default Permission Settings

There are a number of issues that can arise when using the default permissions setup.

First, it is important to note there is a difference between the default Everyone permission settings for files/folders, and the default Everyone permissions for shares.When a user accesses a share based on the Everyone permissions (ie the user is neither the owner of the share, nor a member of the share group), because the share has Read/Write permissions for everyone, this means that the user can delete and rename files that do not belong to them that exist in the root of the share. However, in sub-folders of the same share, where the default Everyone permissions is Read Only, such renames and deletions are not permitted, though those files may be modified if the file write permissions are appropriate.

The second common issue relates to the admin user, guest user and standard users all being primary members of different groups as follows:

* The admin user is a primary member of the group 'admin'
* The guest user is a primary member of the group "nogroup"
* Other users have the group "users" assigned as their primary group (by default)

This means that for a default configuration:

* Files created by the admin user will be Read Only to standard and guest users
* Files created by standard users will be Read Only to guest users
* Files created by guest users will be Read Only to standard users

(Note that the admin user should always be able to access any file, however be careful using the admin user to make edits and work around a permissions issue as the file or folder may then be owned by the admin user making it inaccessible to standard and/or guest users.)

The above is a little counter-intuitive in practice as it doesn't quite follow the hierarchy of access permissions a user often expects where:

* The admin user has global Read/Write access to all files
* Standard users have Read/Write access to their own files & guest created files.
* Guest users can only modify their own files and view others in the share

This is particularly troublesome for new users who, during the setup of their ReadyNAS, may frequently switch between the admin, guest and a regular user account due to lack of familiarity, often without even realising it, and then get into trouble when they cannot edit files that they know they edited previously apparently without issue.

##  Controlling Share Access (per protocol)

CIFS, AFP and FTP access allow a user to more carefully refine share access permissions than what is possible in "Advanced Share Permissions". The following settings can be accessed by selecting the relevant protocol for a specific share at: Frontview » Shares » Share Listing:

![Share Access Control][]

Note that these controls do not over-ride the basic share access permissions previously described and setup in "Advanced Share Permissions", but are used to further restrict access, which is of course the fundamental aim of permissions.

This means that controlling guest and group access for the protocol requires that the guest user or the group concerned already has access enabled via the settings previously described in "Advanced Share Permissions" - usually be enabling Ready/Write access for Everyone. Otherwise, the following scenarios become common:


* If, in Advanced Share Permissions, the Group of the share is defined as "users" (as recommended) and Everyone access is restricted to "None", then guest access will fail when enabled in the above protocol settings. This is because the guest user is only a member of the group "nogroup" so cannot create or read folders that do not also belong to the "nogroup" group . To fix this either:
  * The share group must be changed to "nogroup" (the default set by Frontview),
  * The guest user (actually called "nobody") must be added to the share group (not recommended), or
  * Everyone access must be set to Read Only or Read/Write, as appropriate.
* Similarly, if a group of users is defined, and those users are not also members of the same group that owns the share, access to the share can only be granted in the above dialog if the Everyone permissions are set to Read Only or Read/Write in "Advanced Share Permissions"

It should be apparent that there is a close interaction between the protocol related permission options and the "Advanced Share Permissions" of the share - and it is the interaction of these through misconfiguration that typically leads to problems as conflicts. These conflicts will only be apparent when a user tries to access files in a share, not during the configuration process, as there is no error checking for such conflicts within Frontview.

##  Controlling File/Folder Permissions (per protocol)

The default settings of Group & Everyone permissions for files/folders created in a share are both set as Read Only. This can be over-ridden on a per protocol basis by selecting the relevant protocol for a specific share at: Frontview » Shares » Share Listing

Group and Everyone access is then controlled by additional options such as the following AFP settings:

![Advanced AFP Settings][]

By enabling the Advanced Permission options, default Group & Everyone rights can be individually set to None, Read Only (the default) or Read/Write and so facilitate sharing.

Note: CIFs offers the additional control of being able to specify Group / Everyone permissions separately for Files vs Folders.

For FTP users, there are no settings within Frontview to control the default permissions as there are for CIFS and AFP. This is instead typically controlled within the FTP client. If the client you are using does not provide options to change permissions and/or set default permissions - change your client

##  Private Home Shares

If enabled, each user account is assigned a 'home share' - a private share named after the user and to which only the user, as the owner, has access - both group and everyone permissions are completely disabled. There is no mechanism provided in Frontview to change this behaviour, nor to fix permissions on files that may be inaccessible. This latter point is understandable as if only the owner can access the share, there should never be the possibility that permissions of the share contents be incorrect. Unfortunately this assumption regarding access is incorrect, as will be covered in the next section

##  The "admin" User and the Administrative Shares

All ReadyNAS devices feature a special user account called 'admin'. That account is granted superuser privileges when accessing a ReadyNAS device via AFP or CIFS - which means 'admin' will have unrestricted access to files and folders irrespective of any permissions settings. Frontview allows the 'admin' user to access all private home shares via AFP & CIFS via a special admin-only share called "home". In addition, CIFS provides access to an additional "c" share that includes all other shares. (Note: the same can be achieved via AFP as documented [here][Admin Over AFP].

This can be a useful administrative option, but as the  'admin' user is a member of a different group than all standard users, any files created or modified by the admin user will become inaccessible to standard users. The lack of any mechanism in Frontview to fix home share permissions in particular means such a scenario can only be corrected by accessing the underlying OS via SSH. This is because Frontview does not provide support for controlling the default permissions of files when accessed via these administrative shares, and so the default group (set to "admin") and everyone permissions of Ready Only will be used.

It is therefore strongly recommended to NEVER modify or create files in the administration "home" or "c" shares when connected as 'admin' - better still, do not even access these shares as 'admin' unless absolutely necessary.

##  A note about HTTP/HTTPS access

When connecting via CIFS to a share as the user 'admin', (or AFP if you are leveraging [this tip][Admin Over AFP] the previously mentioned permissions are pretty much ignored and the user has full read/write access to all files. This is because despite connecting as the user 'admin', data is actually manipulated as the user 'root' which is a [specially privileged user on Unix/Linux based systems](http://en.wikipedia.org/wiki/Root_user). The admin user is however a member of the group 'admin' and so care should be taken when modifying or creating files & folders while connected as the admin user: such files will be owned by 'root', assigned to the group 'admin', and therefore standard users cannot access such files unless the everyone permissions are set.

Unfortunately this adds a complication: ReadyNAS devices actually run applications as the admin user - notably the Apache webserver that provides HTTP, HTTPS & WebDAV access to shares. When accessing files via HTTP, HTTPS, and/or WebDAV,  irrespective of which account is used to login to the ReadyNAS, all files are accessed on the as the user 'admin'. Note we are referring here to the real admin user account of the underlying Linux OS, not the superuser (root) that is used when logging into a ReadyNAS device via CIFS or AFP as the admin user (Yeah - it's like the admin account is schizophrenic! One set of permissions when accessing the ReadyNAS via HTTP, another when accessing via CIFS or AFP).

This means that the webserver, running as admin can, by default, only access files that either:

* are owned by admin
* belong to the admin group
* have everyone permissions set to Read Only or Read/Write

If permissions are not set appropriately for Everyone, then the admin account (as used by the webserver) can access neither standard user created files, nor those created by the guest user. This is also true if you connect via FTP as the user 'admin'.

Fortunately access by admin can be fixed in the main part by adding 'admin' as a member of the same group(s) to which users belong - typically "users" - in Frontview » Security » User & Group Accounts.

**Note** that for files created by the admin user via HTTP/S, the webserver is configured to ensure the "Everyone" permissions are always set to "Read/Write".

##  Summary

The primary aim of permissions is to restrict access to information. With this in mind it is important to ensure that the initial basic permissions - as set in the perhaps incongruously named "Advanced Share Permissions" tab - are appropriate and not overly restrictive as these govern all access to data within a share and cannot be over-ridden.

Particular attention should be paid to the Everyone settings and it should not be assumed that these should be set to "None" as some form of Security precaution. Note also that the default settings as established by Frontview are often not appropriate for many users - and even inconsistent - and should be reviewed based on specific needs.

Once the share permissions are setup, share access can then be further restricted on per protocol basis. Again, attention must be paid to Group membership and Group & Everyone permissions should the goal be to allow files to be shared between users, or if guest access to the share is to be allowed.

Finally, if you intend to access files via HTTP/S or WebDAV, it is recommended that you add 'admin' as a member of each group of users to help avoid permissions issues

[NV+]: /assets/images/readynas/netgear-readynas-rnd4425.png
{: .align-right}

[How to setup ReadyNAS Permissions]: {% link _posts/2010-09-02-HowToSetupReadyNASPermissions.md %} "ReadyNAS Permissions Guide"
[Admin Over AFP]: {% link _posts/2010-10-20-enabling-admin-access-to-the-c-volume-over-afp.md %} "Admin Access over AFP"

[Advanced Share Permissions]: {% link /assets/images/readynas/Screen-shot-2010-10-19-at-11.09.29.jpg %}
[Advanced Share Options]: {% link /assets/images/readynas/Screen-shot-2010-10-19-at-11.41.37.jpg %}
[Share Access Control]: {% link /assets/images/readynas/Screen-shot-2010-10-19-at-12.30.42.jpg %}
[Advanced AFP Settings]: {% link /assets/images/readynas/Screen-shot-2010-10-19-at-12.45.55.jpg %}

