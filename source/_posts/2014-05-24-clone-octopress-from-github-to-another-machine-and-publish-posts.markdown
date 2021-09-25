---
layout: post
title: "换机之后Octopress如何安装"
date: 2014-05-24 14:00:50 +0800
comments: true
categories: Blog
---
When you want to clone a octopress blog from the github to a machine and then enabled to publish posts from the cloned repo, you can follow the following steps:

- &emsp; git clone -b source <https://github.com/isunix/isunix.github.com> octopress
- &emsp; cd octopress
- &emsp; git clone <https://github.com/isunix/isunix.github.com> _deploy
- &emsp; sudo gem install bundler
- &emsp; bundle install
- &emsp; bundle exec rake "new_post["The Title of Your Article"]"
- &emsp; bundle exec rake generate
- &emsp; bundle exec rake preview
- &emsp; bundle exec rake deploy
- &emsp; git add .
- &emsp; git commit -m ‘your comment’
- &emsp; git push origin source
