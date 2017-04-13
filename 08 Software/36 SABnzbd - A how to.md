SABnzbd - A how to
==================

**Please note that this software is not officially supported by Feral Hosting.**  
  
**1:** Download SABnzbd from [here](http://sabnzbd.org/download/) to your slot. You can do this either by downloading it on your computer and then uploading it using FTP/SFTP, or with the following command on your server using SSH:  
  

    wget -qO ~/SABnzbd.tar.gz https://github.com/sabnzbd/sabnzbd/releases/download/1.1.0/SABnzbd-1.1.0-src.tar.gz

  
**2:** Extract the files from the archive.  
  

    tar xf ~/SABnzbd.tar.gz

  
**3:** Edit the command needed to run SABnzbd.py and then run it.  
  
This is the command you will need to edit:  
  

    screen -fa -dmS sabnzbd python ~/SABnzbd-*/SABnzbd.py --browser 0 --server $(hostname -f):PORT --https PORT

  
Please replace each `PORT` with a different number between **6000** and **50000**. Putting the https port one port above or below is easiest. Press enter to execute the command.  
  
If you pick the same port as someone else for either http or https you'll see problems:  
  
1) You might get an error message, or;  
2) When you try to access it through your browser you'll be greeted with a password prompt for someone else's SABnzbd  
  
In either case you'll need to kill the process and start it using a different port.  
  
You will be required to accept the invalid certificate in order to connect to the https port.  
  
For example:  
  

    screen -fa -dmS sabnzbd python ~/SABnzbd-*/SABnzbd.py --browser 0 --server $(hostname -f):12345 --https 12346

  
**4:** Access SABnzbd through your browser.  
  
**Important note:** Make sure to use the https port in the URL,  
  

    https://server.feralhosting.com:PORT/sabnzbd/

  
For example:  
  

    https://peterpan.feralhosting.com:12346/sabnzbd/

  
You won't have been given  
  
**5:** Follow the SABnzbd wizard to set up your Usenet account.  
  
**Make sure you set-up a username and password under `Config > General`**  
  
**6:**  You'll need to make 3 folders, you can make the top level 'downloads' folder wherever you wish:  
  

    downloads

  
Inside this new folder make another 2 folder with these names:  
  

    complete

  

    incomplete

  
(**Note, the two subfolders are required**)  
  
Make sure you've set the proper path to these under `Config` in the web interface. **You will need to use the full path**. Below you'll find a sample path:  
  

    /media/DiskID/home/username/private/sab/downloads/

  
Connecting in SSH and restarting sabnzbd  
----  
  
**Attach to the screen:**  
  
To the screen process using this command:  
  

    screen -r sabnzbd

  
**Kill the screen:**  
  
Use this command to kill the screen and the process if needed:  
  

    screen -S sabnzbd -X quit

  
**Restart  the screen**  
  
You can restart it using just this command once you have used the main command above once as it configures the `ini` file.  
  

    screen -fa -dmS sabnzbd python SABnzbd-*/SABnzbd.py

  
**Added NZB's don't download**  
  
There's a bug in SabNZB that will prevent things from downloading if there's a `www-browser` session running in the background. You can check for and quit any `www-browser` with the below"  
  

    ps x | grep www-browser | grep -v grep

  
If this returns a line containing "www-browser" run the below  
  

    killall -9 -u $(whoami) www-browser

  
  

