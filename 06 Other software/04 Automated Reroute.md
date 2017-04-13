Automated Reroute
=================

If you find yourself regularly visiting the [reroute page](https://network.feral.io/reroute) to make route changes, or you just want an easy way to accurately test speed from Feral servers to your home network, run the auto-reroute script on your computer at home. The script downloads test files from each of Feral's routes, determines the fastest route, then sets that route for you. Results are logged to ~/.auto-reroute/auto-reroute.log  
  

Linux & OSX
-----------

  
  
Open up a terminal and paste in, and run the following command:  
  

    curl -s -L -o ~/auto-reroute.sh http://git.io/hsFb && bash ~/auto-reroute.sh

  
  

Windows (Using Cygwin)
----------------------

  
  
Need help installing Cygwin? Check out [this FAQ page.](https://www.feralhosting.com/faq/view?question=235)  
  
If you don't already have them installed, re-run the cygwin installer, and install `curl` (under "Net") and `bc` (under "Math").  
Once installed, open up a Cygwin terminal, paste in, and run the following command:  
  

    curl -s -L -o ~/auto-reroute.sh http://git.io/hsFb && bash ~/auto-reroute.sh

  
  
  

Sample Run
----------

  
The following is a real time example of what the script should look like when run.  
  
![](http://i.imgur.com/6AkGI7d.gif)  
  

