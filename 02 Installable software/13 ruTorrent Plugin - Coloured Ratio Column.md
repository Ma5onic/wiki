ruTorrent Plugin - Coloured Ratio Column
========================================

This plugin adds colour to your ruTorrent UI's ratio column, changing from red to green (though orange and yellow) as your ratio increases.  
  
You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  

Installing the Plugin
---------------------

Whilst logged in via SSH simply execute these commands:  
  

    wget -qO ~/ratio.zip http://git.io/71cumA
    unzip -qo ~/ratio.zip -d ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/
    rm -f ratio.zip

  
Then simply open ruTorrent (or refresh the page if it was already open) to see the changes.  
  

