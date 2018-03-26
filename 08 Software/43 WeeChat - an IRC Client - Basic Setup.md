WeeChat - an IRC Client - Basic Setup
=====================================

  
This FAQ is for downloading and installing [WeeChat](http://www.weechat.org/) on your slot.  
  
WeeChat is a fast, light and extensible chat client. It runs on many platforms like Linux, Unix, BSD, GNU Hurd, Mac OS X and Windows (cygwin).  
  
Please run this command in SSH first:  
  

    mkdir -p ~/bin && bash

  

1: Build WeeChat and install it
-------------------------------

Previous versions suggested you run an installer script to compile a local version. All slot servers now have Weechat installd by default so this step can be skipped.

To uninstall previous versions please run:

    rm ~/bin/weechat
  

2: Start WeeChat
----------------

  
We have added the location to the `PATH` in step 1, so we can use this command:  
  

    screen -dmS weechat weechat

  
Now attach to the screen:  
  

    screen -r weechat

  
The full path to execute WeeChat is:  
  

    ~/bin/weechat

  

3: Configure WeeChat
--------------------

  
These are some required settings. You enter them in WeeChat after you have started it.  
  

    /server add What-Network irc.what-network.net/6697 -ssl

  
Replace  `"username,username_1,username_2"` and the two  instances of `"username"` with a username of your  choice.  
  

    /set irc.server.What-Network.nicks "username,username_1,username_2"
    /set irc.server.What-Network.username "username"
    /set irc.server.What-Network.realname "username"

  
Some final settings:  
  

    /set irc.server.What-Network.ssl on
    /set irc.server.What-Network.ssl_verify off
    /set irc.server.What-Network.ssl_dhkey_size 1024
    /save

  
Add other networks as desired.  
  

4: Connecting to predefined IRC networks
----------------------------------------

  
Use this command to connect to the Feral Hosting IRC channel,  `#feral` on the `What-Network`  IRC network that we defined in the previous step.  
  

    /connect What-Network

  

5: Join a channel
-----------------

  

    /j #feral

  
To detach from the screen, press and hold `CRTL` and `a` then press `d`.  
  

Further reading
---------------

  
Here you can get information on further configuration, such as auto join and more.  
  
[WeeChat FAQ](http://www.weechat.org/files/doc/weechat_faq.en.html)  
  
[WeeChat Quick Start Guide](http://www.weechat.org/files/doc/stable/weechat_quickstart.en.html)  
  
[WeeChat Quick Start Guide](http://www.weechat.org/files/doc/stable/weechat_user.en.html)  
