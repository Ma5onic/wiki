Unrar - How to Install a Newer Version
======================================

Winrar - How to install a newer version than the slot version (3.90)  
  

    mkdir -p ~/bin && bash
    wget -qO ~/unrar.tar.gz http://www.rarlab.com/rar/unrarsrc-5.3.9.tar.gz
    tar xf ~/unrar.tar.gz && cd ~/unrar
    make && make install DESTDIR=~
    cd && rm -rf unrar{,.tar.gz}

  
You should now be able to use this program like this:  
  

    unrar

  
If you do not get version 5 + then log out then back into SSH.  

