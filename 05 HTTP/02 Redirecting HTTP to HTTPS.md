Redirecting HTTP to HTTPS
=========================

  
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)  
  

### Dual URL format force HTTPS

  
This guide will help you force HTTPS usage on your default domains, independent of one another, at the same time.  
  
First, please navigate to your `public_html` folder (replacing username and server with the relevant details) via FTP or SFTP:  
  

    ~/www/username.server.feralhosting.com/public_html/

  
Second, create a file called **.htaccess** and place the following inside it:  
  
You **DO NOT** need to edit this code before it will work for you  
  
To edit in SSH do:  
  

    nano -w ~/www/$(whoami).$(hostname -f)/public_html/.htaccess

  
Then copy an paste this code below:  
  

    RewriteEngine on
    #
    RewriteCond %{HTTP:X-Forwarded-Proto} !https
    RewriteCond %{HTTP:x-HOST} ^.+\..+\.feralhosting\.com$ [NC]
    RewriteRule ^.*$ https://%{HTTP:X-Host}%{REQUEST_URI} [R,L]
    #
    RewriteCond %{HTTP:X-Forwarded-Proto} !https
    RewriteCond %{HTTP:x-HOST} ^.+\.feralhosting\.com$ [NC]
    RewriteRule ^.*$ https://%{HTTP:X-Host}/%{ENV:USER}%{REQUEST_URI} [R,L]

  
The press and hold `CTRL` then press `x` to save. Press `y` to confirm.  
  
Run this `chmod` command in SSH no matter how you created the file:  
  

    chmod 644 ~/www/$(whoami).$(hostname -f)/public_html/.htaccess

  
If you are still unsure here is an example you can paste into your `.htaccess` on pastebin.  
  
Once saved it should happen almost immediately. Though you might have to clear your history/cache and/or restart the browser to see the change in some cases.  
  
This will work for both URL formats at the same time:  
  
`http://username.server.feralhosting.com` to `https://username.server.feralhosting.com`  
  
and  
  
`http://server.feralhosting.com/username` to `https://server.feralhosting.com/username`  
  

### Force all HTTP to `https://server.feralhosting.com` only

  
If you would like to force all traffic to only:  
  

    server.feralhosting.com/username

  
**Be Warned:** this will effectively lock you out of the `username.server.feralhosting.com` URL format, breaking or locking you out of many Web-apps and usages of your `www`.  
  
Then use this code instead.  
  

    RewriteEngine on
    #
    RewriteCond %{HTTP:X-Forwarded-Proto} !https
    #
    RewriteCond %{HTTP:x-HOST} ^(.+\.)?(.+)\.feralhosting\.com$ [NC]
    RewriteRule ^.*$ https://%{ENV:APACHE_HOSTNAME}/%{ENV:USER}%{REQUEST_URI} [R,L] 
    RewriteCond %{HTTP:x-HOST} ^(.+\.)(.+)\.feralhosting\.com$ [NC]
    RewriteRule ^.*$ https://%{ENV:APACHE_HOSTNAME}/%{ENV:USER}%{REQUEST_URI} [R,L] 

  
There are two rules we need to force `https://server.feralhosting.com`  
  
`http://server.feralhosting.com/username/` to `https://server.feralhosting.com/username`  
  
`http://username.server.feralhosting.com/` to `https://server.feralhosting.com/username`  
  

### Fix password protected folders

  
Now after applying the above steps, you'll be asked twice for your credentials when accessing an authentication-requiring folder like ruTorrent via HTTP.  
  
You can fix this easily by enclosing the authentication by a `<FilesMatch ".">` block.  
  
For example, this is how your .htaccess file in your ruTorrent folder should look like:  
  

    <FilesMatch ".">
    AuthType Basic
    AuthName "username"
    AuthUserFile "path to .htpasswd"
    Require valid-user
    </FilesMatch>

  
That's it. This will also improve security, as the credentials won't be sent in plaintext via HTTP.  
  

### nginx

  
This will force HTTPS usage on your default domains, independent of one another, at the same time.  
  
Execute this command in SSH to have the required files automatically created and nginx restarted.  
  

    wget -qO ~/nginxhttps.sh http://git.io/A34SpA && bash ~/nginxhttps.sh

  
  

