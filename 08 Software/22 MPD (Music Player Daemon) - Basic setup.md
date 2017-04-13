MPD (Music Player Daemon) - Basic setup
=======================================

MPD Installation
================

  
  
[MPD (Music Player Daemon)](http://www.musicpd.org/) is an extremelly liteweight music server with built-in music streaming and transcoding capabilities. There are no requirements for Java and no licenses you have to buy.  
  
1. \`mkdir -p ~/.mpd/playlists\`  
2. \`touch ~/.mpd/{database,log,state}\`  
3. Copy the configuration to \`~/.mpd/mpd.conf\`  
4. Start with \`mpd ~/.mpd/mpd.conf\`  

    music_directory                  "~/private/rtorrent/data"
    db_file                          "~/.mpd/database"
    log_file                         "~/.mpd/log"
    pid_file                         "~/.mpd/pid"
    state_file                       "~/.mpd/state"
    playlist_directory               "~/.mpd/playlists"
    #password                        "password@read,add,control,admin"
    bind_to_address                  "aphrodite.feralhosting.com"
    port                             "44000"
    gapless_mp3_playback             "yes"
    auto_update                      "yes"

    audio_output {
                   type             "httpd"
                   name             "LAME"
                   encoder          "lame"
                   port             "8001"
                   bitrate          "320"
    }

    replaygain                       "album"
    replaygain_preamp                "0"

  
  
5. Open the stream in VLC via "Open Netowrk" and input \`<http://aphrodite.feralhosting.com:8001>\`  
6. Fire up [ncmpcpp](http://ncmpcpp.rybczak.net) or your favorite client and start playing some tunes.  
  
  
Shamelessly copied from [this gist](https://gist.github.com/maletor/8153179)  

