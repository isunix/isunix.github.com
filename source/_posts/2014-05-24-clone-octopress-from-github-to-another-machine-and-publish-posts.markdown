---
layout: post
title: "clone octopress from github to another machine and publish posts"
date: 2014-05-24 14:00:50 +0800
comments: true
categories: Blog
---
When you want to clone a octopress blog from the github to a machine and then enabled to publish posts from the cloned repo, you can follow the following steps:   

1. git clone -b source https://github.com/isunix/isunix.github.com octopress    
2. cd octopress    
3. git clone https://github.com/isunix/isunix.github.com _deploy        
4. sudo gem install bundler   
5. bundle install    
6. rake new_post[“The Title of Your Article”]    
7. bundle exec rake generate
8. bundle exec rake preview    
9. bundle exec rake deploy    
10. git add . 
11. git commit -m ‘your comment’  
12. git push origin source