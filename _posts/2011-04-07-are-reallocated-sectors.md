---
title: What are Reallocated Sectors?
date: 2011-04-07
---

Most ReadyNAS users have probably experienced it. Waking up, eventually checking email over a morning cup of coffee to find that overnight your NAS has sent you the friendly warning:

> Error message: Reallocated sector count has increased in the last day.
>
> Disk1: Previous count:0 Current count:4<br />
>
> **Growing SMART errors indicate a disk that may fail soon. If the errors continue to increase, you should be prepared to replace the disk**
{: .notice}

So after clearing out the coffee you just spluttered all over your keyboard,  what are Reallocated Sectors and, more importantly, what are you going to do about them?

![Disk Image][]
**Note:** ReadyNAS devices perform HDD SMART tests early each morning - so it is most common to get such a message in your morning inbox)
{: .notice--primary}
{% include sph/clear %}

## What are Reallocated Sectors?

The disks, or more correctly the platters, in a Hard Disk Drive (HDD) are of course circular - data is organised on each platter in a series of concentric circles called a track, with each track partitioned into multiple smaller units called sectors. By convention, each sector is able to store either 512 bytes or 4Kbytes of data.

In large drives there can be millions of such sectors and for a disk to fully function each one of those sectors must operate perfectly - in theory. As the capacity of disks increases, and thereby the sector count increases, the possibility of a drive having problematic sectors also increases.

HDD Manufacturers strive to ensure their drives are 'perfect' but in the real world where they are also try to drive costs down we have to accept the fact that this is an extremely difficult goal to achieve. Further, HDD users do not wish to find their data unexpectedly corrupted due to a 'bad sector' and have no recourse. Therefore HDD manufacturers introduced the technique of being able to "Reallocate" sectors.

When writing to a sector the HDD verifies that the data has been written successfully. If the verification fails, and perhaps after multiple retries, then the HDD considers that particular sector as 'bad' and so reallocates the data to another sector while keeping a record of the bad sector (ie a "Reallocated Sector") so that it will not be used in future. This method avoids user data being corrupted and means the disk continues to be fully operational despite a very minor flaw.

## Are Reallocated Sectors a Problem?

In themselves, reallocated sectors are a sign your HDD is properly protecting your data. Ideally we would hope to never see them, but in practice they are quite common.

Reallocated sectors really become a big deal when they start to increase rapidly or reach a very high count (eg thousands) - that tends to be an strong indicator of a disk that is about to fail. For example, a typical scenario is if the ReadyNAS reports a jump from 3 reallocated sectors to 103, and perhaps more the following day(s). (The ReadyNAS devices check for increased Reallocated Sectors once per day)

An increasing number or large count of reallocated sectors can also cause performance issues as the drive is repeatedly having to deal with these and perhaps finding new sectors that must be reallocated, so reduced performance in combination with an increased reallocated sector count may also be a strong indicator of pending failure.

## What to do about Reallocated Sectors?

In my experience it is not unusual to see a small number of reallocated sectors discovered in the early operating life of a disk. As the disk is used for the first time and starts to write to the various locations it often finds a small number of sectors that need reallocating. There is no specific number of reallocated sectors that is considered "bad" - different people have different opinions - and as described all disks can have millions of sectors, so 2, 4 or 8 reallocated sectors is hardly a big deal.

The number of reallocated sectors that should cause concern becomes a judgement call, though some of the diagnostic tools provided by HDD manufacturers have thresholds of when reallocated sectors should be considered a problem that can vary per disk type - so this is one way to check if the disk should be replaced.

Note: The [ReadyNAS FAQ](http://www.readynas.com/forum/faq.php#How_can_I_verify_that_my_disk_is_bad%3F) lists the various HDD diagnostic tools available

My personal rule of thumb in the absence of any HDD manufacturer guidelines or disk checks:

* Single digits? Ignore it - the disk is "bedding in"
* Less than 100? Don't worry about it too much but pay attention:
  * Hearing funny noises from the drive?
  * Has performance decreased?
  * Have a spare disk at the ready.
* More than 100 or see the number increase rapidly? Replace the drive
  * Note that the disk is still operating properly and so there is no need to remove the failing disk before a replacement is obtained & available to be hot-swapped.
  * Remember that 100 reallocated sectors is just a guideline; but it is common to see the number start to increase fairly rapidly once such a level is reached.

In summary, read the message sent by the ReadyNAS carefully and then make your own judgement call:

Growing SMART errors indicate a disk that **may fail soon**. If the errors continue to increase, you should **be prepared** to replace the disk.
{: .notice--primary}

[Disk Image]: /assets/images/readynas/hard-disk9_tn.gif "Hard Disk Design"
{: .align-right}
