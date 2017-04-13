Cron
====

Cron is a handy way of executing tasks on a schedule or at certain points. This guide will edit the crontab via SSH and will focus on two issues:  
  
1) Getting custom software started when the server is rebooted; and  
  
2) Running tasks repeatedly to a schedule  
  
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH Guide - The Basics](https://www.feralhosting.com/faq/view?question=12)  
  
Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)  
  
You login information for the relevant slot will be shown here:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)  
  

Bringing up the crontab editor
------------------------------

  
To bring up the crontab editor, simply copy-paste the following command:  
  

    crontab -e

  
If this is your very first time you'll be given a choice of editors. `Nano` is fine to use so unless you have other desires simply press enter.  
  
You'll be presented with this text:  
  

    # Edit this file to introduce tasks to be run by cron.
    #
    # Each task to run has to be defined through a single line
    # indicating with different fields when the task will be run
    # and what command to run for the task
    #
    # To define the time you can provide concrete values for
    # minute (m), hour (h), day of month (dom), month (mon),
    # and day of week (dow) or use '*' in these fields (for 'any').#
    # Notice that tasks will be started based on the cron's system
    # daemon's notion of time and timezones.
    #
    # Output of the crontab jobs (including errors) is sent through
    # email to the user the crontab file belongs to (unless redirected).
    #
    # For example, you can run a backup of all your user accounts
    # at 5 a.m every week with:
    # 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
    #
    # For more information see the manual pages of crontab(5) and cron(8)
    #
    # m h  dom mon dow   command

  
This provides some basic information on crontabs - you can keep it if you like, or get rid of it if you prefer. The lines are commented out so are for information purposes only and don't affect any cron jobs added.  
  

1 - Ensuring software starts up if the server reboots
-----------------------------------------------------

  
Sometimes a server might need to be rebooted. Though software like torrent clients, Plex and MySQL will get restarted automatically there are many common pieces of software which don't. A cron job will prevent you needing to manually restart things.  
  
Once in the editor, add the following line to a new line of the crontab:  
  

    @reboot $COMMAND

  
The special string @reboot means the command will be run at reboot. In our example, `$COMMAND` should be replaced with whichever command you wish to run.  
  
So, for instance:  
  

    @reboot screen -dmS autodl irssi

  
That will start up irssi for you and its screen can be reattached with `screen -r autodl`  
  

2 - Running things on a schedule
--------------------------------

  
A major use of cron jobs is to get things to run on a schedule. The various configurations are outside the scope of this quick quide so a couple of example (combined with the commented out text you get in the initial crontab, provided above) should be enough to get you going. Placeholders are used throughout - diskID, usernames and paths will need to be changed!  
  
This example will execute flexget every ten minutes:  
  

    */10 * * * * /media/diskID/username/flexget --cron execute

  
The following two are equivalent and will run a script called `script.sh` at midnight:  
  

    @daily /media/diskID/username/script.sh

  

    0 0 * * * /media/diskID/username/script.sh

  

