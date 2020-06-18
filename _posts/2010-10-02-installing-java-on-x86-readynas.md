---
title: Installing Java on x86 ReadyNAS
date: 2010-10-02
tags:
  - Applications
---

Here's a step by step guide to installing Java from the official Debian Etch repository.

## Java 5

Step 1) Add the non-free repository to `/etc/apt/sources.list`

```shell
deb http://archive.debian.org/debian etch non-free
```

Step 2) Run `apt-get update`

Step 3) Before installing java, we need to make a small update: Sun (Oracle) force you to accept a license when installing Java, but there is no way to do this when installing via apt-get, which causes the install to fail. So we need to setup the acceptance beforehand. To do this create a text file with the contents:

```shell
sun-java5-jdk shared/accepted-sun-dlj-v1-1 select true
sun-java5-jre shared/accepted-sun-dlj-v1-1 select true
sun-java6-jdk shared/accepted-sun-dlj-v1-1 select true
sun-java6-jre shared/accepted-sun-dlj-v1-1 select true
```

Then run:

```shell
/usr/bin/debconf-set-selections
```

Step 4) Install

```shell
apt-get install sun-java5-jre
```

## Java 6

Step 1) Add the following repository to the file `/etc/apt/sources.list`
```shell
deb http://archive.debian.org/debian-backports etch-backports main contrib non-free
```

Step 2) Update apt

```shell
apt-get update
```

Step 3) Install Java

```shell
apt-get install sun-java6-jre
```
