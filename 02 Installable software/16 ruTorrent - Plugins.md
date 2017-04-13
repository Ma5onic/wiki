ruTorrent - Plugins
===================

ruTorrent's features can be extended in many different ways through the use of plugins. Though some more common ones will be installed when installing ruTorrent itself there are lots more that can be added.  
  

Custom Plugins
--------------

This section provides information on the most common custom plugins, how to install them and troubleshooting the most common problems that can arise. Please note though the plugins should work (if you follow the guide properly), Feral cannot provide much support for their use or help should anything go wrong. Please make sure you've read these FAQ pages fully as help on the problem may be covered already.  
  
This notice absolutely does not prevent you from raising a ticket should anything go wrong but please bear in mind staff may not be able to assist beyond basic troubleshooting (for example reinstalling, clarifying error messages and so on).  
  
  

### Installing Custom Plugins - General Method

Plugins can be added to ruTorrent simply by adding its directory to ruTorrent's plugins directory. This is possible in a number of ways, but the easiest is SSH. If you've never used SSH commands the idea of using a terminal window may seem daunting. There is a guide on simply getting connected to your slot through SSH [here](https://www.feralhosting.com/faq/view?question=12).  
  
Unless contained in the list in the next section, execute the following commands to install a plugin, replacing *plugin\_name* with the official name of the plugin:  
  

    cd ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/plugins/
    svn checkout https://github.com/Novik/ruTorrent/trunk/plugins/plugin_name

  
  

### Installing Custom Plugins - Special Requirements

Sometimes a plugin needs a different approach. This can be either because the download is located in a different place, another version is needed, the plugin depends on other software or because there are further steps needed to get the plugin up and running. Simply click through the following links to see the installation method and further help.  
  
[Unpack](https://www.feralhosting.com/faq/view?question=337)  
[Autodl-irssi](https://www.feralhosting.com/faq/view?question=142)  
[Screenshots](https://www.feralhosting.com/faq/view?question=328)  
[Filemanager](https://www.feralhosting.com/faq/view?question=330)  
[Fileshare](https://www.feralhosting.com/faq/view?question=210)  
[Feralstats](https://www.feralhosting.com/faq/view?question=126) - linking your usage page to ruTorrent  
[Coloured Ratio Column](https://www.feralhosting.com/faq/view?question=184)  
[Mediastream](https://www.feralhosting.com/faq/view?question=209)  
[Fileupload](https://www.feralhosting.com/faq/view?question=331) - using Plowshare to upload to service providers via ruTorrent  
  

Troubleshooting Default Plugins
-------------------------------

*I'm experiencing issues with RSS feeds*  
There are multiple known issues that can be seen with ruTorrent's RSS plugin and it's recommended that another method (for example [Flexget](https://www.feralhosting.com/faq/view?question=234)) is used instead. If you want to try and troubleshoot the plugin instead, please see [this page](https://www.feralhosting.com/faq/view?question=162).  
  
*I get a message "Ratio: Plugin failed to start"*  
This most often occurs when you've set too high a value in one of the fields. You'll need to remove ratio.dat from your ruTorrent settings directory and refresh ruTorrent. The plugin should then be usable.  
  
The easiest way to remove ratio.dat is to execute this command via SSH:  

    rm ~/www/$(whoami).$(hostname -f)/public_html/rutorrent/share/users/$(whoami)/settings/ratio.dat

  
As a rule of thumb you should leave the minimum percentage at 100% and use -1 (for unlimited) for any value you're not looking to control. For example, if you want the ratio group to work based on time, set the maximum percentage to -1 rather than some massive percentage.  
  

