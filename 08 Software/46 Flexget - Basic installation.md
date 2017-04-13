Flexget - Basic installation
============================

**Please note!** Though this software runs in nearly all cases without problems, Feral cannot provide much support for its use or help should anything go wrong. Please make sure you've read this FAQ fully as help on the problem may be covered already.  
  
This notice absolutely does not prevent you from raising a ticket should anything go wrong but please bear in mind staff may not be able to assist beyond basic troubleshooting (for example restarting, clarifying error messages and so on).  
  

Preparation
-----------

You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  
  

Installation - using virtualenv
-------------------------------

Flexget suggests the use of a virtual environment in its installation guide. To install using this method please execute these commands:  
  

    pip install --user --ignore-installed --no-use-wheel virtualenv
    ~/.local/bin/virtualenv ~/flexget/
    ~/flexget/bin/pip install flexget
    touch ~/config.yml

  
The final command executed will create an empty file called config.yml on your slot (at home level). This is done because creating via virtualenv does not automatically create a config.yml file. The command will not overwrite the contents of config.yml if it already exists.  
  
  

Installation - using pip
------------------------

It's also possible to install using pip. This might be necessary if you wish to use Flexget's deluge plugin rather than simply passing it to Deluge's watch directory.  
  

    pip install --user --ignore-installed --no-use-wheel flexget
    touch ~/config.yml

  
The final command executed will create an empty file called config.yml on your slot (at home level). This is done because creating via virtualenv does not automatically create a config.yml file. The command will not overwrite the contents of config.yml if it already exists.  
  
  

Configuring
-----------

Configuring the config.yml to download series is not covered in this guide. The [Flexget website](http://flexget.com/wiki/Configuration) has lots of resources and beginner guides to get you started. **Please note:** staff are not able to configure your config.yml for you.  
  
The only configuration covered in this guide is passing to the various torrent clients supported at Feral. This is only needed if you wish to pass additional options to the client. Otherwise, it should be fine to simply specify the watch directory and let the client manage the torrent.  
  
  

### rTorrent

First of all you need to obtain the path to the rTorrent socket. For this, simply execute this command:  

    echo $(pwd)/private/rtorrent/.socket

  
Here is an example of a dummy guide using variables instead of actual values:  
  

    tasks:
      task1:
        rss: rss feed URL
        series:
          - series name
        rtorrent:
          uri: path_to_socket

  
As you might imagine, replace *path\_to\_socket* with the path you got from the first command.  
  
  

### Deluge

If you install Flexget to virtualenv you'll likely encounter an error stating that dependency \`deluge\` is missing. For this reason you'll need to install via pip --user (please see the second installation guide near the top of this page).  
  
In preparation you need to obtain the port that deluge is listening on. To get this simply execute the following command:  
  

    grep daemon_port ~/.config/deluge/core.conf

  
Here is an example of a dummy guide showing the layout. It uses variables rather than proper port numbers.  
  

    tasks:
      task1:
        rss: rss feed URL
        series:
          - series name
        deluge:
          port: deluge_port

  
Simply replace *deluge\_port* with the number you got from the command above. Only the port is needed - flexget should be able to read the auth file for a username and password from the default location, but if you don't specify the port it will try to connect on port 58846.  
  
  

### Transmission

  
To use directly with transmission you first need to install and configure transmissionrpc. This is done by executing these commands:  
  

    pip install --user transmissionrpc
    sed -i "s|base_url + '/t|base_url + '/$(whoami)/t|g" ~/.local/lib/python2.7/site-packages/transmissionrpc/client.py

  
Here is an example of a dummy guide showing the layout. It uses variables rather than proper port numbers.  
  

    tasks:
      task1:
        rss: rss feed URL
        series:
          - series name
        transmission:
          host: server.feralhosting.com
          port: 80
          username: username
          password: password

  
Simply replace *server* with your server name, *username* with your username and *password* with your Transmission access password.  
  

Running flexget
---------------

Running flexget directly from its location will depend on the method you used to install it. If you followed the official method of creating a virtualenv then you can call it directly by executing:  
  

    ~/flexget/bin/flexget execute

  
If you installed it using pip you would need to call it by executing:  
  

    ~/.local/bin/flexget execute

  
Note that both of these methods will download data if properly configured and a match is found. If you don't want this to happen simply specify the --test option.  
  
  

Cron - running flexget automatically
------------------------------------

Cron is a method of running jobs at regular intervals or on special pre-defined occasions. To bring up the crontab editor use the following command:  
  

    crontab -e

  
If this is your very first time you'll be given a choice of editors. Nano is fine to use so unless you specifically want something else just press enter.  
  
There will already be some basic information on crontabs in the file - you can keep it if you like, or get rid of it if you prefer. The lines are commented out so are for information purposes only and don't affect any cron jobs added.  
  
At a new line in the file copy-paste the following:  
  

    */10 * * * * flexget_path --cron execute

  
You must replace *flexget\_path* with the location of the flexget binary (that could be `~/flexget/bin/flexget` or `~/.local/bin/flexget`).  
  
The example cron job above will run Flexget every 10 minutes. You can reduce that if you like but it's in your interest to respect the tracker rules on this. If you don't know what they prefer it's best to ask (Feral will not assist circumventing a tracker ban).  
  

Troubleshooting
---------------

*On executing Flexget I get a permission denied error on /tmp/safe-0.4.words.cache*  
Somebody else is using Flexget and writing there, so your instance will not be able to. You'll need to set the TMPDIR variable. You can export it each time ir set it as an alias for ease of use. To set it in .bashrc execute these commands:  
  
For installation via virtualenv  

    mkdir ~/tmp
    echo "alias flexget='TMPDIR=$HOME/tmp ~/flexget/bin/flexget'" >> ~/.bash_aliases
    source ~/.bash_aliases

  
For installation via pip  

    mkdir ~/tmp
    echo "alias flexget='TMPDIR=$HOME/tmp ~/.local/bin/flexget'" >> ~/.bash_aliases
    source ~/.bash_aliases

  
You can then just use flexget from your slot to run it (options such as --test will still work with the alias).  
  
*When I try to connect with deluge there's a message that dependency \`deluge\` is missing*  
This will either be because Deluge is not installed or because you're using the virtualenv. Firstly, please consider whether or not you could simply specify the path to Deluge's watch folder instead. If you need to use deluge plugin, please install using the pip --user method.  
  
*When trying to install Flexget using pip I get an error "ImportError: cannot import name IncompleteRead"*  
Please try installing pip using these commands before trying to install Flexget again:  
  

    easy_install --install-dir=~/.local/lib/python2.7/site-packages pip

  
  

