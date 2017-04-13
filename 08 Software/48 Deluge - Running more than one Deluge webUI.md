Deluge - Running more than one Deluge webUI
===========================================

Start off by following this FAQ on [running more than one instance of Deluge](https://www.feralhosting.com/faq/view?question=197).  
  
Shell into your slot and go into your new deluge directory and edit the web.conf file  
  

    cd ~/.config/deluge2 && nano web.conf

  
Near the top, around 5 lines down you will see "port" and then 5 numbers. This is the port that your current Deluge webUI is running on. Pick another random 5 digit number between *10000 - 50000* and put that in here. Make sure you remember what it was too as you will need it in a minute. Once you have done this, go further down the file until you see the configuration option "base". This will look like "/username/deluge/" change this to "/". Once you are done, hold *Ctrl+O*, then enter to save. Then *Ctrl+X* to exit.  
  
Next, we will start the new webUI. To do this, simply run the following:  
  

    deluge-web -c ~/.config/deluge2 --fork

  
To ensure that the second webUI restarts when the server does, you will want to add it do the cron, so:  
  

    crontab -e

  
Paste the following in exactly, at the bottom  
  

    @reboot /usr/local/bin/deluge-web -c ${HOME}/.config/deluge2

  
You should now be able to access the secondary webUI on:  
  

    username.servername.feralhosting.com:PORT_YOU_CHOSE_EARLIER

  
You can now add the deluge daemon connection using the information returned in [running more than one instance of Deluge](https://www.feralhosting.com/faq/view?question=197) article under "Retrieve important information"  
  

