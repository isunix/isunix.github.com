---
layout: post
title: "ssh-keygen usage"
date: 2014-09-05 13:57:20 +0800
comments: true
categories: Perl	
---
Say I am on a server named "stsun1" and every time I want to login to a server named "stsun2", I have to enter my password, by using ssh-keygen we can avoid this.  

```

1. login to stsun1     

2. cd ~/.ssh and check if you have 'id_rsa',  'id_rsa.pub' files, if not, go to step 3, if you already have one, go to step 4.    

3. ssh-keygen -t rsa, and you will see 'id_rsa',  'id_rsa.pub' files.    

4. copy the .pub file to the .ssh dir on server stsun2, then "cat id_rsa.pub >> ~/.ssh/authorized_keys"

```

That' all!







