PHP - modify settings
=====================

  

Apache and Nginx php settings using local php.ini
-------------------------------------------------

  
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)  
  

### Bash Script

  
This bash script will do these things for you.  
  
**1:** Install the Apache php.ini and configure the default mysql, mysqli and pdo sockets.  
**2:** Install the nginx php.ini and configure the default mysql, mysqli and pdo sockets.  
**3:** Reload Apache with immediate effect.  
**4:** Reload nginx and php-fpm with immediate effect.  
  

    wget -qO ~/phpsettings http://git.io/hGdl && bash ~/phpsettings

  
Once you have used the script you can now edit and save your php.ini at:  
  
Apache = `~/.apache2/php.ini`  
  

    nano ~/.apache2/php.ini

  
nginx = `~/.nginx/php/php.ini`  
  

    nano ~/.nginx/php/php.ini

  
**Important note:** The default mysql, mysqli and pdo socket settings are already set to your local socket path by the script.  
  
When you have finished editing the `php.ini` you can use the script to reload Apache or Nginx.  
  

Apache using htaccess
---------------------

  
In your `.htaccess` files you can add these lines and change the paths or numbers to match yours:  
  
**Important note:** `.htaccess` files work recursively from their current location. If you want some settings to apply to the entire server put these settings in a `.htaccess` in your server root. If you only need them to apply to certain directories, place the settings in a `.htaccess` within those directories.  
  
This is an example of the `.htaccess` in your server root.  
  
Where `username` is your Feral username and `server` is the name of the server your slot is hosted on.  
  

    ~/www/username.server.feralhosting.com/public_html/.htaccess

  
**Default Socket setting**  
  

    php_value mysql.default_socket "/media/DiskID/home/username/private/mysql/socket"
    php_value mysqli.default_socket "/media/DiskID/home/username/private/mysql/socket"

  
Will make it so `localhost` uses these socket paths.  
  
If networking has been enabled in your `~/private/mysql/my.conf` you can also set these:  
  
**Default port settings**  
  

    php_value mysql.default_port 23456
    php_value mysqli.default_port 23456

  
This will define the default port.  
  
**Modifying other settings:**  
  
The basic concept is this:  
  

    php_value some_setting value/path

  
For example:  
  

    php_value max_execution_time 100

  
This will change the default value from 30 to 100  
  
**Max file upload size**  
  

    php_value upload_max_filesize 100M
    php_value post_max_size 100M
    php_value max_input_time 300
    php_value max_execution_time 300
    php_value memory_limit = 100M

  
Will allow larger file uploads, up to `100M`.  
  

