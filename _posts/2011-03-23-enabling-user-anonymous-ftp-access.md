---
title: Enabling User & Anonymous FTP Access
date: 2011-03-23
---

Anonymous FTP access is a useful way to allow people access to download files from your NAS via a web browser without having to setup user accounts or figure out WebDAV.

Here's how to enable anonymous FTP access to your ReadyNAS, while still retaining User Authentication Mode for the data you still wish to protect access to

![FTP Authentication Mode][]

## Background to Access Modes

When configuring the ReadyNAS FTP service, a user is given 2 authentication mode options: anonymous & user mode

In user mode, a user must login with a valid username & password and is then able to access only those shares that have been appropriately configured for FTP access.

In anonymous mode, a user can simply login with the user name 'anonymous' - no password is required, though an email address will be requested. Web browsers that support FTP (eg Internet Explorer, Firefox) tend to try to access ftp sites anonymously in this way by default, before prompting for a username & password if access is not possible. Again access will only be available to the shares appropriately configured.

If however, when using anonymous mode,  the user does provide a valid user name and password, the default configuration of the ReadyNAS FTP server simply prevents the user logging in - ie anonymous and user authentication modes are mutually exclusive - which can be counter intuitive and not always the desired behaviour. Fortunately this behaviour can be changed.

## Enabling User & Anonymous Access

Via SSH access to your NAS, this combined user / anonymous authentication mode can be configured as follows:

1. Configure the FTP server for User Authentication mode in Frontview » Services » Standard File Services » FTP
2. Ensure that User mode is working as expected by connecting to the FTP server
3. Via SSH, edit the file `/etc/proftpd.conf` to add the following line at the end of the file:<br />`  Include /etc/frontview/proftpd/Anonymous.conf`
4. Restart the FTP server with the following command<br />`  /etc/init.d/proftpd restart`
5. Connect to the FTP server as the user 'anonymous' and verify access

## Notes

* This change will be overwritten if you make any changes to the NAS setup in Frontview » Services » Standard File Services. Also, a firmware update may overwrite the change. However, having the default authentication mode set to User means that this should not present any security issue - overwriting the change will simply prevent anonymous access which can be re-enabled as above.
* Opening up anonymous access, while convenient, can be a security risk - make sure you test that no shares are inadvertently exposed due to inappropriate configuration in Frontview
* Users who have enabled user SSH access to the NAS by providing a valid shell in `/etc/passwd` will see different behaviour when using the standard anonymous authentication mode:
  * User access is then allowed, however any logged in user other than anonymous will have access to the entire NAS file system rather than being sandboxed to only access the Frontview configured shares.
  * This is because the default ReadyNAS anonymous FTP server configuration assumes user shell access is not enabled and relies on this to prevent user access rather than configuring the FTP server to prevent user access.
  * The above modification is one method that may be used to resolve this.

[FTP Authentication Mode]: /assets/images/readynas/ftpauthenticationmode.jpg "FTP Authentication Mode"
{: .sph_img_ctr}

