Fixing Filter/Feed loss bug for RSS Downloader Plugin (ruTorrent)
=================================================================

  
to fix this problem, I've spent some time figuring how the plugin works and after a few months of testing I'm finally releasing my fix to this problem  
  

1: what this fix exactly does:
------------------------------

  
when adding a new feed/filter it creates a backup file automatically for either the feeds or the filters.  
  
these backup files are automatically updated when you add new or do changes to the feeds/filters and when the feeds/filters are correctly loaded  
  
in my tests so far i encountered some errors regarding the feeds/filters but but haven't lost any of the feeds or filters so far  
  

2: how to get this fix
----------------------

  
you can either download the `rss.php` file from [here](https://mega.co.nz/#!i01wlA7I!0q4l0jYnXTYVfI8ww-5bVsd8eOEWJ76kQZCpT-pZcGg) and replace your current `rss.php` in your rutorrent director  
I created this fix with rutorrent that you can install from your account manager.  
so I don't know if this works with other version of rutorrent.  
  
or you can add the following parts by yourself  
  
**2.1** open your rss.php in your rutorrent directory.  
  
**2.2** got to line 821. there you will see "public function rRSSManager()"  
  
**2.3** in that function after the line with "$this-&gt;cache  = new rCache( '/rss/cache' );"  
  
replace the following 3 lines  
  

    $this->rssList = new rRSSMetaList();
    $this->cache->get($this->rssList);
    $this->rssList->resetErrors();

  
with  
  

    $this->MetalListLoadAndBackup();

  
**2.4** once done go to line 831 add a line after it and add the following code  
  

    private function MetalListLoadAndBackup() {
        $this->rssList = new rRSSMetaList();

        $name = $this->rssList->hash;
        if($this->cache->get($this->rssList)) {
            $this->rssList->hash = $name . "_backup";
            $this->cache->set($this->rssList);
            $this->rssList->hash = $name;
        } else {
            $this->rssList->hash = $name . "_backup";
            $this->cache->get($this->rssList);
            $this->rssList->hash = $name;
        }
        $this->rssList->resetErrors();
    }

  
**2.5** now go to line 873 and add a new line after that and add the following  
  

    private function FilterListLoadAndBackup() {
        $flts = new rRSSFilterList();

        $name = $flts->hash;
        if($this->cache->get($flts)) {
            $flts->hash = $name . "_backup";
            $this->cache->set($flts);
        } else {
            $flts->hash = $name . "_backup";
            $this->cache->get($flts);
        }
        $flts->hash = $name;
        
        return $flts;
    }

  
now we are almost there  
  
**2.6** on line 891 replace the following  
  

    $flts = new rRSSFilterList();
            $this->cache->get($flts);

  
with  
  

    $flts = $this->FilterListLoadAndBackup();

  
now we are done... this should do the trick  
these functions will do the backup and load the backup if the actual file is corrupted (as explained at the top)  
  

