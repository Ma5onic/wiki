Perl - Installing modules
=========================

In SSH do the commands described in this FAQ. If you do not know how to SSH into your slot use this FAQ: [SSH basics - Putty](https://www.feralhosting.com/faq/view?question=12)  
  
Your FTP / SFTP / SSH login information can be found on the Slot Details page for the relevant slot. Use this link in your Account Manager to access the relevant slot:  
  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_link.png)  
  
You login information for the relevant slot will be shown here:  
![](https://raw.github.com/feralhosting/feralfilehosting/master/Feral%20Wiki/0%20Generic/slot_detail_ssh.png)  
**Perl 5 is installed on all servers by default**  
Type to show the current version:  

    perl -v

  

Installing modules:
-------------------

  
The majority of perl modules are user installable, there is some setup required before hand.  
**1. cpan config**  
Make the config directory  

    mkdir -p ~/.cpan/CPAN

  
Add your config. You can either copy and paste the (really long) one-liner below into SSH or create the file `~/.cpan/CPAN/MyConfig.pm` with the contents also listed below.  
  
One-liner:  

    echo -e "\$CPAN::Config = {\n  'applypatch' => q[],\n  'auto_commit' => q[0],\n  'build_cache' => q[100],\n  'build_dir' => q[$HOME/.cpan/build],\n  'build_dir_reuse' => q[0],\n  'build_requires_install_policy' => q[yes],\n  'bzip2' => q[/bin/bzip2],\n  'cache_metadata' => q[1],\n  'check_sigs' => q[0],\n  'colorize_output' => q[0],\n  'commandnumber_in_prompt' => q[1],\n  'connect_to_internet_ok' => q[1],\n  'cpan_home' => q[$HOME/.cpan],\n  'ftp_passive' => q[1],\n  'ftp_proxy' => q[],\n  'getcwd' => q[cwd],\n  'gpg' => q[/usr/bin/gpg],\n  'gzip' => q[/bin/gzip],\n  'halt_on_failure' => q[0],\n  'histfile' => q[$HOME/.cpan/histfile],\n  'histsize' => q[100],\n  'http_proxy' => q[],\n  'inactivity_timeout' => q[0],\n  'index_expire' => q[1],\n  'inhibit_startup_message' => q[0],\n  'keep_source_where' => q[$HOME/.cpan/sources],\n  'load_module_verbosity' => q[none],\n  'make' => q[/usr/bin/make],\n  'make_arg' => q[],\n  'make_install_arg' => q[],\n  'make_install_make_command' => q[/usr/bin/make],\n  'makepl_arg' => q[INSTALLDIRS=site],\n  'mbuild_arg' => q[],\n  'mbuild_install_arg' => q[],\n  'mbuild_install_build_command' => q[./Build],\n  'mbuildpl_arg' => q[--installdirs site],\n  'no_proxy' => q[],\n  'pager' => q[/usr/bin/less],\n  'patch' => q[/usr/bin/patch],\n  'perl5lib_verbosity' => q[none],\n  'prefer_external_tar' => q[1],\n  'prefer_installer' => q[MB],\n  'prefs_dir' => q[$HOME/.cpan/prefs],\n  'prerequisites_policy' => q[follow],\n  'scan_cache' => q[atstart],\n  'shell' => q[/bin/bash],\n  'show_unparsable_versions' => q[0],\n  'show_upload_date' => q[0],\n  'show_zero_versions' => q[0],\n  'tar' => q[/bin/tar],\n  'tar_verbosity' => q[none],\n  'term_is_latin' => q[1],\n  'term_ornaments' => q[1],\n  'test_report' => q[0],\n  'trust_test_report_history' => q[0],\n  'unzip' => q[/usr/bin/unzip],\n  'urllist' => [q[http://cpan.mirror.anlx.net/], q[http://ftp.ticklers.org/pub/CPAN/], q[http://mir2.ovh.net/ftp.cpan.org/]],\n  'use_sqlite' => q[0],\n  'version_timeout' => q[15],\n  'wget' => q[/usr/bin/wget],\n  'yaml_load_code' => q[0],\n  'yaml_module' => q[YAML],\n};\n1;\n__END__" > ~/.cpan/CPAN/MyConfig.pm

  
Config to copy and paste. You will need to edit everywhere instance of USERHOME with the full path to your home directory. You can find this by typing `$HOME` in SSH  

    $CPAN::Config = {
      'applypatch' => q[],
      'auto_commit' => q[0],
      'build_cache' => q[100],
      'build_dir' => q[USERHOME/.cpan/build],
      'build_dir_reuse' => q[0],
      'build_requires_install_policy' => q[yes],
      'bzip2' => q[/bin/bzip2],
      'cache_metadata' => q[1],
      'check_sigs' => q[0],
      'colorize_output' => q[0],
      'commandnumber_in_prompt' => q[1],
      'connect_to_internet_ok' => q[1],
      'cpan_home' => q[USERHOME/.cpan],
      'ftp_passive' => q[1],
      'ftp_proxy' => q[],
      'getcwd' => q[cwd],
      'gpg' => q[/usr/bin/gpg],
      'gzip' => q[/bin/gzip],
      'halt_on_failure' => q[0],
      'histfile' => q[USERHOME/.cpan/histfile],
      'histsize' => q[100],
      'http_proxy' => q[],
      'inactivity_timeout' => q[0],
      'index_expire' => q[1],
      'inhibit_startup_message' => q[0],
      'keep_source_where' => q[USERHOME/.cpan/sources],
      'load_module_verbosity' => q[none],
      'make' => q[/usr/bin/make],
      'make_arg' => q[],
      'make_install_arg' => q[],
      'make_install_make_command' => q[/usr/bin/make],
      'makepl_arg' => q[INSTALLDIRS=site],
      'mbuild_arg' => q[],
      'mbuild_install_arg' => q[],
      'mbuild_install_build_command' => q[./Build],
      'mbuildpl_arg' => q[--installdirs site],
      'no_proxy' => q[],
      'pager' => q[/usr/bin/less],
      'patch' => q[/usr/bin/patch],
      'perl5lib_verbosity' => q[none],
      'prefer_external_tar' => q[1],
      'prefer_installer' => q[MB],
      'prefs_dir' => q[USERHOME/.cpan/prefs],
      'prerequisites_policy' => q[follow],
      'scan_cache' => q[atstart],
      'shell' => q[/bin/bash],
      'show_unparsable_versions' => q[0],
      'show_upload_date' => q[0],
      'show_zero_versions' => q[0],
      'tar' => q[/bin/tar],
      'tar_verbosity' => q[none],
      'term_is_latin' => q[1],
      'term_ornaments' => q[1],
      'test_report' => q[0],
      'trust_test_report_history' => q[0],
      'unzip' => q[/usr/bin/unzip],
      'urllist' => [q[http://cpan.mirror.anlx.net/], q[http://ftp.ticklers.org/pub/CPAN/], q[http://mir2.ovh.net/ftp.cpan.org/]],
      'use_sqlite' => q[0],
      'version_timeout' => q[15],
      'wget' => q[/usr/bin/wget],
      'yaml_load_code' => q[0],
      'yaml_module' => q[YAML],
    };
    1;
    __END__

  
  
**2. Bash setup**  
Add the below to your ~/.bashrc  

    PATH=$HOME/perl5/bin:$HOME/bin:$HOME/.local/bin:/user/local/bin:/usr/local/bin:$HOME/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
    PERL5LIB=$HOME/perl5/lib/perl5:
    PERL_MB_OPT=--install_base $HOME/perl5
    PERL_LOCAL_LIB_ROOT=:$HOME/perl5
    PERL_MM_OPT=INSTALL_BASE=$HOME/perl5

  
And source your bashrc  

    source ~/.bashrc

  
**3. Install some Perl mods**  

     cpan Module::Name

  
For example:  

    cpan Bencode
    Reading '/media/md0/bobtentpeg/.cpan/Metadata'
      Database was generated on Wed, 13 Jul 2016 16:53:44 GMT
    Running install for module 'Bencode'
    Fetching with LWP:
    http://cpan.mirror.anlx.net/authors/id/A/AR/ARISTOTLE/Bencode-1.402.tar.gz
    Fetching with LWP:
    http://cpan.mirror.anlx.net/authors/id/A/AR/ARISTOTLE/CHECKSUMS
    Checksum for /media/md0/bobtentpeg/.cpan/sources/authors/id/A/AR/ARISTOTLE/Bencode-1.402.tar.gz ok
    <SNIP>
    Files=3, Tests=76,  0 wallclock secs ( 0.03 usr  0.00 sys +  0.12 cusr  0.00 csys =  0.15 CPU)
    Result: PASS
      ARISTOTLE/Bencode-1.402.tar.gz
      /usr/bin/make test -- OK
    Running make install
    Manifying 1 pod document
    Installing /media/md0/bobtentpeg/perl5/lib/perl5/Bencode.pm
    Installing /media/md0/bobtentpeg/perl5/man/man3/Bencode.3pm
    Appending installation info to /media/md0/bobtentpeg/perl5/lib/perl5/x86_64-linux-gnu-thread-multi/perllocal.pod
      ARISTOTLE/Bencode-1.402.tar.gz
      /usr/bin/make install  -- OK

  
  

