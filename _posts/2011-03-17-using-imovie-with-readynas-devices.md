---
title: Using iMovie with ReadyNAS Devices
date: 2011-03-17
tags:
  - Media
  - Applications
---

![iMovie][]

One key reason for my investing in a NAS was to host the large video files that are generated during video editing with applications iMovie and Final Cut Express.

While it is relatively easy to setup FCE to use network storage to host video clips (network storage is fully supported in Apple Pro Apps like Final Cut and Aperture), iMovie is another matter due to Apple constraining its consumer apps by requiring data to only be hosted on HFS+ formatted local disks or directly attached storage devices. (Done to reduce the support burden?)

Fortunately, there is a workaround that appears to work for both iMovie '09 and iMovie '11, though it requires AFP or NFS networking to be successful - CIFS seems to be supported less & less by Apple.

**_Note: See Bottom of post for latest updates due to Apple-made changes in Lion_**

In terminal enter the following:

`defaults write -app iMovie allowNV -bool true`

Once set, iMovie should allow AFP & NFS mounted volumes to be used just like direct attached devices such as USB disks.

For example, using iMovie '11 here is what I see:

* Aperture = iSCSI disk (supported due to HFS+ formatting)
* HomeMovies = AFP mounted volume
* homenas = NFS mounted volume
* media = CIFS mounted volume

As can be seen, the CIFS volume (media) has a small exclamation mark next to it which indicates it is not available to iMovie, whereas the local disk, iSCSI, AFP and NFS volumes are now all fully available.

Remember also that OSX 10.6 can mount a sub-folder of a share as a separate volume, so it is fully possible to store iMovie events & projects within sub-folders of a share rather than the root of a share. For example, in the setup above, "HomeMovies" is in fact a sub-folder of the "media" share mounted over AFP such that all my media is hosted on a single share which makes it easier to manage files in finder (ie no unnecessary transfers over the network as all media data is in the same share)

### Edit (31/03/11):

Argh!!! Apple have changed how they mount subfolders in OSX 10.6.7 back to the way it worked in 10.5.x. See: [http://support.apple.com/kb/HT4538](http://support.apple.com/kb/HT4538)

But check out [this post][Admin over AFP] - same method can be used to workaround this

### Update (09/11):

It appears that Apple has now completely disabled the use of Network Volumes with the release of OS X Lion. This is true for both iMovie and the recently released Final Cut Pro X. Unless you're willing to go to the expense of XSAN (not an option with ReadyNAS devices) then it appears iSCSI is the sole remaining technology that will allow Mac users to work directly with network storage.

### Update (10/11):

So it appears there are still work arounds that can be used:

For iMovie - creating symbolic links to Event and Project folders stored on network volumes still seems to work, though not for Final Cut Pro X

For Final Cut Pro X - [See here][Final Cut Pro]

[iMovie]: {% link /assets/images/readynas/imovie.png %}
{: .align-right}

[Admin over AFP]: {% link _posts/2010-10-20-enabling-admin-access-to-the-c-volume-over-afp.md %} "Admin Access over AFP"

[Final Cut Pro]: {% link _posts/2011-10-18-using-final-cut-pro-x-with-readynas.md %} "Final Cut Pro X"
