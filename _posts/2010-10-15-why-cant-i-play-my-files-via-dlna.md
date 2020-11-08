---
title: Why can't I play my files via DLNA?
date: 2010-10-15
toc: false
tags:
  - Media
---

The [DLNA Organisation][] defines itself as follows:

> ![DLNA Logo] The digital home is an evolution of the idea that PCs, consumer electronics and mobile devices should work together seamlessly through a wired or wireless network to share digital content within a home environment. Digital Living Networking Alliance - DLNA - extends that idea to include sharing content on the go as well.
>
> <cite><a href="http://www.dlna.org/digital_living/faq/">DLNA Frequently Asked Questions</a></cite>

The aim is simple and admirable - create a mechanism whereby anyone can access any of their media on any of their devices - Computer, TV, Phone etc. - connected to a home network. Then ensure the success of that mechanism by certifying product compliance with the proposed mechanism.

Netgear has achieved DLNA certification for a number of their ReadyNAS products, providing the ability to stream media to client devices via their ReadyDLNA software included in their NAS firmware. ReadyDLNA simply streams media as-is using the DLNA specified methods - it doesn't modify it or transcode the media in any way, and will stream far more formats than specified by DLNA. (Not that you would know this without trying ReadyDLNA, because Netgear hasn't released any form of user guide for ReadyDLNA or even published the formats it supports)

But this level of support by ReadyDLNA is also the source of an all too common set of questions on the ReadyNAS Forums when trying to access media via ReadyDLNA:

* Why don't I see all of my media when accessing it via DLNA?
* Why doesn't my DLNA Certified client play my FLAC audio/MPEG4 AVC Video/[Insert format here] ?
* Why is it that my DLNA Certified client can play [insert format here] when accessed from a disc, or from a network share - but not via ReadyDLNA?
* Is the ReadyDLNA server broken?

According to the DLNA [Media Format and Transport Model][], support for the following formats are specified as required or optional to be able to achieve DLNA certification:

![Device Formats][]

![Media Formats][]

As you will see from the above, the formats specified - even including the optional formats - are fairly limited. No Matroska containers, no MP4 AVC (ie H.264) for "Home Devices" such as TVs and networked Blueray players etc. So achieving compliance clearly doesn't fulfil the "idea that PCs, consumer electronics and mobile devices should work together seamlessly through a wired or wireless network to share digital content"

But of course these tables are just what a manufacturer needs to support for DLNA compliance - there is of course no reason why a client manufacturer can't extend their DLNA capability with support for more formats than this right?

Yeah right... Great in theory - not so great in practice.

Many manufacturers (for example Microsoft, Sony, Western Digital to mention 3 I know of for sure), support far more audio & video standards in their products than those listed for DLNA compliance. But they only support many of these formats when accessing media either from a physical disc (eg USB drive or blueray disc), or via a network share - NOT when streaming media over DLNA.

I don't know for sure why they restrict their capabilities this way; I suspect it is related to how a DLNA server advertises the format of the media to the client, and some vendors not wishing to implement proprietary extensions to their DLNA products to support additional formats - but it's hard to be sure given the DLNA spec is only available to members. For sure, the limitation can't it be a constraint of DLNA Compliance as otherwise ReadyDLNA wouldn't support so many additional formats (eg FLAC and MKV) and so this must be a conscious decision by such manufacturers to restrict their products. If anyone knows better, PLEASE enlighten me.

Just be aware that if you have a DLNA Certified Client, and it can't play media via DLNA that possibly it can play by other means - now you know why & who to complain to before posting yet another "Why isn't ReadyDLNA working?" post

[DLNA Organisation]: https://dlna.org/

[Media Format and Transport Model]: http://www.dlna.org/industry/why_dlna/key_components/media_format/

[DLNA Logo]: {% link /assets/images/readynas/CERT_COLOR_R.gif %}
{: .align-right}

[Device Formats]: {% link /assets/images/readynas/DLNAHomeDeviceFormats.jpg %}
{: .align-center}

[Media Formats]: {% link /assets/images/readynas/DLNAMobileMediaFormats.jpg %}
{: .align-center}
