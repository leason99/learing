
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

------

撥號計劃使用perl的正則表達式。

常用的匹配模式如下：

  ^ 表示開始匹配，^123 表示匹配123開頭
  $表示結束匹配
  456$表示匹配456結束
  | 表示或者，匹配任何一個
  [] 表示匹配其中的任意一個字符
  [0-9] 等於匹配[0123456789]
  \d等於匹配[0-9]
\d+ 等於匹配1 個或多個數字
\d* 等於匹配0 個或多個前面的字符




