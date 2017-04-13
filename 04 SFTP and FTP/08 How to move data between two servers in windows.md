How to move data between two servers in windows
===============================================

Moving data between two servers with FTP without downloading it to your local computer first is called an *FXP transfer*. For you to be able to transfer data this way, FXP mode must be enabled on both servers â€” the server you are transferring to and the one you are transferring from. FXP is enabled on your Feral server by default.  
  
You need your login details to both servers. You can find your Feral access details on your [Software Status page](https://www.feralhosting.com/heron/manager/software/). Make sure you use the drop-down box to switch between different servers.  
  
Download [FTPRush](http://www.ftprush.com/download.html) for example, open it and it will look like this:  
  
Now you have two windows open: on the right you see your local data, and on left you see a blank window. Now go to Tools &gt; Site Manager &gt; Click "Sites" &gt; File &gt; New &gt; New Site &gt; Type the name for your first site and press OK. Now put your login in this window and click OK.  
  
Now do the same for that other server as well.  
  
Now switch from local view to remote using this button:  
  
Now connect to both of those servers and go to your torrent clients data folder:  
  
Now choose all folders and files and just drag-and-drop them into that other window (server) and it will start fxp'ing the files right away.  
  
**Important note:** It is not possible to transfer files between FTP and SFTP servers, or between two SFTP servers.  

