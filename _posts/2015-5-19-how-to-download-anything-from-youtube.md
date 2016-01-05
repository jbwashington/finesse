---
layout: post
title: Download Any Song From Command Line Instantly
---

1. download and install [youtube-dl] by copying and pasting this into terminal:

```
sudo wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl && sudo chmod a+rx /usr/local/bin/youtube-dl
```

2. put this in your .bash_aliases file.  If you don't already have it, drop it off in the home folder with ```touch ~/.bash_aliases``` then open it with whatever text editor you prefer and add this:

```bash
function mp3 {
    # Get the best audio from YouTube, convert it to MP3, and save it to the current
    # directory.
    youtube-dl --default-search=ytsearch: \
               --restrict-filenames \
               --format=bestaudio \
               --extract-audio \
               --audio-format=mp3 \
               --audio-quality=1 "$*"
}
```

3. save, exit, and reopen terminal, and try it like this:

```mp3 fetty wap - 1738 ```

check the folder you're in now, the mp3 should be in there.

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

![Remy Boys](http://i.giphy.com/6DGdl9irxUnba.gif)
