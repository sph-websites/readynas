---
title: Enabling Admin access to the C Volume over AFP
date: 2010-10-20
toc: false
tags:
  - Configuration
  - Security
---

The ReadyNAS firmware has long enabled the admin user to connect to the NAS via CIFS and be able to see the root data volume. For those not familiar, when the admin user connects to the NAS s/he will see all shares plus an additional share called "c" - this is the data volume on the NAS that contains all shares.

One of the key benefits to this is it allows the admin use to directly move data between shares - the data does not travel via the client PC or Mac - and so moves are virtually instantaneous, allow admin to reorganise data quickly & easily.

This is a great feature, but what about those operating in Mac only environment where CIFS is not enabled?

There is a fix, though it requires SSH access to your NAS. Simply add the following line to the file `/etc/netatalk/AppleVolumes.system`:

```shell
"/c" "c" cnidscheme:dbd forceuid:root allow:admin
```

Voilà! admin can now connect to you NAS over AFP and has full access to the root of the data volume, just like CIFS users

**Note:** This change will not survive a firmware upgrade, and so must be made again after the upgrade.
