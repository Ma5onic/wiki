rTorrent - Notifications
========================

There are different ways you can be notified of when torrents are added or completed in rTorrent. This guide covers just two of these services - Growl and Pushbullet.  
  
You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  
  

Growl
-----

This script will send a Growl notification when you add a torrent and when the torrent is completed. By default it sends a notification for every torrent, but it can be customized based on watch folder or torrent label.  
  
Growl is available for [Windows](http://www.prowlapp.com/faq.php#windows), [Mac](http://growl.info/) and [Linux](http://mattn.github.io/growl-for-linux/).  
  
  

### Installing Growl

Execute these commands to install the necessary script and libraries, and to configure rTorrent to use them:  
  

    wget -qO ~/growltorrent.py http://btp.pw/growltorrent.py
    echo "system.method.set_key = event.download.finished,notify_finished,"execute=python,$PWD/growltorrent.py,--finished,$d.get_name="" >> ~/.rtorrent.rc
    echo "system.method.set_key = event.download.inserted_new,notify_inserted_new,"execute=python,$PWD/growltorrent.py,--inserted-new,$d.get_name="" >> ~/.rtorrent.rc
    pkill -fu "$(whoami)" 'SCREEN -S rtorrent'
    screen -dmS rtorrent rtorrent
    easy_install --user gntp

  
  

### Configuring Growl

You'll need to edit the script to supply the relevant details. You can do this easily via SSH by executing `nano ~/growltorrent.py`  
  
In the following section replace the IP address with yours. The password field is optional but sensible - change test in the config file and set the same password within Growl itself. If you don't want a password simply remove the word test (leaving the double quotes)  
  

    CONFIG = {
    "hostname": "123.45.67.89",
    "password": "test"
    }

  
Make sure that port `23053` is opened/forwarded on your router and that Growl is set to allow network connections. You can test your setup by running the following commands on your slot (feel free to change the message!):  
  

    python ~/growltorrent.py --finished "A torrent was finished"
    python ~/growltorrent.py --inserted-new "A torrent was added"

  
  

Pushbullet
----------

First of all you need an account at [Pushbullet](https://www.pushbullet.com/) and the necessary API access token. You can get this from the My Account section of the Pushbullet site, clicking Create Access Token. You should make a note of this as it's necessary to make use of the API.  
  
  

### Creating and Configuring a Pushbullet Script

Create the necessary file by executing this command:  
  

    nano ~/pushbullet.sh

  
Then paste the following, replacing *access\_token* with the API access token you obtained earlier:  
  

    #!/bin/bash
    tname=$1
    curl -u access_token: https://api.pushbullet.com/v2/pushes -d type=note -d title="$tname added to rTorrent"

  
You should then make it executable with this command:  
  

    chmod +x ~/pushbullet.sh

  
To test, execute this command:  
  

    ~/pushbullet.sh push test

  
  

### Configuring rTorrent

To configure rTorrent to use the script simply execute the following:  
  

    echo "system.method.set_key = event.download.inserted_new,push_me,\"execute=$PWD/pushbullet.sh,\$d.get_name=\"" >> ~/.rtorrent.rc
    pkill -fu "$(whoami)" 'SCREEN -S rtorrent' 
    screen -dmS rtorrent rtorrent

  
  

