Jackett - Basic setup
=====================

In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH Guide - The Basics](https://www.feralhosting.com/faq/view?question=12)  
  
Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)  
  
You login information for the relevant slot will be shown here:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)  
  

Installing Jackett
------------------

  
**Important note:** Jackett requires mono to function. But, since it is also a tool for use with Sonarr you should already have this installed. Please see [this](https://www.feralhosting.com/faq/view?question=303) page for a guide to installing mono and Sonarr.  
  
Then run these commands to get and install Jackett:  
  

    wget -qO ~/Jackett.tar.gz https://github.com/Jackett/Jackett/releases/download/v0.7.303/Jackett.Binaries.Mono.tar.gz
    tar xf ~/Jackett.tar.gz
    rm -rf ~/Jackett.tar.gz

  
Start Jackett:  
  

    screen -dmS jackett mono --debug ~/Jackett/JackettConsole.exe && screen -list

  
Attach to this screen at any time by using the command `screen -r jackett`  
You can stop Jackett with ctrl+c to get the config file created.  
  
Your configuration will be saved here at `~/.config/Jackett/ServerConfig.json`  
Now we need to randomize the start port because the default is 9117 (and this may already be taken):  
  

    sed -i 's|"Port": 9117,|"Port": '$(shuf -i 10001-59001 -n 1)',|g' ~/.config/Jackett/ServerConfig.json

  
You can read the port  and find the access URL with:  

    echo -e "\nhttp://$(hostname -f):$(sed -rn 's|(.*)"Port": (.*),|\2|p' ~/.config/Jackett/ServerConfig.json)"

  

