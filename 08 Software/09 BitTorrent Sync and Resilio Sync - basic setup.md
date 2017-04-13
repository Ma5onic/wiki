BitTorrent Sync and Resilio Sync - basic setup
==============================================

**Important Note:** There is a conflict between the new version of btsync released `1.4.75` and the previously configured conf file used in this FAQ. You will need to do these three things:  
  
**1:** Download the conf file again and follow the steps below this notice to configure it. You do not need to set a username or password this time. You will be prompted to create this when you visits the WebUi.  
  
**2:** restart btsync using this command in SSH:  
  

    killall -u $(whoami) btsync && ~/btsync/./btsync --config ~/btsync/sync.conf

  
**3:** Clear your browser history and cache completely and then reload the WebUi  
  
**End of Notice**  
  
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)  
  
Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)  
  
Your login information for the relevant slot will be shown here:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)  
  

btsync manual installation
--------------------------

  
Here are some basic set-up steps for btsync.  
  
Info: Automatically sync files via secure, distributed technology. [btsync homepage](http://labs.bittorrent.com/experiments/sync.html)  
  
You will need to execute these commands in [SSH](https://www.feralhosting.com/faq/view?question=12)  
  
  

### btsync 1.4

  

    mkdir -p ~/btsync
    wget -qO ~/btsync/btsync.tar.gz http://download.getsyncapp.com/endpoint/btsync/os/linux-x64/track/stable
    tar xf ~/btsync/btsync.tar.gz -C ~/btsync && cd && rm -f btsync/btsync.tar.gz

  

### rslsync

  
BTSync has been rebranded to Resilio Sync:  
  

    wget https://download-cdn.getsync.com/stable/linux-x64/resilio-sync_x64.tar.gz
    mkdir -p ~/rslsync; tar xvzf resilio-sync_x64.tar.gz -C ~/rslsync
    mkdir -p ~/.rslsync; ~/rslsync/rslsync --dump-sample-config > ~/.rslsync/rslsync.conf && rm resilio-sync_x64.tar.gz

  

Configure the conf file:
------------------------

  
Now run this command to set a few variables we need:  
  

    sed -i 's|MYHOME|'"$HOME"'|g' ~/.rslsync/rslsync.conf
    sed -i 's|8888|'$(shuf -i 10001-49000 -n 1)'|g' ~/.rslsync/rslsync.conf

  

Start Resilio Sync:
-------------------

  
Now start Resilio Sync using this command:  
  

    ~/rslsync/rslsync --config ~/.rslsync/rslsync.conf

  
It is now running in the background ready for us to use.  
  

Accessing the WebUi
-------------------

  
To access the Web Gui you must use a browser and visit the URL, where `username` is your Feral username and `server` is the name of your Feral server that hosts the slot Resilio Sync is installed on:  
  
**Important note:** to use https you can use the URL format `username.server.feralhosting.com` without editing the conf. You may have to press `F5` a few times for the Gui to load after accepting the invalid cert.  
  
Use this command  to see the generated WebUI port via SSH:  
  

    sed -rn 's|.*"listen" : "0.0.0.0:(.*)".*|\1|p' ~/.rslsync/rslsync.conf

  
Then modify the example URL below with your server information and WebUI port listed by the previous command:  
  

    server.feralhosting.com:PORT

  
For example:  
  

    chronos.feralhosting.com:34567

  
or  
  

    username.server.feralhosting.com:PORT

  
For example:  
  

    superman.chronos.feralhosting.com:34567

  
Either will work.  
  

Using the WebUI
---------------

Once you are at the WebUI you will be prompted to create a user account. This is only for accessing and using the WebUI.  
  
Once you have done this step you will be prompted to log in and then you're ready to use it!  
  

Network & Speed Tweaks
----------------------

Please be aware that these were tweaks were first suggested before BTSync was rebranded to Resilio Sync - options may be worded differently, located elsewhere or removed entirely.  
  
Mileage may vary, remember the default values to go back to. I'll also mention them here.  
  

    Setting disk_low_priority to False

  
  
Allows for more disk usage, specially if you're Syncing to a secondary hard drive, no reason to have it set to low priority.  
  

    send_buf_size and recv_buf_size

  
The default values are 10 per variable. I slowly increased them by 5 each time and see if I saw any improvement. I didn't see any improvement till I set both variables to 35. Like I said, you may change them further and see if you find any improvement, but don't go to crazy.  
  
  

Kill btsync
-----------

To Kill the processes use this command to find running instances:  
  

    ps x | grep btsync | grep -v grep

  
Kill all btsync processes this way:  
  

    killall -u $(whoami) btsync

  
  

Kill Resilio Sync
-----------------

To Kill the processes use this command to find running instances:  
  

    ps x | grep rslsync| grep -v grep

  
Kill all rslsync processes this way:  
  

    killall -u $(whoami) rslsync

  
  

