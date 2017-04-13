ruTorrent Plugin - Filemanager
==============================

You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  

Installing Filemanager
----------------------

To install Filemanager execute these commands:  
  

    cd ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/
    svn co -q https://github.com/nelu/rutorrent-thirdparty-plugins/trunk/filemanager

  
As with all plugins, you'll need to refresh ruTorrent if it's open in a browser to get any changes recognised.  
  
  

Using the Screenshots Function of Filemanager
---------------------------------------------

### Installing ffmpeg

The plugin uses ffmpeg to generate screenshots and due to the removal of this software from Debian stable you'll need to install it to your slot instead. This is easily done by executing the following commands:  
  

    mkdir -p ~/bin && bash
    wget -qO ~/ffmpeg.tar.gz http://johnvansickle.com/ffmpeg/releases/ffmpeg-release-64bit-static.tar.xz
    tar xf ~/ffmpeg.tar.gz 
    rm -rf ffmpeg-*-64bit-static/{manpages,presets,readme.txt}
    cp ~/ffmpeg-*-64bit-static/* ~/bin
    chmod 700 ~/bin/{ffmpeg,ffprobe,ffmpeg-10bit,qt-faststart}
    rm -rf ffmpeg{.tar.gz,-*-64bit-static}

  
  

### Configuring Filemanager to Use ffmpeg

Execute these commands to properly configure Filemanager to use your version of ffmpeg and ffprobe:  
  

    cd && sed -i "s|(getExternal(\"ffprobe\")|(getExternal(\"~/bin/ffprobe\")|g" ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/filemanager/flm.class.php
    sed -i "s|(getExternal('ffmpeg')|(getExternal('$(pwd)/bin/ffmpeg')|g" ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/filemanager/flm.class.php

  
  

Troubleshooting
---------------

*When I do something (create an archive, move a file etc.) the action seems to complete but nothing has changed*  
Make sure you've set the permissions correctly in Filemanager's scripts directory.  
  
*When I try to generate screenshots I get ffmpeg/ffprobe related errors*  
Make sure you've configured screenshots to point to the instance of ffmpeg running on your slot. If in doubt, follow this guide from top to bottom again and refresh ruTorrent.  
  

