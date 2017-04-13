Autodl-irssi - Installation and Configuration
=============================================

**Please note!** Though this software runs in nearly all cases without problems, Feral cannot provide much support for its use or help should anything go wrong. Please make sure you've read this FAQ fully as help on the problem may be covered already.  
  
This notice absolutely does not prevent you from raising a ticket should anything go wrong but please bear in mind staff may not be able to assist beyond basic troubleshooting (for example restarting, clarifying error messages and so on).  
  

Preparation
-----------

You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  
  

Installation - using the automated bash script
----------------------------------------------

Features of the bash script:  
  
  1.  Installs the latest version of autodl-irssi  
  2.  Runs the fix script to use correct IPs for Feral slots  
  3.  Sets a port and password in autodl.cfg and the ruTorrent plugin's conf.php  
  4.  It does not amend autodl.cfg if it exists  
  
To use the script just use this command:  
  

    wget -qO ~/install.autodl.sh http://git.io/oTUCMg && bash ~/install.autodl.sh

  
  

Installation - manual
---------------------

Manual installation allows a greater degree of control but the automated script should be sufficient for the majority of use cases.  
  
  

### Preparation for manual install

  
First you need to make sure any previous versions are dead and removed, after having backed up the autodl.cfg. If this is your first time installing autodl you will not need to run these.  
  

    killall irssi -u $(whoami); screen -wipe
    cp -f ~/.autodl/autodl.cfg ~/.autodl/autodl.cfg.bak
    rm -rf ~/.irssi/scripts/AutodlIrssi ~/.irssi/scripts/autorun/autodl-irssi.pl
    rm -rf ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/autodl-irssi

  
  

### Installing autodl-irssi

    mkdir -p ~/.irssi/scripts/autorun ~/.autodl
        echo -e "[options]\ngui-server-port = 0\ngui-server-password = pass" > ~/.autodl/autodl.cfg
        wget -qO ~/autodl-irssi.zip https://github.com/autodl-community/autodl-irssi/releases/download/community-v1.60/autodl-irssi-community-v1.60.zip
        unzip -qo ~/autodl-irssi.zip -d ~/.irssi/scripts/
        cp -f ~/.irssi/scripts/autodl-irssi.pl ~/.irssi/scripts/autorun/
        rm -f autodl-irssi.zip .irssi/scripts/{README*,autodl-irssi.pl,CONTRIBUTING.md}

  
  

### Installing the autodl ruTorrent plugin

    wget -qO ~/autodl-rutorrent.zip https://github.com/autodl-community/autodl-rutorrent/archive/master.zip
    unzip -qo ~/autodl-rutorrent.zip
    mv ~/autodl-rutorrent-master/_conf.php ~/autodl-rutorrent-master/conf.php
    mv ~/autodl-rutorrent-master ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/autodl-irssi 
    rm ~/autodl-rutorrent.zip

  
  

Configuring - manual install
----------------------------

This guide does not cover configuring autodl.cfg (either manually or via the ruTorrent plugin). It only discusses fixing a couple of issues and configuring the plugin to be able to communicate with auto-irssi. This step is not needed if you run the bash script.  
  
  

### Fixing IPs

Autodl-irssi and its plugin assume a local IP of 127.0.0.1 rather than the 10.0.0.1 that Feral uses. These commands make the necessary changes - please execute them whilst autodl-irssi is not running (see the next section for checking if it's running and how to kill and start it up):  
  

    sed -i "s|use constant LISTEN_ADDRESS => '127.0.0.1';|use constant LISTEN_ADDRESS => '10.0.0.1';|g" ~/.irssi/scripts/AutodlIrssi/GuiServer.pm
    sed -i 's|$rtAddress = "127.0.0.1$rtAddress"|$rtAddress = "10.0.0.1$rtAddress"|g' ~/.irssi/scripts/AutodlIrssi/MatchedRelease.pm
    sed -i 's|my $scgi = new AutodlIrssi::Scgi($rtAddress, {REMOTE_ADDR => "127.0.0.1"});|my $scgi = new AutodlIrssi::Scgi($rtAddress, {REMOTE_ADDR => "10.0.0.1"});|g' ~/.irssi/scripts/AutodlIrssi/MatchedRelease.pm
    sed -i 's|if (!socket_connect($socket, "127.0.0.1", $autodlPort))|if (!socket_connect($socket, "10.0.0.1", $autodlPort))|g' ~/www/"$(whoami)"."$(hostname -f)"/public_html/rutorrent/plugins/autodl-irssi/getConf.php

  
  

### Linking autodl-irssi with the ruTorrent plugin

To be able to manage autodl-irssi through ruTorrent we need to get them communicating with each other by editing their config files. Nano is a good choice to do this since it will prevent possible line ending issues when using other tools.  
  
Edit the autodl-irssi config file with no by executing this command:  
  

    nano ~/.autodl/autodl.cfg

  
The file will look like this:  
  

    [options]
    gui-server-port = 0
    gui-server-password = pass

  
Change the port to something between `10001` and `49999` and change *pass* to a password of your choice.  
  
Once you're done hold `CTRL` and then press `x` to save. Press `y` to confirm.  
  
Using nano again, amend the ruTorrent plugin's config file:  

    nano ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/autodl-irssi/conf.php

  
Change the variables $autodlPort and $autodlPassword so they match what you selected in autodl.cfg.  
  
  

Starting and restarting
-----------------------

In order to restart the software the existing process should be killed. If the check below does not display a process number please proceed to step 3. These steps are tailored towards processes started by this FAQ.  
  
1.    Check:  

    pgrep -fu "$(whoami)" "autodl"

  
2.    Kill:  

    kill "$(pgrep -fu "$(whoami)" "autodl")"

  
3.    Restart:  

    screen -dmS autodl irssi

  
**Important note:** You can repeat step 1 after attempting to kill to check if it's been shut down. Give the program at least 10 seconds to shut down at step 2 before trying to restart. If it refuses to exit then you have to force it to quit using this command instead:  
  

    kill -9 "$(pgrep -fu "$(whoami)" "autodl")"

  
  

Upgrading
---------

You can choose to update autodl-irssi within ruTorrent by clicking the autodl-irssi tab and then the Update button, or within irssi by executing:  

    /autodl update

  
Updating the core files will revert parts of autodl-irssi to use 127.0.0.1 as a local IP instead of 10.0.0.1. So if you see an error after updating please re-run the bash script  
  
  

Cron - start up automatically if the server is rebooted
-------------------------------------------------------

Unfortunately sometimes the server needs to be rebooted. When this happens the system will start up a lot of the processes automatically on your slot. It will not however start up custom software. We need to manually set something up to make this happen.  
  
To bring up the crontab editor use the following command:  
  

    crontab -e

  
If this is your very first time you'll be given a choice of editors. Nano is fine to use so unless you specifically want something else just press enter.  
  
There will already be some basic information on crontabs in the file - you can keep it if you like, or get rid of it if you prefer. The lines are commented out so are for information purposes only and don't affect any cron jobs added.  
  
At a new line in the file copy-paste the following:  
  

    @reboot screen -dmS autodl irssi

  
  

Troubleshooting
---------------

*I get "Error: Could not connect: (111) Connection refused"*  
  
1.  Is autodl-irssi running? Check using the check command in the Starting and restarting section. Start it up if not.  
2.  If running, please try re-running the fix commands from the Configuration section. Refresh ruTorrent to see if it has helped.  
3.  If it hasn't helped, double check the port and passwords in autodl.cfg and conf.php for the plugin match.  
  

