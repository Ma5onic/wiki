ruTorrent Plugin - Screenshots
==============================

You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  

Installing ffmpeg
-----------------

The plugin uses ffmpeg to generate screenshots and due to the removal of this software from Debian stable you'll need to install it to your slot instead. This is easily done by executing the following commands:  
  

    mkdir -p ~/bin && bash
    wget -qO ~/ffmpeg.tar.gz http://johnvansickle.com/ffmpeg/releases/ffmpeg-release-64bit-static.tar.xz
    tar xf ~/ffmpeg.tar.gz 
    rm -rf ffmpeg-*-64bit-static/{manpages,presets,readme.txt}
    cp ~/ffmpeg-*-64bit-static/* ~/bin
    chmod 700 ~/bin/{ffmpeg,ffprobe,ffmpeg-10bit,qt-faststart}
    rm -rf ffmpeg{.tar.gz,-*-64bit-static}

  
  

Installing Screenshots
----------------------

If you're using 3.6 of ruTorrent (which is the default version installed here at Feral) you won't be able to use the general plugin install method described on [this page](https://www.feralhosting.com/faq/view?question=282). Instead, execute these commands:  
  

    rm -rf ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/screenshots
    wget -q https://bintray.com/artifact/download/novik65/generic/plugins/screenshots-3.6.tar.gz
    tar xf screenshots-3.6.tar.gz -C ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/
    rm screenshots-3.6.tar.gz

  
The first command removes any existing instance of screenshots in case you previously installed an incorrect version. Naturally if you are using the 3.7 version of ruTorrent then you can install Screenshots by following the general plugin install method.  
  
  

Configuring screenshots
-----------------------

To make sure your version of ffmpeg is used we need to amend the screenshot plugin's config file. This can be done simply by executing this command:  
  

    cd && sed -i "s|ffmpeg'] = ''|ffmpeg'] = '$(pwd)/bin/ffmpeg'|g" ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/screenshots/conf.php

  
As with all plugins, you'll need to refresh ruTorrent if it's open in a browser to get any changes recognised.  
  
  

Troubleshooting
---------------

*When I load ruTorrent I get an error "screenshots: Plugin will not work. rTorrent user can't access external program (ffmpeg)"*  
Make sure you've configured screenshots to point to the instance of ffmpeg running on your slot. If in doubt, follow this guide from top to bottom again and refresh ruTorrent.  
  
*When I generate screenshots I get no pictures, just a list of numbers*  
That happens when using the 3.7 version of screenshots with the 3.6 version of ruTorrent. Please install the 3.6 version using the instructions above.  
  

