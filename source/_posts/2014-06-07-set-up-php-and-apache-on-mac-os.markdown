---
layout: post
title: "在mac上搭建PHP和Apache服务"
date: 2014-06-07 14:25:00 +0800
comments: true
categories: PHP
---
I have set up Apache and PHP on my computer many times, every time I googled or Baidued about it, it is high time to keep a note about those steps.    

1. sudo mate /etc/apache2/httpd.conf
2. uncomment "#LoadModule php5_module libexec/apache2/libphp5.so"
3. save the file and quit. 
4. sudo cp /etc/php.ini.default /etc/php.ini
5. sudo apachectl start 
6. ln -s /Library/WebServer/Document $HOME/www
7. rename the file "index.html.en" or just delete the file if you do not want to be botthered.  

That's the steps all it takes to set up your apache and PHP on a MAC OS machine.

