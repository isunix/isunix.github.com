---
layout: post
title: "使用Python的requests包下载电影"
date: 2015-12-04 14:50:25 +0800
comments: true
categories: Python
---
This post shows a working way to download movies using python requests module.

```py
import requests
import re
import sys

class MovieDownload:
    def __init__(self, url):
        self.url = url
        if self.url.__contains__('//'):
            self.download_movie()
        else:
            print("wrong url entered")


    def download_movie(self):
        r = requests.get(self.url)
        pattern_title = re.compile('<h2 class="entry_title">(.*?)</h2>')
        title = re.findall(pattern_title, r.text)[0].split('/')[0]
        pattern_to_download = re.compile('<li><a href="(.*?)">.*?1024\.mkv.*?</a>')
        movie_urls = re.findall(pattern_to_download, r.text)

        with open('movie.txt', 'w') as f:
            print("There are {} urls here!\n".format(len(movie_urls)))
            f.write("There are {} urls here!\n\n".format(len(movie_urls)))
            for movie_url in movie_urls:
                print("{}\n".format(movie_url))
                f.write("{}\n\n".format(movie_url))


url = "http://cn163.net/archives/3639/"
MovieDownload(url)

sys.exit(0)
```

and then execute the script as:

```sh
python3 movie_download.py
```
