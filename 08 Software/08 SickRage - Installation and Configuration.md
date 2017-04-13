SickRage - Installation and Configuration
=========================================

**Please note!** Though this software runs in nearly all cases without problems, Feral cannot provide much support for its use or help should anything go wrong. Please make sure you've read this FAQ fully as help on the problem may be covered already.  
  
This notice absolutely does not prevent you from raising a ticket should anything go wrong but please bear in mind staff may not be able to assist beyond basic troubleshooting (for example restarting, clarifying error messages and so on).  
  

Preparation
-----------

You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  
  

Installation - using the automated bash script
----------------------------------------------

Features of the bash script:  
  
  1.  Installs Sick Beard or SickRage from GitHub (this guide only covers SickRage - for Sick Beard please see [this guide](https://www.feralhosting.com/faq/view?question=332))  
  2. Configures the proxypass to provide an https URL  
  3. Can to choose to update the software and/or install only the proxypass  
  
To use the script just use this command:  
  

    wget -qO ~/install.sick http://git.io/vfGch && bash ~/install.sick

  
  

Installation - manual
---------------------

Manual installation allows a greater degree of control but the automated script should be sufficient for the majority of use cases.  
  
  

### Clone SickRage from GitHub

First you need to download SickRage by cloning the repository onto your slot. To do that, copy-paste the following:  
  

    git clone https://github.com/SickRage/SickRage ~/.sickrage

  
There's another repo you could use (SiCKRAGETV) if you wanted. To clone that the command would be:  
  

    git clone https://github.com/SiCKRAGETV/SickRage ~/.sickrage

  
  

### Start up SickRage

To start up SickRage we need to pick a port for it to run on. In the command below replace *port* with a number between **10001** and **49999**  
  

    python ~/.sickrage/SickBeard.py -d -p port --pidfile="$HOME/.sickrage/sickrage.pid"

  
If nothing happens or there is an error it could be that the port you picked is in use. Simply try with a different number.  
  
Once started up you can visit SickRage by visiting `http://server.feralhosting.com:port` where *server* is the name of your server and *port* is the port you picked earlier.  
  
Within the SickRage UI, click the Config icon (the two gears at the top) and then click General. Next, click the Interface tab. Near the bottom of the fields you'll be able to set a username and password for the web UI. Whilst it's not mandatory you do this, it is a sensible thing to do.  
  
  

### Configure the proxypass

The bash script in the first Installation section can set up the proxypass for you without installing SickRage, so even if you wish to use a different repository you can still make use of the script for this purpose.  
  
  

Configuring
-----------

This section covers connecting SickRage to the three torrent clients currently supported by Feral: rTorrent, Deluge and Transmission. In SickRage's user interface click the Config icon (the two gears at the top) and then click Search Settings. Next, click the Torrent Search tab. You can choose the torrent client you want to configure from the menu.  
  
  

### rTorrent

First of all you need to configure the rTorrent RPC and this is done by switching from apache to nginx. That can be done by following [this guide](https://www.feralhosting.com/faq/view?question=231).  
  
Enter the details as follows:  
  
`Torrent host:port`: <https://>*server*.feralhosting.com/*username*/rtorrent/rpc/ (replace *server* with your server name and *username* with your username)  
     
`Http Authentication`: Basic  
     
`Client username`: `rutorrent` (the word rutorrent, *not* your ruTorrent username)  
  
`Client password`: The same password as you use to access ruTorrent  
  
  

### Deluge (via webUI)

Enter the details as follows:  
  
`Torrent host:port`: <https://>*server*.feralhosting.com/*username*/deluge/ (replace *server* with your server name and *username* with your username)  
  
`Client password`: Your Deluge webUI password  
  
`Downloaded files location`: It might be set to rTorrent's data directory - make sure it's set to a location you're happy with (or make sure it's blank to use Deluge's default).  
  
  

### Deluge (via daemon)

There are a couple of commands we need to run via SSH first to obtain the daemon port and password (the password is not the same as the webUI password).  
  
To find the port run this command:  
  

    sed -rn 's/(.*)"daemon_port": (.*),/\2/p' ~/.config/deluge/core.conf

  
To find the password run this command:  
  

    sed -rn "s/$(whoami):(.*):(.*)/\1/p" ~/.config/deluge/auth

  
Armed with the port and password, enter the details as follows:  
  
`Torrent host:port`: <https://>*server*.feralhosting.com:*port* (replace *server* with your server name and *port* with the results of the command above)  
  
`Client username`: Your Deluge daemon username (unless you've changed it, it'll be your Feral username)  
     
`Client password`: Your Deluge daemon password  
  
`Downloaded files location`: Makke sure it's set to a location you're happy with (or make sure it's blank to use Deluge's default).  
  
  

### Transmission

Enter the details as follows:  
  
`Torrent host:port`: <https://>*server*.feralhosting.com/*username* (replace *server* with your server name and *username* with your username)  
  
`Transmission RPC URL`: `transmission/rpc`  
     
`Client username`: The username you use to access Transmission  
  
`Client password`: The same password as you use to access Transmission  
  
  

### SABnzbd

SickRage can also search for NZB files. This section covers connecting Sick Beard to [SABnzbd](https://www.feralhosting.com/faq/view?question=125).  
  
Enter the details as follows:  
  
`SABnzbd server URL`: <https://>*server*.feralhosting.com:*port*/sabnzbd/ (replace *server* with your server name and *port* with your HTTPS port for SABnzbd)  
  
`SABnzbd username`: The username you set for the SABnzbd UI  
  
`SABnzbd password`: The password you set for the SABnzbd UI  
  
`SABnzbd API key`: Find this in the General section of SABnzbd's settings  
  
  

Starting and restarting
-----------------------

In order to restart the software the existing process should be killed. If the check below does not display a process number please proceed to step 3. These steps are tailored towards processes started by this FAQ.  
  
1.    Check:  

    pgrep -fu "$(whoami)" "python $HOME/.sickrage/SickBeard.py -d"

     
2.    Kill:  

    kill "$(pgrep -fu "$(whoami)" "python $HOME/.sickrage/SickBeard.py -d")"

     
3.    Restart:  

    python ~/.sickrage/SickBeard.py -d --pidfile="$HOME/.sickrage/sickrage.pid"

  
**Important note:** You can repeat step 1 after attempting to kill to check if it's been shut down. Give the program at least 10 seconds to shut down at step 2 before trying to restart. If it refuses to exit then you have to force it to quit using this command instead:  
  

    kill -9 "$(pgrep -fu "$(whoami)" "python $HOME/.sickrage/SickBeard.py -d")"

  
  

Cron - start up automatically if the server is rebooted
-------------------------------------------------------

Unfortunately sometimes the server needs to be rebooted. When this happens the system will start up a lot of the processes automatically on your slot. It will not however start up custom software. We need to manually set something up to make this happen.  
  
To bring up the crontab editor use the following command:  
  

    crontab -e

  
If this is your very first time you'll be given a choice of editors. Nano is fine to use so unless you specifically want something else just press enter.  
  
There will already be some basic information on crontabs in the file - you can keep it if you like, or get rid of it if you prefer. The lines are commented out so are for information purposes only and don't affect any cron jobs added.  
  
At a new line in the file copy-paste the following:  
  

    @reboot rm -rf ~/.sickrage/sickrage.pid
    @reboot python ~/.sickrage/SickBeard.py -d --pidfile="$HOME/.sickrage/sickrage.pid"

  
  

Troubleshooting
---------------

*When I click "Test Connection" I get the error 'Error: Unable to connect to rTorrent'*  
If rTorrent is running and you've [switched to nginx](https://www.feralhosting.com/faq/view?question=231) this likely means some of the details you've entered are not correct. Please double-check that your username is **rutorrent** (as in the actual word, "rutorrent", *not* the username you use to log in to ruTorrent).  
  
*I went to start up SickRage and received an error '...sickrage.pid already exists. Exiting.'*  
Assuming you're using the default locations please run the following command before trying the start up command again:  

    rm ~/.sickrage/sickrage.pid

  
  

