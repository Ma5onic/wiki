Plex Requests - Basic Setup
===========================

Plex Requests is a new and simple way for users to request new contents for Plex, and automated download requests linking it with [Couchpotato](https://www.feralhosting.com/faq/view?question=218), [Sickrage](https://www.feralhosting.com/faq/view?question=281) or [Sonarr](https://www.feralhosting.com/faq/view?question=303). For more informations, please check [official site](http://plexrequests.8bits.ca/)  
  
\# Installing Meteor  
  
First, we've to install Meteor with this command :  
  

    curl https://gist.githubusercontent.com/feralhosting/ed3321cdebf8a59d47a5/raw/979f8b1d042c9ed20d2db0f9705b8a6df4133bdf/meteor.sh | sh 

  
after we've to check if Meteor is correctly installed, so check it with this command :  
  

    meteor --version 

  
and if it has installed correctly you will see this :  
  
![](http://i.imgur.com/y1NZVYF.png)  
  
Note: If meteor cannot be found, try disconnecting and reconnecting to the host.  
  

Installing Plex Requests
------------------------

  
  
After you've installed Meteor correctly, you can install Plex Requests, so first we clone git repo with this command:  

    git clone https://github.com/lokenx/plexrequests-meteor.git ~/.plexrequests
    cd ~/.plexrequests

  
After these two commands, we open a new screen and start Plex Requests with this command :  

    screen -S plexrequests meteor --port portnumber

  
portnumber should be above 30000 and unique to your setup.  
if every is gone well you'll see this on your terminal:  
![](http://i.imgur.com/5K5WVOG.png)  
  
and now you can press CTRL + A + D on your keyboard to detach screen. And Plex Requests is installed and running on this address :  
  

    http://username.server.feralhosting.com:portnumber

  

