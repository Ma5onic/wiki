Downloading Torrent Data via HTTP
=================================

You'll need to execute some commands via SSH (secure shell). If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12). Commands are kept as simple as possible and in most cases will simply need to be copied and pasted into the terminal window (then executed by pressing the `Enter` key).  
  
This guide will help you to download your torrent data from the client via HTTP, so you can download through your browser if you like. This might be particularly useful if your ISP applies quality of service measures (i.e. throttling) on FTP traffic, since HTTP traffic is typically prioritised.  
  
  

Creating Symbolic Links
-----------------------

To download via HTTP you'll need to put the thing to download in your public\_html folder. You could copy/move the data directly but that has several downsides, so the easiest way is to use symbolic links.  
  
Firstly, create a links directory using this command:  
  

    mkdir -p ~/www/$(whoami).$(hostname -f)/public_html/links

  
Then we can add the relevant symbolic links for your torrent client using these commands. You can link to more than one torrent client if you like. Please note that the links assume the default location for the torrent client's data directory:  
  
rTorrent  

    ln -s ~/private/rtorrent/data/ ~/www/$(whoami).$(hostname -f)/public_html/links/rtorrent_data

  
Deluge  

    ln -s ~/private/deluge/data/ ~/www/$(whoami).$(hostname -f)/public_html/links/deluge_data

  
Transmission  

    ln -s ~/private/transmission/data/ ~/www/$(whoami).$(hostname -f)/public_html/links/transmission_data

  
  

Accessing Your Page
-------------------

Anything in public\_html can be accessed by appending it to your base URL. This base URL will change depending on whether you want HTTP or HTTPS - for HTTP you would use the following:  
  

    http://username.server.feralhosting.com/

  
For HTTPS it would be:  
  

    https://server.feralhosting.com/username/

  
In both cases *username* is replaced with your username and *server* is replaced by your server name.  
  
By default you will access the symbolic links via HTTP but you can follow the linked-to guide in the section below, "Using HTTPS" if you wish to connect securely.  
  
  

Password Protecting
-------------------

It's a good idea to password protect your links directory to stop it being accessible to anyone and everyone - including web crawlers. There is a guide to password protecting your links directory with an easy-to-use bash script on [this](https://www.feralhosting.com/faq/view?question=22) page.  
  
  

Using HTTPS
-----------

By default you'll be redirected to the HTTP version of your links page. You can change this and force traffic to be sent and received over HTTPS by using [this](https://www.feralhosting.com/faq/view?question=161) guide.  
  
Please note that the certificates here at Feral currently cover feralhosting.com and *server*.feralhosting.com but do not cover *username*.*server*.feralhosting.com.  
  

