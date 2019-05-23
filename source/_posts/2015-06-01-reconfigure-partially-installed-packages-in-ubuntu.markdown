---
layout: post
title: "reconfigure partially installed packages in ubuntu"
date: 2015-06-01 13:22:30 +0800
comments: true
categories: Linux&Mac
---
When I try to upgrade my ubuntu version from 14.04 to 14.10, the system rebooted during the upgrade. When I try to login to the gnu desktop, it goes back to the login screen again and again.

So I have to login in using the "tty" terminal by "ctrl+alt+F3", and then issue the following command:

```bash
sudo dpkg --configure -a
```

There maybe something wrong logging in using the mosted updated kernal, so we can choose to log in using an previous version of kernal(provided if is not removed yet]).

Then if we still want to upgrade, we can do it when we successfully log in to the system.


