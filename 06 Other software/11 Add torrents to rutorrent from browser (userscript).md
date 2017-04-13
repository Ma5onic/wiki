Add torrents to rutorrent from browser (userscript)
===================================================

  
This is a userscript that will allow you to add torrents to your uTorrent through any browser that supports userscripts (commonly Chrome via Tampermonkey and FireFox via Greasemonkey). This also works  
  
Supports sites: What, PTP, BTN, SCC, BIB, AB, bB, TPB, Demonoid, D-Addicts (and would probably work on others, especially gazelle based trackers, if you edit them into the include portion of your script (explained here: [Include\_and\_exclude\_rules](http://wiki.greasespot.net/Include_and_exclude_rules))  
  
It looks like this:  
  
![](https://raw.github.com/SaberSalv/saber-addtorrent/master/snapshot.jpg)  
  
**1:** Go and get the [saber-addtorrent Grease Monkey Script](http://userscripts.org/scripts/show/150375)  
  
**2:** Press install.  
  
**3:** After installation, go to one of the supported sites (I'm going to use PtP in my example).  
  
**4:** Go to a torrent page. This will be the movie/album/season page, not the artist or series page. Scroll to the bottom, and find the button highlighted in the image below (though, the CSS on what.cd seems to be messed up, and the config button shows up below the header, so if you can't find it, look around the page some).  
  
![](http://i.imgur.com/Gtg5cyz.png)  
  
**5:** Click that link, and the box you see will pop up. Put in the details for your rutorrent. You can easily get these by going to [manager/slot/server](https://www.feralhosting.com/manager/) and scrolling down to your rutorrent info under Installed Software. I recommend HTTPS, always.  
  
**Main settings**  
  
This isn't exactly intuitive. The first box will set the number of download link images you will see. The second box will change what label the corresponding download link will apply to that torrent in rutorrent. I just set mine to 1 and a general sort tag, but you could add as many as you want for advanced labelling.  
  
Example:  
  
![](http://i.imgur.com/oSEqqX1.png)  
  
The bottom boxes are for setting images, so you could use something like favicons for each link, or just leave it how it is for the defaults.. And it changes to the second image after you've downloaded it.  
  

