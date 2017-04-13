Using WinSCP to Sync Your Slot with Home (Windows)
==================================================

Easily sync your Server with your Windows PC  
  
Install WinSCP from the official site  
<http://winscp.net/eng/index.php>  
  
The main install includes the Command Line Options which we will be using.  
  
Just click Next Next Finish on the WinSCP and install as standard.  
  
We will create a .bat file to copy from our Slot to our home computer, this will only copy new content that is not on our home machine already.  
  
Open a new Notepad in windows and copy the following into the Notepad window replacing elements in curly braces { } with your information.  
  
winscp.com /command ^  
    "open s<ftp://>{username}:{password}@{slotname}.feralhosting.com/" ^  
    "get -neweronly /{location on your slot}/\* {homecomputerlocation}" ^  
    "exit"  
  
  
  
here is my example with the username & password removed.  
  
  
winscp.com /command ^  
    "open s<ftp://>{username}:{password}@dione.feralhosting.com/" ^  
    "get -neweronly /media/sdn1/home/{username}/.sickrage.tv.shows/\* D:\\Media\\TV\\" ^  
    "exit"  
  
  
We then save our notepad as a .bat file inside the folder we installed WinSCP.  
  
Then you can easily set this bat file to run via a scheduled task.  

