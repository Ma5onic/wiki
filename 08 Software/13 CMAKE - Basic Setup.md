CMAKE - Basic Setup
===================

CMake is an open-source, cross-platform family of tools designed to build, test and package software. CMake is used to control the software compilation process using simple platform and compiler independent configuration files, and generate native makefiles and workspaces that can be used in the compiler environment of your choice.  
  
In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)  
  
Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)  
  
You login information for the relevant slot will be shown here:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)  
  

CMAKE installation
------------------

  
Use these first two commands to create to do some pre requisite tasks:  
  

    mkdir -p ~/bin && bash

  
**Important note** You can check here for the current version - <http://www.cmake.org/download/>  
  

### Binary Distribution Installation (Fast).

  

    wget -qO ~/cmake.tar.gz http://www.cmake.org/files/v3.2/cmake-3.2.2-Linux-x86_64.tar.gz
    tar xf ~/cmake.tar.gz --strip-components=1 -C ~/

  
Then test it works:  
  

    cmake --version

  

### Compile from Source Code

  
Install the program from source using these commands:  
  

    wget -qO ~/cmake.tar.gz http://www.cmake.org/files/v3.2/cmake-3.2.2.tar.gz
    tar xf ~/cmake.tar.gz && cd ~/cmake-3.2.2
    ./configure --prefix=$HOME
    make && make install
    cd && rm -rf cmake{-3.2.2,.tar.gz}

  
Then test it works:  
  

    cmake --version

  

Usage:
------

  
You can use this prefix to specify the directory you wish to install the program to.  
  

    cmake -DPREFIX=$HOME

  

Issues with CURL:
-----------------

  
When installing `weechat` for example, the curl location is not default so we must specify it. To do this though we must make sure it is not going to skip an important setting.  
  
Inside the directory of the application you wish to install there should be a file called `CMakeLists.txt`. Open this file and check for the line:  
  

    SET(CMAKE_SKIP_RPATH ON

  
If this line exists then remove it.  
  
This example is how `weechat` is installed on the slot when the script is used.  
  

    cmake -DCMAKE_INSTALL_RPATH=/opt/curl/current/lib -DPREFIX=$HOME -DCURL_LIBRARY=/opt/curl/current/lib/libcurl.so -DCURL_INCLUDE_DIR=/opt/curl/current/include

  
  

