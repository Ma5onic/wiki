ruTorrent Plugin - Unpack
=========================

Installing Unpack
-----------------

If you're using 3.6 of ruTorrent (which is the default version installed here at Feral) you won't be able to use the general plugin install method described on [this page](https://www.feralhosting.com/faq/view?question=282). Instead, execute these commands:  
  

    rm -rf ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/unpack
    wget -q https://bintray.com/novik65/generic/download_file?file_path=plugins%2Funpack-3.6.tar.gz
    tar xf download_file\?file_path\=plugins%2Funpack-3.6.tar.gz -C ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/
    rm download_file\?file_path\=plugins%2Funpack-3.6.tar.gz

  
The first command removes any existing instance of unpack in case you previously installed an incorrect version. Naturally if you are using the 3.7 version of ruTorrent then you can install unpack by following the general plugin install method.  

