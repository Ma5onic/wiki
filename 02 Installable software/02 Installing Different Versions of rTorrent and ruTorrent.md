Installing Different Versions of rTorrent and ruTorrent
=======================================================

When you install rTorrent and ruTorrent from the Install Software link you're given the latest version that Feral provides. This is currently 0.9.6 in the case of rTorrent and 3.6 for ruTorrent.  
  
Some trackers will restrict use of certain versions of rTorrent so it's handy to have some options. It's possible to install and use different versions of both rTorrent and ruTorrent if need be using the instructions in each section below. Whilst your choice of rTorrent is restricted to what is held at Feral it should be possible to install any new version of ruTorrent that's released without waiting for staff.  
  
You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  
  

Selecting an rTorrent Version
-----------------------------

The list below contains the versions of rTorrent and libtorrent that are available (the number after the \_w is the libtorrent version number). The versions followed by a \* were released in tandem and so should be preferred. Please note that versions ending in an odd number were classed as development releases so may have stability issues.  
  

    0.9.6_w0.13.6 *
    0.9.4_w0.13.4 *
    0.9.3_w0.13.3 *
    0.9.2_w0.13.2 *
    0.9.1_w0.13.1 *
    0.9.0_w0.13.0 *
    0.8.9_w0.12.9 *
    0.8.8_w0.12.9
    0.8.8_w0.12.8 *
    0.8.7_w0.12.7
    0.8.6_w0.12.6 *
    0.8.6_w0.12.5
    0.8.5_w0.12.6
    0.8.5_w0.12.5 *
    0.8.4_w0.12.6
    0.8.4_w0.12.5
    0.8.4_w0.12.4 *
    0.8.3_w0.12.6
    0.8.3_w0.12.5
    0.8.3_w0.12.4
    0.8.3_w0.12.3 *
    0.8.2_w0.12.6
    0.8.2_w0.12.5
    0.8.2_w0.12.4
    0.8.2_w0.12.3
    0.8.2_w0.12.2 *
    0.8.1_w0.12.6
    0.8.1_w0.12.5
    0.8.1_w0.12.4
    0.8.1_w0.12.3
    0.8.1_w0.12.2
    0.8.1_w0.12.1 *
    0.8.1_w0.12.0

  
Older versions of rTorrent might not worky very well with newer versions of ruTorrent so if you wish to use ruTorrent you may find yourself limited in the options you have.  
  
Install the version and restart rTorrent to activate it as follows:  
  

    echo -n 'version' > ~/private/rtorrent/.version
    pkill -fu "$(whoami)" 'SCREEN -S rtorrent'
    screen -S rtorrent rtorrent

  
In the first code above replace *version* with a version number in the previous list.  
  
You can verify the correct version is running with this command (you should see a process running which contains your chosen version number):  
  

    ps x | grep opt/rtorrent | grep -v grep

  
  

Installing a Different Version of ruTorrent
-------------------------------------------

The current version of ruTorrent installed is not the latest so if you wish to take advantage of any new features in the later version you'll need to install it manually. Before doing that, please take note of the following:  
  
    -    The instructions assume you want the latest version of ruTorrent. If you want to install an earlier version for some reason you'll need to edit the first command to grab an earlier version (or upload it separately via FTP);  
  
    -    The final command will result in your previous ruTorrent instance being removed and replaced. If you want it back you'd need to reinstall, either using the Install Software link on your manager page or manuall (if the previous version is not installed by the Install Software link);  
  
    -    Custom plugins you previously installed are not copied - this is because you should update them to match the version of ruTorrent you're using.  
  
To install the latest version please execute the following via SSH:  
  

    cd ~/www/$(whoami).$(hostname -f)/public_html/
    git clone https://github.com/Novik/ruTorrent.git
    cp -r rutorrent/conf/* ruTorrent/conf/
    cp rutorrent/.ht* ruTorrent/
    rm -rf rutorrent/ && mv ruTorrent/ rutorrent/

  
  

Troubleshooting
---------------

*When I restart rTorrent I get a message "screen is terminating"*  
Try starting up rTorrent without screen (just type rtorrent and press `enter`). If you see a message like the following, please double-check you've selected a correct version:  
  

    /usr/local/bin/rtorrent: line 24: /opt/rtorrent/version_entered/bin/rtorrent: No such file or directory

  
  

