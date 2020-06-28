---
title: Migrating TimeMachine Backups to a ReadyNAS
date: 2011-06-01
toc: false
tags:
  - Backups
  - Applications
redirect_from:
  - /2011/06/migrating-timemachine-backups-to_1097.html
---

ReadyNAS devices can be used as a target for TimeMachine backups. However when users first set this facility up they also often want to migrate an existing backup from an external HDD attached to their mac to the ReadyNAS so that they maintain their backup history but free up the external HDD

Here's is one way to do this that is known to work based on [feedback from one user][] as well as success doing this myself.

![Time Machine][]

1. Enable the TM service on the ReadyNAS in Frontview

2. Configure the mac to backup to the ReadyNAS and allow a backup to start. This will cause the TM to create the required diskimage on the ReadyNAS that you will replace with the data from your USB disk

3. Allow the backup job to copy some data, but to save time stop the job after a short while (as we will be replacing the backup data there is no point allowing the job to complete)

4. Disconnect the mac from the AFP service and then reconnect over AFP to the NAS with the username "ReadyNAS" and the TM password you setup in step 1

5. You should then have access to a share called "ReadyNAS", in which there is a diskimage that will be named after your mac - this is the new backup target. Double click on it to mount the image

6. Start Disk Utility on your mac and then use the Restore function to copy the TimeMachine contents of the external HDD connected to the mac to the diskimage you just mounted - this will take a while.

7. Once complete, dismount the external drive and mounted diskimage, disconnect from the from the ReadyNAS AFP service, and then launch a TM job.

If all went well TM will mount the backup image which now has the same data as your external HDD and the TM job will incrementally add new backup data. Once verified, redeploy the external HDD

[feedback from one user]: https://www.readynas.com/forum/viewtopic.php?f=71&t=43835&p=247665#p247702 "User Feedback"

[Time Machine]: /assets/images/readynas/TimeMachine_tn.png "Apple TimeMachine"
{: .align-right}
