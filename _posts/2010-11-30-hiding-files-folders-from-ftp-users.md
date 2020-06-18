---
title: Hiding Files & Folders from FTP users
tagline: ""
date: 2010-11-30
toc: false
---

The ReadyNAS devices support a variety of protocols, a consequence of which is that shares may include a number of system folders that are only intended to be used to support certain protocols.

By default these files & folders are typically hidden when a ReadyNAS device is accessed via CIFS or AFP, but all of them show up when accessed via FTP which can at best be distracting and at worst downright confusing for users. It can also lead to issues if FTP users were to modify any of those folders for any reason.

Hiding these files & folders, and any others that you may wish, is fortunately easy to do on a share be share basis as follows:

1. In the root of the share create a file called `.ftpaccess`
2. Add the following setting to the file: `HideFiles (<regexp>)$`

Where `regexp` is a [Regular Expression][] matching the files & folders you wish to hide. For example:

`HideFiles (index\.html|Temporary.Items|Network.Trash.Folder)$`

**Notes:**

* This setting only hides the files/folders - it does not prevent user access
* While multiple 'HideFiles' settings can be added to the .ftpaccess file, and the FTP server will not generate an error or warning, it appears to only honour the first setting in the file.
* Be careful to configure the permissions of the .ftpaccess file appropriately to prevent other users editing or deleting it

[Regular Expression]: http://en.wikipedia.org/wiki/Regular_expression "Regular Expressions"
