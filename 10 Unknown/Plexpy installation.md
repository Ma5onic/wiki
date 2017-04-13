Plexpy installation
===================

In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH Guide - The Basics](https://www.feralhosting.com/faq/view?question=12)  
  
Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)  
  
You login information for the relevant slot will be shown here:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)  
  

Installing PlexPy
-----------------

  
Run these commands to install and launch PlexPy. The commands also put PlexPy into a screen.  
  

    git clone https://github.com/drzoidberg33/plexpy.git
    sed -i 's|http_port = 8181|http_port = '$(shuf -i 10001-32001 -n 1)'|g' ~/plexpy/config.ini
    screen -dmS plexpy python ~/plexpy/PlexPy.py

  
Then, do this command to complete the setup of PlexPy:  
  

    screen -r plexpy

  
The reason for the screen is to keep it running when you close the SSH connection. Once you're done in the screen you can get out of it by pressing `ctrl + a + d`. In other words, hold down `ctrl` and press `a` and with both those held down still, press `d`.  

