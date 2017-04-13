ruTorrent Plugin - Fileupload
=============================

This plugin will allow you to use Plowshare to upload to various filesharing services via ruTorrent.  
  

Preparation
-----------

You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  
As it's not possible to set a path to plowup (Plowshare's uploading software) within the plugin's configuration files you'll need to make sure that plowup is in your PATH. Otherwise you'll receive an error that rTorrent is not able to access it. To do this, please log in via SSH and execute the following commands:  
  

    echo "PATH=$HOME/bin:$PATH" > ~/.bashrc
    source ~/.bashrc

  
  

Installing Fileupload
---------------------

### Installing Plowshare

To install Plowshare execute the following commands:  
  

    mkdir -p ~/bin && bash
    git clone https://github.com/mcrapet/plowshare.git ~/.plowshare-source && cd ~/.plowshare-source
    make install PREFIX=$HOME
    cd && rm -rf .plowshare-source

  
  

### Configuring Plowshare

Run this command to install the plowshare modules:  
  

    plowmod --install

  
If you get "command not found" then you need to revisit the preparation steps above because your ~/bin/ directory is not in PATH.  
  
  

### Installing the Fileupload Plugin

Execute these commands to install the plugin:  
  

    cd ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/
    svn co -q https://github.com/nelu/rutorrent-thirdparty-plugins/trunk/fileupload

  
You should then refresh ruTorrent to make sure the plugin can communicate with your plowup binary correctly. If you get an error ("fileupload: Plugin will not work. rTorrent user can't access external program (plowup)."), kill and restart rTorrent like so:  
  

    pkill -fu "$(whoami)" 'SCREEN -S rtorrent'
    screen -S rtorrent rtorrent

  
  

