rclone - Cloud Service Syncing
==============================

How to Install and Use rclone to Sync Files With Cloud Services
===============================================================

  
You can use rclone with many cloud services for uploading, downloading, and syncing your files.  
  
Rclone supports the following cloud services:  
- Amazon Cloud Drive (ACD)  
- Google Drive  
- Amazon S3 (Not ACD)  
- Openstack Swift / Rackspace cloud files / Memset Memstore  
- Dropbox  
- Google Cloud Storage (Differnt then Google Drive)  
- Microsoft One Drive  
- Hubic  
- Backblaze B2  
- Yandex Disk  
- The local filesystem  
  

Installation
------------

  
  
First download [rclone](http://rclone.org/downloads/):  
  

    mkdir -p ~/bin; cd; wget http://downloads.rclone.org/rclone-current-linux-amd64.zip -O ./bin/rclone.zip

  
  
Unzip rclone  
  

    unzip ./bin/rclone.zip

  
  
Now move the rclone file  
  

    mv ./rclone-*-linux-amd64/rclone ./bin/

  
  
Delete the old files  
  

    rm -rf ./rclone-*-linux-amd64/

  

    rm ./bin/rclone.zip

  
  
You're done installing. Go ahead and setup your cloud service:  
  
\[h2\]Amazon Cloud Drive (ACD)\[h2\]  
  
Configure rclone  
  

    rclone config

  
  
Now add your remote  
  

    n

  
  
Enter Your Desired Name, for Amazon Cloud Drive, I suggest just putting acd  
  

    acd

  
  
Storage:  
  

    1

  
  
For client\\\_id and client\\\_secret, leave blank (just press enter)  
  
Now since were working on a headless machine say no  
  

    n

  
  
Now for Amazon Cloud Drive setup, you need to install rclone on your local machine  
  

Windows
-------

  
  
On Windows, download the windows file here: <http://downloads.rclone.org/rclone-current-windows-amd64.zip>  
  
Unzip the files to your desired location, then open cmd and navigate to that location  
  

    cd /<path>/rclone-v1.29-windows-amd64/

  
  
Now authorize ACD  
  

    rclone.exe authorize "amazon cloud drive"

  
  
The authorization page will open in your defualt web browser, login with your amazon account and return to the cmd window.  
  
Now, copy the code between "Paste the following code into your remote machione ---&gt;" and "&lt;---End Paste"  
  
If you are having issues coping the code, right click and click "Select all". Then go to pastebin.com and paste it. Now copy the code between "Paste the following code into your remote machione ---&gt;" and "&lt;---End Paste". You can close the pastebin tab.  
  
Paste the code in your server's window  
  
Save the remote  
  

    y

  

    q

  
  

Linux
-----

  
  
Download the appropriate files from the rclone download page: <http://rclone.org/downloads/>  
  
Now enter these commands with your info where it should go  
  

    unzip rclone-v1.17-linux-amd64.zip
    cd rclone-v1.17-linux-amd64
    sudo cp rclone /usr/sbin/
    sudo chown root:root /usr/sbin/rclone
    sudo chmod 755 /usr/sbin/rclone
    sudo mkdir -p /usr/local/share/man/man1
    sudo cp rclone.1 /usr/local/share/man/man1/
    sudo mandb 

  
  
Now setup your Remote  
  

    rclone authorize "amazon cloud drive"

  
  
The authorization page will open in your defualt web browser, login with your amazon account and return to the cmd window.  
  
Now, copy the code between "Paste the following code into your remote machine ---&gt;" and "&lt;---End Paste"  
  
If you are having issues coping the code, right click and click "Select all". Then go to pastebin.com and paste it. Now copy the code between "Paste the following code into your remote machine ---&gt;" and "&lt;---End Paste". You can close the pastebin tab.  
  
Paste the code in your server's window  
  
Save the remote  
  

    y

  

    q

  
  
Your all done! See below for rclone useage  
  

Google Drive
------------

  
  
Configure rclone  
  

    rclone config

  
  
Now add your remote  
  

    n

  
  
Enter Your Desired Name, for Google Drive, I suggest just putting gdrive  
  

    gdrive

  
  
Storage:  
  

    6

  
  
For client\\\_id and client\\\_secret, leave blank (just press enter)  
  
Now since were working on a headless machine say no  
  

    n

  
  
Now copy the link your given by rclone and go to it in your browser, login to your Google account, click "Allow"  
  
You will key a textbox with a key, copy the key and paste it into rclone  
  
Now save the remote  
  

    y

  

    q

  
  
Your all done, see below for usage  
  

Usage
-----

  
  
To Upload by Copying  
  

    rclone copy /path/to/file <remote name>:<remote path>

  
  
To Upload by Moving  
  

    rclone moving /path/to/file <remote name>:<remote path>

  
  
To Upload by Sync (Won't upload already uploaded files)  
  

    rclone sync /path/to/file/ <remote name>:<remote path>

  
  
To ls your cloud service  
  

    ls <remote name>:<remote path>
    lsd <remote name>:<remote path>
    lsl <remote name>:<remote path>

  
  
To delete  
  

    rclone delete <remote name>:<remote path>

  
  
For more commands and help  
  

    rclone help

  

