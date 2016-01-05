---
layout: post
title: Download And Play Any Song From Command Line Instantly
---

You ever wanted to start playing "Let It Burn", like really fast?

Me too, and this is the fastest way I've seen thus far.  This is how you do it.

1. Download and install [youtube-dl] by copying and pasting this into terminal:

```bash
sudo wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl && sudo chmod a+rx /usr/local/bin/youtube-dl
```

2. Put this in your .bash_aliases file.  If you don't already have it, drop it off in the home folder with the following command:

```bash
touch ~/.bash_aliases
```

Open it with whatever text editor you prefer and add this:

```bash
function play {
    # Skip DASH manifest for speed purposes. This might actually disable
    # being able to specify things like 'bestaudio' as the requested format,
    # but try anyway.
    # Get the best audio that isn't WebM, because afplay doesn't support it.
    # Use "$*" so that quoting the requested song isn't necessary.
    youtube-dl --default-search=ytsearch: \
               --youtube-skip-dash-manifest \
               --output="${TMPDIR:-/tmp/}%(title)s-%(id)s.%(ext)s" \
               --restrict-filenames \
               --format="bestaudio[ext!=webm]" \
               --exec=afplay "$*"
}
```

3. Save, exit, and reopen terminal, and try it like this:

```play usher - let it burn ```

![Usher](http://i.giphy.com/11Jo6MieZMiPZu.gif)

If you just want to save any song to the current folder, just use this alias:

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
