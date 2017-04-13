How to transfer files to Amazon Cloud Drive (ACD)
=================================================

To upload and download files to you Amazon Cloud Drive solution utilizing [adc\_cli](https://acd-cli.readthedocs.org/en/latest/) a lightweight command-line client for Amazon Cloud Drive (ACD), allowing you to access ACD storage from the command line.  
[Login to slot via ssh](https://www.feralhosting.com/faq/view?question=12)  
Below are detailed instruction and command that need to be run. Installation requires custom install of python with linked sql.  
Run this commands one by one and be patient it takes time  
  

    wget http://www.sqlite.org/2016/sqlite-autoconf-3130000.tar.gz
    tar xf sqlite-autoconf-3130000.tar.gz && rm sqlite-autoconf-3130000.tar.gz
    cd sqlite-autoconf-3130000/
    LDFLAGS="-L${HOME}/opt/lib" CFLAGS="-L${HOME}/opt/include" ./configure --prefix=$HOME/opt
    make && make install && cd
    mkdir -p ~/python/python3
    wget -qO ~/python.tar.xz  https://www.python.org/ftp/python/3.5.0/Python-3.5.0.tar.xz
    tar xf ~/python.tar.xz && cd ~/Python-3.5.0
    LD_RUN_PATH=$HOME/opt/lib ./configure --prefix=$HOME/python/python3 LDFLAGS="-L$HOME/opt/lib" CPPFLAGS="-I$HOME/opt/include"
    LD_RUN_PATH=$HOME/opt/lib make
    make install
    cd && rm -rf ~/python{-3.5.0,.tar.xz}
    ~/python/python3/bin/pip3 install --user --upgrade git+https://github.com/yadayada/acd_cli.git

  
  
One time authentication setup and database sync.  
  
Before using acd\_cli, you need to go through one-time authentication, where you authorize acd\_cli to access your Amazon Cloud Drive account via OAuth.  
  

    .local/bin/acd_cli init

  
  
You have two options:  
Login to <https://tensile-runway-92512.appspot.com> with Amazon credentials, follow prompts, at the end you will be presented with download "oauth\_data" file. Save on your local hard drive and the ftp upload to your\_user\_directory .cache/acd\_cli  
Second option:  
Follow prompts, fill out your amazon information, checkmark "always". Navigate using arrow key. After all information filled go up to login and press enter or right arrow you will be presented with your token, csave the plaintext response data into a file called "oauth\_data" in the directory ".cache/acd\_cli/"  
Now end amazon session by pressing "q".  
  
Before running any command with acd\_cli, you need to sync its local cache with your Amazon Cloud Drive account. Run  

    .local/bin/acd_cli sync

  
  
This completes setup.  
  
Using it. To see your Amazon Cloud Drive directory and usage:  

    .local/bin/acd_cli usage

  
Result will be like that  
*Documents:    966,    1.2 GiB  
Other:      10030,    6.8 TiB  
Photos:      5651,  30.4 GiB  
Videos:      3502,    1.2 TiB  
Total:      20149,    8.1 TiB*  
  
To list files in a folder:  

    .local/bin/acd_cli ls /Videos

  
  
To upload folder to ACD  

    .local/bin/acd_cli upload -x 2 -r 4 --deduplicate ~/folder_to_upload/ /amazon_folder_destination/

  
-x MAX\_CONNECTIONS, -r MAX\_RETRIES  
--deduplicate exclude duplicate files from upload, useful in case of errors. Only files with different checksum will be replaced.  
  
For downloading files to feralhosting use "download" command instead of "upload" and reverse directories for file location.  
  

Troubleshooting
---------------

  
If you see this error when trying to upload or download:  
  

    UnicodeEncodeError: 'utf-8' codec can't encode character '\udcc3' in position 7: surrogates not allowed
    16-05-03 21:58:36.154 [ERROR] [acd_cli] - Please set your locale or use the "--utf" flag.

  
Please try exporting the locale and then running the command as follows:  
  

    export LC_ALL="en_US.UTF-8" && ~.local/bin/acd_cli upload

  

