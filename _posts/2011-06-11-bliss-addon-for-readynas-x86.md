---
title: Bliss Addon for ReadyNAS (x86)
date: 2011-06-11
toc: false
tags:
  - Media
  - Applications
---

**Warning:** The addon described in this post no longer exists
{: .notice--warning .text-center}

When first purchasing a ReadyNAS, my only real thought was to have a centalised backup for an every growing library of documents & media, and a facility to make backing those files up easy. But owning a ReadyNAS device introduced me to the idea of actively streaming audio from a central library to multiple clients. My audio library is now available on any of our computers at home, via our [Plex][] based media center, multiple [Squeezebox][] audio players, iOS devices and even remotely via the excellent [Subsonic][] application.

The ubiquitous access to our audio however soon revealed one limitation: the high resolution screens of some of the devices being used (eg iPad) clearly showed that the artwork associated with my audio library was pretty poor quality, incorrect, incompatible with some applications but not others, or just non-existent. In short - the audio artwork of out music library was a mess.

While I found that there are a number of applications around that puport to help with artwork issues, most seem to focus on tagging rather than artwork, with artwork being just another tag. Also as all of my media was stored on my NAS, streamed from it and managed there, I much preferred to have an artwork management application that would also run from the ReadyNAS rather than run separately with an OS specific frontend .

That's when I found [Bliss][]

## Background

[![Bliss Screenshot 1][]][Bliss Screenshot 1 Image]
Bliss is a java application that can run under Windows, OSX and Linux with an interface that is is web based and so accessible from any OS. It seemed ideal for running on a ReadyNAS and so it has proved - correcting and embedding artwork into all of my audio files with minimal effort on my part, be they MP3, FLAC, ALAC, AAC or even the odd Windows Media files I have hanging around. Better still - the artwork quality is easily controllable; I choose to only allow artwork of 500x500 pixel resolution or greater to be used which looks great on my iPad, in Subsonic or Plex and means there's a good selection of artwork to choose from.

[![Bliss Screenshot 2][]][Bliss Screenshot 2 Image]
The interface to bliss is very simple. Bliss scans your audio library to provide a view of all of your albums in alphabetical order together with the current artwork (See image above). Click on the album and bliss presents you with the option to change the artwork providing suggested artwork from various internet resources such as Google or Amazon. Changing the artwork includes the option to embed it into the audio files as well as copying the artwork file to the relevant folder containing the audio files (See image to right).

And while focused primarily on artwork, bliss is not just limited to fixing artwork - Genre, year and naming of files can also be fixed. Better still, the application is under very active development with a lot of new capabilities coming.

There are a number of more complete reviews of bliss - links to which can be found [here](https://www.blisshq.com/testimonials.html). But I've been so impressed with the application that I decided to take the step of developing an addon for ReadyNAS devices so that bliss can easily be installed and setup without a user having to manually setup the application via command line. Here's how to get the addon installed an bliss running on your ReadyNAS

## Installation & Usage

The addon can be downloaded from the [ReadyNAS forum](https://www.readynas.com/forum/viewtopic.php?f=48&t=53986)

<!-- or from here: [`https://www.sphardy.com/web/bliss/bliss_addon_latest`](/web/bliss/bliss_addon_latest) -->

Installation is as for any ReadyNAS addon via Frontview. The addon will download the latest publicly available version of bliss directly from the [https://www.blisshq.com](https://www.blisshq.com/) website during installation. (The version installed will be displayed in the Frontview Configuration panel). Once the addon is installed, note that it does not immediately launch the bliss application. This is because the addon first requires a configuration setting.

As bliss will download new artwork to the NAS, and potentially embed artwork into the audio files, it requires full write access to those audio files. To enable this and ensure appropriate file access and ownership is maintained the addon requires that a user account be defined which has write access to those files/folders. This needs to be entered in the dialog box and confirmed by pressing the "Change" button. Once the user has been defined the application can be started by checking the enable box and pressing "Save".

Note: If a user name is entered that does not exist, the addon will not start.

<!-- Commented out as images are lost

[caption id="attachment_716" align="alignnone" width="150" caption="Upload in Frontview"][![](https://www.sphardy.com/web/readynas/files/2011/06/Screen-shot-2011-06-02-at-3.10.19-PM-300x202.jpg)](https://www.sphardy.com/web/readynas/files/2011/06/Screen-shot-2011-06-02-at-3.10.19-PM.jpg)[/caption]
»

[caption id="attachment_717" align="alignnone" width="150" caption="Confirm the Installation"][![](https://www.sphardy.com/web/readynas/files/2011/06/Screen-shot-2011-06-02-at-3.11.00-PM-300x201.jpg)](https://www.sphardy.com/web/readynas/files/2011/06/Screen-shot-2011-06-02-at-3.11.00-PM.jpg)[/caption]
»

[caption id="attachment_768" align="alignnone" width="150" caption="Bliss Fully Installed"][![](https://www.sphardy.com/web/readynas/files/2011/06/Screen-shot-2011-06-11-at-3.08.14-PM-300x201.jpg)](https://www.blogger.com/web/readynas/files/2011/06/Screen-shot-2011-06-11-at-3.08.14-PM.jpg)[/caption]

[![](https://www.sphardy.com/web/readynas/files/2011/06/Screen-shot-2011-06-11-at-10.57.18-AM-300x156.jpg)](https://www.sphardy.com/web/readynas/files/2011/06/Screen-shot-2011-06-11-at-10.57.18-AM.jpg)
-->

The addon will download the latest publicly available version of bliss directly from the [https://www.blisshq.com](https://www.blisshq.com/) website during installation. (The version installed will be displayed in the Frontview Configuration panel). Once the addon is installed, note that it does not immediately launch the bliss application. This is because the addon first requires a configuration setting.

As bliss will download new artwork to the NAS, and potentially embed artwork into the audio files, it requires full write access to those audio files. To enable this and ensure appropriate file access and ownership is maintained the addon requires that a user account be defined which has write access to those files/folders. This needs to be entered in the dialog box and confirmed by pressing the "Change" button. Once the user has been defined the application can be started by checking the enable box and pressing "Save".

Note: If a user name is entered that does not exist, the addon will not start.

<!--
[caption id="attachment_723" align="alignleft" width="266" caption="Launch Bliss"][![](https://www.sphardy.com/web/readynas/files/2011/06/Screen-shot-2011-06-02-at-3.16.05-PM-266x300.jpg)](https://www.sphardy.com/web/readynas/files/2011/06/Screen-shot-2011-06-02-at-3.16.05-PM.jpg)[/caption]
-->

Once the addon is enabled and running, it can be access by pressing the "Launch Bliss..." button, or loading `http://<nas_ip_address>:3220` in your web browser

On first launching bliss, initial settings such as location of audio files & artwork requirements must be defined, full details of which can be found [here.](https://www.blisshq.com/support/tutorials/first-steps.html)

Bliss will then scan your media, presenting each album with its current artwork and an assessment of whether that artwork meets the requirements you defined when setting bliss up in the previous step. For those items that are not compliant, click on the edit icon and bliss will search the likes of Amazon, Google and MusizBrainz for relevant artwork that can be used instead - both embedding it in the audio files as well as downloading the image file to the folder contaning the album

And that is pretty much it.

To those who give bliss a go, I hope you find it as useful as I have.

**Note:** As the title of this post hopefully makes clear, this addon is only available for x86 based ReadyNAS such as the Pro and Ultra series. Please don't ask for a Sparc version for NV+ and/or Duo - there will not be one as bliss is an x86 application only.

[Plex]:       https://www.plexapp.com/
[Squeezebox]: https://www.mysqueezebox.com/
[Subsonic]:   https://www.subsonic.org/
[Bliss]:      https://www.blisshq.com/

[Bliss Screenshot 1]: {% link /assets/images/readynas/Screen-shot-2011-06-11-at-2.55.06-PM_tn.jpg %}
{: .sph_img_left}

[Bliss Screenshot 1 Image]: {% link /assets/images/readynas/Screen-shot-2011-06-11-at-2.55.06-PM.jpg %}

[Bliss Screenshot 2]: {% link /assets/images/readynas/Screen-shot-2011-06-02-at-5.40.00-PM_tn.jpg %}
{: .sph_img_right}

[Bliss Screenshot 2 Image]: {% link /assets/images/readynas/Screen-shot-2011-06-02-at-5.40.00-PM.jpg %}
