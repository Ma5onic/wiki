ruTorrent Plugin - Fileshare
============================

You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  

Installing Fileshare
--------------------

Fileshare requires Filemanager and both can be installed using the following commands:  
  

    cd ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/
    svn co -q https://github.com/nelu/rutorrent-thirdparty-plugins/trunk/filemanager
    svn co -q https://github.com/nelu/rutorrent-thirdparty-plugins/trunk/fileshare

  
Further information on Filemanager can be found [here](https://www.feralhosting.com/faq/view?question=330).  
  
  

Configuring Fileshare
---------------------

These commands will configure the plugin to run on your slot:  
  

    ln -s ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/fileshare/share.php ~/www/$(whoami).$(hostname -f)/public_html/
    sed "/if(getConfFile(/d" -i ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/fileshare/share.php
    sed -i "s|'http://mydomain.com/share.php';|'http://$(whoami).$(hostname -f)/share.php';|g" ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/fileshare/conf.php

  
  

