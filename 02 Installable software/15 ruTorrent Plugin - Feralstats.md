ruTorrent Plugin - Feralstats
=============================

Feralstats is a user-created plugin for ruTorrent which displays your usage page information within the ruTorrent UI. As it is user-created it has  
  
You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  

Installing and Authenticating Feralstats
----------------------------------------

To install and use first run these commands:  
  

    cd ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/
    wget -qO feralstats.zip http://git.io/nB1WyA
    unzip -qo feralstats.zip && rm -f feralstats.zip

  
In order to actually use the plugin you need to refresh ruTorrent, select to "Authorize the statustool" and grant permissions for each of the three requests. Then access ruTorrent again and your usage should be displayed.  
  
  

Usage Notes
-----------

Feralstats was made by a user and is therefore not something that Feral maintains. It's an improvement over the default ruTorrent plugin for disk space since that plugin merely provides the total disk space left, not space left in your quota.  
  
However, it works by displaying the information from your usage page - therefore it only changes when the usage page changes (which is when done manually, or automatically every 24 hours). Feral's slots have also moved to an unrestricted bandwidth model and therefore the bandwidth display is no longer relevant.  
  
  

Troubleshooting
---------------

*It just says "Authorize the statustool" in ruTorrent even though I already have*  
Please make sure you've selected to grant permission to all three requests as the plugin will not work otherwise. If you have done this, please try removing the plugin and reinstalling it.  

