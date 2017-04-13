ruTorrent Plugin - Mediastream
==============================

This is a plugin to allow you to stream from within ruTorrent. It requires the DivX web player to be installed first on your computer. This guide does not cover that step and for anything other than test streaming something like [Plex](https://www.feralhosting.com/faq/view?question=297) will probably be a better solution for you.  
  
You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  

Installing Mediastream
----------------------

Mediastream requires Filemanager and both can be installed using the following commands:  
  

    cd ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/
    svn co -q https://github.com/nelu/rutorrent-thirdparty-plugins/trunk/filemanager
    svn co -q https://github.com/nelu/rutorrent-thirdparty-plugins/trunk/mediastream

  
Further information on Filemanager can be found [here](https://www.feralhosting.com/faq/view?question=330).  
  
  

Configuring Mediastream
-----------------------

These commands will configure the plugin to run on your slot:  
  

    mkdir ~/www/$(whoami).$(hostname -f)/public_html/stream
    ln -s ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/mediastream/view.php ~/www/$(whoami).$(hostname -f)/public_html/stream/
    sed -i "s|'http://mydomain.com/stream/view.php';|'http://$(whoami).$(hostname -f)/stream/view.php';|g" ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/mediastream/conf.php

  
  

Troubleshooting
---------------

*I get the error "Video cannot be found, it may have been removed"*  
Please make sure the configuration steps have been followed correctly.  

