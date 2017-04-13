How do I make thumbnails of video files
=======================================

**[Movie Thumbnailer (mtn)](http://moviethumbnail.sourceforge.net/)**  
  

    Movie thumbnailer (mtn) -- saves thumbnails (screenshots) of movie or video files to jpeg files. 
    It uses FFmpeg's libavcodec as its engine, so it supports all popular codecs, e.g. divx h264 mpeg1 mpeg2 mp4 vc1 wmv xvid, 
    and formats, e.g. .3gp .avi .dat .mkv .wmv. mtn is open source software. It should run on all operating systems which have gcc, 
    FFmpeg, and GD, for example, Linux and Windows.

  
This FAQ assumes you know how to [SSH](https://www.feralhosting.com/faq/view?question=12) into your slot.  
  
**1:** Download [mtn](http://moviethumbnail.sourceforge.net/) and extract mtn  
  
**copy and paste this entire thing as one command, or break it into three at the '&&'s**  
  

    wget http://sourceforge.net/projects/moviethumbnail/files/movie%20thumbnailer%20linux%20binary/mtn-200808a-linux/mtn-200808a-linux.tgz/download -O mtn.tar.gz && tar xfvz mtn.tar.gz && cd mtn-200808a-linux/

  
**2:** Downloading the font files needed.  
   
We'll use the free Liberation fonts from the Debian repo  
  
**a:** Download  
  

    wget http://ftp.us.debian.org/debian/pool/main/f/fonts-liberation/fonts-liberation_1.07.4-1_all.deb

  
**b:** Extract the .deb  
  

     ar x fonts-liberation_1.07.4-1_all.deb

  
**c:** Extract the data.tar.xz (where the font files are)  
  

    tar xf data.tar.xz

  
In order to use [mtn](http://moviethumbnail.sourceforge.net/), you must supply the path to the font files we just downloaded because the servers have no fonts installed by default.  
  
Your commands will look something like this(I recommend adding an alias, see below):  
  

    ~/mtn-200808a-linux/mtn ~/private/rtorrent/data/movie.avi -f ~/mtn-200808a-linux/usr/share/fonts/truetype/liberation/LiberationMono-Bold.ttf -c 3 -r 3 -s 600

  
The -f needs to be followed by the path to your font.tff file. The -c and -r are for number of columns and number of rows, respectively.  -s takes the image every 600 seconds, until you've hit your r/x limit.  
  
Gives you an image that looks like this:  
  
![](http://i.imgur.com/QYX3T.jpg)  
  
To simplify things you can add the following line to your **~.bashrc**  
  

    alias mtn="~/mtn-200808a-linux/mtn -f ~/mtn-200808a-linux/usr/share/fonts/truetype/liberation/LiberationMono-Bold.ttf -c # -r # -s #"

  
Be sure to replace the \#'s with actual numbers, based on how you want the image to look.  Or if you plan on using many different setups, remove the "-c \# -r \# -s \#" and add those in when using the command.  
  
And then use the command by running  
  

    mtn ~/path/to/cute.kitties.awww.mp4

  
  

