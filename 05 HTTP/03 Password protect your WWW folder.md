Password protect your WWW folder
================================

In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH Guide - The Basics](https://www.feralhosting.com/faq/view?question=12)  
  
**Important notes:** Please see the end of the FAQ for nginx.  
  

Htpasswd toolkit Bash script
----------------------------

  
This bash script provides some easy options to perform some common tasks.  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/bashscript.png)  
  
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH Guide - The Basics](https://www.feralhosting.com/faq/view?question=12)  
  

    wget -qO ~/htpasswdtk.sh http://git.io/eJySww && bash ~/htpasswdtk.sh

  
This script will also get the latest version and copy it to your `~/bin` directory and make it executable.  
So after you have run it for the first time you can simply do:  
  

    htpasswdtk

  

How it works:
-------------

  

### Apache:

  
You create a file called a `.htaccess` inside a directory in your WWW folder. You then populate this file with special instructions that Apache will interpret and apply to the web-server.  
  
For password protecting a directory you must use the `.htaccess` in tandem with a `.htpasswd` file that stores the username and password information for created users.  
  
So the `.htaccess` stores the setup information for the authentication that will look to a special `.htpasswd` file for the required user credentials.  
  

### Nginx:

  
nginx does not use `.htaccess` files therefore you must use `conf` files and reload the web-server for the changes to take effect.  
  
Configurations settings are stored in the `conf` files loaded by nginx from this location:  
  

    ~/.nginx/conf.d/000-default-server.d

  
So the `conf` file stores the set-up information for the authentication using location based directives that will look to a special `.htpasswd` file for the required user credentials.  
  

Section 1: Apache - creating our .htaccess
------------------------------------------

  
**Step 1:** In SSH we must first navigate to the directory we want to protect and then create the `.htaccess`.  
  

    cd ~/www/$(whoami).$(hostname -f)/public_html/

  
This will move us into the root of our `WWW` folder  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htaccess_0.png)  
  
This command will either open an existing file or create the new file upon saving using a text editor called nano, so now type:  
  

    nano -w .htaccess

  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htaccess_1.png)  
  
It will look something like this if you are doing this for the first time.  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htaccess_2.png)  
  
Now below is the info we are going to fill this file with but it it not ready yet. Open a text editor such as [NotePad ++](http://notepad-plus-plus.org/) and edit it to reflect your unique settings such as username and paths. This is information for ONE user, YOU. We will see how to add users later on in Section 3.  
  

    AuthName "Secure Area"
    AuthType Basic
    AuthUserFile /media/DISKID/home/username/private/.htpasswd

    require user username

  
**Important note:** Your full path may be a little different (your disk ID will not be in capital letters and your path may not contain home):  
  

    AuthUserFile /media/DiskID/username/private/.htpasswd

  
Use this command in [SSH](https://www.feralhosting.com/faq/view?question=12) to check your path:  
  

    echo $HOME

  
For example, this command will give the full path to a particular directory  
  

    ls -d ~/private/.htpasswd

  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htaccess_3.png)  
  
Once you have done this copy the text to your clipboard, then back in the SSH window press press `SHIFT + INS` (or right mouse-click in PuTTy or KiTTy) to paste it into your nano window  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htaccess_4.png)  
  
As you can see, we are telling `.htaccess` 2 things:  
  
**1:** Where to look for the file containing the password, in this case it is called `.htpasswd`  
  
**2:** What user to authenticate with that password.  
  
We are done with creating our `.htaccess` file. Press and hold `CTRL` then press `x` to save and exit nano. It will ask: Save modified buffer? Press `Y` to save changes, and then `ENTER` to confirm.  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htaccess_5.png)  
  
Now press enter to save it with the correct filename.  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htaccess_6.png)  
  
We now need to change permissions on the file. Type:  
  

    chmod 600 .htaccess

  
As long as you are still in this `public_html` directory  
  
The system will respond with a blank line.  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htaccess_7.png)  
  
That is it. You have successfully created you `.htaccess` file. Time to do the `.htpasswd`  
  

### Final Notes for Section 1:

  
I recommend you place the `.htaccess` file only INSIDE the folders you wish to protect, you can do this via FTP(SFTP). This will let you give free access to some folders in your `WWW` but hide any that contain this `.htaccess` we just created.This means anyone can access the `WWW` folder, but cannot access folders restricted by your `.htaccess`  
  
**Important note:** To allow users access to only some folders and not others please see **Final Notes Section 3:**  
  
To change our own password or other users inside an existing `.htpasswd` see Section 2.1  
  

Section 2: Creating our .htpasswd file
--------------------------------------

  
**Important notes:** Please use a good password where the at least the first 8 characters are not easily guessable. A combination of Letters, numbers and mixed case will be perfect, for example: **dHr6wY7l** and so on.  
  
**Step 2:** Let's now create our `.htpasswd` file. First we navigate to the Directory where we want to store it (we configured it earlier in our `.htaccess` file):  
  

    cd ~/private

  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_0.png)  
  
Now type:  
  

    htpasswd -cm .htpasswd username

  
Use the same username that you configured earlier in `.htaccess`. The system will ask you to type in your desired password:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_1.png)  
  
You can use your own password, ( remember the info at the start of the guide about password managers and Chrome).  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_2.png)  
  
Type it or Paste it but remember you will not see anything as you type or that you pasted, that is normal. Press **enter** You will be asked to re-type your password, after which `.htpasswd` will be created.  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_3.png)  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_4.png)  
  
We now need to change permissions on this file, too. Type:  
  

    chmod 600 .htpasswd

  
This will `chmod` a file by the name of `.htpasswd` to `600` in our current location, in this case that is `~/private`  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_5.png)  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_6.png)  
  
And this is it. You have passworded your WWW directory for a single user.  
  

### Final Notes for Section 2:

  
I recommend you place the `.htaccess` file only INSIDE the folders you wish to protect, you can do this via FTP(SFTP). This will let you give free access to some folder in your WWW but hide any that contain this `.htaccess` we just created.This means anyone can access the WWW folder, but cannot access folders restricted by your `.htaccess`  
  
To allow users access to only some folders and not others please see the **Final Notes Section 3:** section  
  
**Important notes:** If you receive an `Internal Server Error` message when you try to access your page/directory, check for typing errors in your `.htaccess` file.  
  
To un-protect a directory, delete the `.htaccess` and the `.htpasswd` files, or just rename the `.htaccess` file to `.htaccess_off`  
  

Section 2.1 Adding users
------------------------

  
This will be what your `.htaccess` looks like.  
  

    AuthName "Secure Area"
    AuthType Basic
    AuthUserFile /media/sde1/home/exampleuser/private/.htpasswd

    require user exampleuser

  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_adduser_0.png)  
  
What we need to dis is add a new authorised user to access this directory.  
  

    AuthName "Secure Area"
    AuthType Basic
    AuthUserFile /media/sde1/home/exampleuser/private/.htpasswd

    require user exampleuser
    require user guestuser

  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_adduser_1.png)  
  
Alternatively you can allow all valid users to access the directory. This will allow any user present in the .`htpasswd` file to access the protected directory. This simplifies the process for multiple users but will all anyone in the `.htpasswd` to access the directory.  
  

    AuthName "Secure Area"
    AuthType Basic
    AuthUserFile /media/sde1/home/exampleuser/private/.htpasswd

    require valid-user

  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_adduser_2.png)  
  
To change your own password inside an existing `.htpasswd` you must use the `.htpasswd` command. Replace `exampleuser` in the below command for the name of the user you wish to change/update the password for.  
  

    htpasswd ~/private/.htpasswd exampleuser

  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_adduser_3.png)  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_adduser_4.png)  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_adduser_5.png)  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_adduser_6.png)  
  
**Section 3: Password Protecting a Directory for Multiple Users**  
  
To give multiple users access to one or more directories we must do two things. Assuming you have followed the steps in this guide we will add a new user to our `.htaccess` and give them a password by editing the `.htpasswd`.  
  
**Step 1:** To add your own users please edit the `.htaccess` file and add your user as shown in section `2.1` first to allow your specific user or to all all valid users.  
  
**Step 2:** Then use this command to add the new user to the `.htpasswd`, where you change `guestuser` to the name of the user you wish to add:  
  

    htpasswd ~/private/.htpasswd guestuser

  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_update_0.png)  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_update_1.png)  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_update_2.png)  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/HTTP/Password%20protect%20your%20WWW%20folder/htpasswd_update_3.png)  
  
**Final Notes Section 3:**  
  
To deny a user access to a folder you do no have to delete them from the `.htpasswd`. All you have to do is remove their user name from the `.htaccess` in the folders you do not wish them access to, so for example.  
  

    require user exampleuser

  
Only `exampleuser` will have access to this folder. other users will not even see it exists. When a user visits your `WWW` folder they will only see and access folders that have their username in the `.htaccess` using our configuration.  
  
**Section 4: Rutorrent Specific Info**  
  
The guide tells you everything you need to know in detail on how to change/create the settings/files you need. This is just to tell you where the relevant files if you wish to use the existing Rutorrent `.htaccess` and `.htpasswd`  
  
Apache:  
  
The `.htaccess` is located here:  
  

    ~/www/username.server.feralhosting.com/public_html/rutorrent/.htaccess

  
The `.htpasswd` is located here.  
  

    ~/www/username.server.feralhosting.com/public_html/rutorrent/.htpasswd

  
nginx:  
  
The `rutorrent.conf` is located here:  
  

    ~/.nginx/conf.d/000-default-server.d/rutorrent.conf

  
The `.htpasswd` is located here.  
  

    ~/www/username.server.feralhosting.com/public_html/rutorrent/.htpasswd

  
**Final Notes for Section 4:**  
  
**Important notes:** The ruTorrent `.htaccess` makes use of  
  
You can change the rutorrent `.htaccess` to link to another `.htpasswd` of your choosing (one created in Section 2 for example) by editing the file as described in Section 1.  
  
In this case the `.htpasswd` is stored within the `WWW` realm and not outside it (like the `.htpasswd` from Section 2 is). Moving this to somewhere outside the `WWW` is a good idea.  
  

nginx
-----

  
nginx does not use `.htaccess` files. All settings are done in the configuration files.  
  
All locations are relative to the WWW root which is always:  
  

    ~/www/username.server.feralhosting.com/public_html/

  
Or if you added a VHost:  
  

    ~/www/somesite.co.uk/public_html/

  
You nginx configuration files stored here:  
  

    ~/.nginx/conf.d/000-default-server.d

  
Create a new conf file and enter this information, for example:  
  

    nano -w ~/.nginx/conf.d/000-default-server.d/links.conf

  
Then copy this information into it:  
  

    location /links {
        auth_basic "Please log in";
        auth_basic_user_file /media/DiskID/username/path/to/.htpasswd;
    }

  
Where:  
  
`/media/DiskID/username/path/to/.htpasswd` reflects the actual full path to your `.htpasswd`. You can use the method described in the Apache section of this FAQ to generate and manage your `.htpasswd` files.  
  
The press and hold `CTRL` then press `x` to save. Press `y` to confirm.  
  
For example, to password protect your server root you would do this:  
  

    location / {
        auth_basic "Please log in";
        auth_basic_user_file /media/DiskID/username/path/to/.htpasswd;
    }

  
Where:  
  

    location /

  
Is specifying the server root and not a sub directory.  
  
Then save the edits to the `links.conf` and reload your nginx configuration for the settings to take effect.  
  

    /usr/sbin/nginx -s reload -c ~/.nginx/nginx.conf

  
**Important note:** Please note you may need to clear your browser cache for changes to reflected in your current browser session.  
  

Notes:
------

  
If you have an application, like Ampache, that has its own authentication you can disable basic auth for these location, if you have protected  your entire WWW for example.  
  
**Apache:**  
  
Add these two lines to a `.htaccess` inside the folder you wish to disable basic auth on. If the `.htaccess` does not exist in the desired location then create it.  
  

    Satisfy Any
    Allow from all

  
**nginx:**  
  
Create a location based rule in any existing conf file located at: `~/.nginx/conf.d/000-default-server.d/` or create a new one there just for this, for example:  
  

    ~/.nginx/conf.d/000-default-server.d/ampache.conf

  
Then add this to the file then save.  
  

    location /ampache {
        auth_basic  off;
    }

  
Then reload nginx using this command:  
  

    /usr/sbin/nginx -s reload -c ~/.nginx/nginx.conf

  

