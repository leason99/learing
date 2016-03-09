
  no usable zlib; please install zlib devel package or equivalent
  
  apt-get install zlib1g-dev  

no usable libjpeg; please install libjpeg devel package or equivalent
 
  apt-get install libjpeg-dev
  
  Library requirements (sqlite3 >= 3.6.20) not met; consider adjusting the PKG_CONFIG_PATH environment variable if your libraries are in a nonstandard prefix so pkg-config can find them.
  
  apt-get install sqlite3 libsqlite3-dev
  
  
  [install guide] (http://www.freeswitch.org.cn/2009/11/08/freeswitch-xin-shou-zhi-nan.html)
  finall 
  
  apt-get install autoconf automake devscripts gawk g++ git-core libjpeg-dev \
 libncurses5-dev libtool make python-dev gawk pkg-config libtiff5-dev \
 libperl-dev libgdbm-dev libdb-dev gettext libssl-dev libcurl4-openssl-dev \
 libpcre3-dev libspeex-dev libspeexdsp-dev libsqlite3-dev libedit-dev libldns-dev



not found libtool or should  have newer version

sudo apt-get install libtool-bin


make:
 apt-get install yasm nasm
 https://github.com/nolka/php-lua-install-script
 
 install libopus-dev
 http://stackoverflow.com/questions/25395394/installing-opus-in-freeswitch
 codecs/mod_opus
 
 libsndfile-dev

 ``
  +---------- FreeSWITCH install Complete ----------+
 + FreeSWITCH has been successfully installed.     +
 +                                                 +
 +       Install sounds:                           +
 +       (uhd-sounds includes hd-sounds, sounds)   +
 +       (hd-sounds includes sounds)               +
 +       ------------------------------------      +
 +                make cd-sounds-install           +
 +                make cd-moh-install              +
 +                                                 +
 +                make uhd-sounds-install          +
 +                make uhd-moh-install             +
 +                                                 +
 +                make hd-sounds-install           +
 +                make hd-moh-install              +
 +                                                 +
 +                make sounds-install              +
 +                make moh-install                 +
 +                                                 +
 +       Install non english sounds:               +
 +       replace XX with language                  +
 +       (ru : Russian)                            +
 +       (fr : French)                             +
 +       ------------------------------------      +
 +                make cd-sounds-XX-install        +
 +                make uhd-sounds-XX-install       +
 +                make hd-sounds-XX-install        +
 +                make sounds-XX-install           +
 +                                                 +
 +       Upgrade to latest:                        +
 +       ----------------------------------        +
 +                make current                     +
 +                                                 +
 +       Rebuild all:                              +
 +       ----------------------------------        +
 +                make sure                        +
 +                                                 +
 +       Install/Re-install default config:        +
 +       ----------------------------------        +
 +                make samples                     +
 +                                                 +
 +                                                 +
 +       Additional resources:                     +
 +       ----------------------------------        +
 +       https://www.freeswitch.org                +
 +       https://freeswitch.org/confluence         +
 +       https://freeswitch.org/jira               +
 +       http://lists.freeswitch.org               +
 +                                                 +
 +       irc.freenode.net / #freeswitch            +
 +                                                 +
 +       Register For ClueCon:                     +
 +       ----------------------------------        +
 +       https://www.cluecon.com                   +
 +                                                 +
 +-------------------------------------------------+
``
