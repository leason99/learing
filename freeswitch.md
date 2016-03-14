
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




http://fanli7.net/a/bianchengyuyan/C__/20120813/203874.html
http://wenku.baidu.com/view/fde3e68cbceb19e8b8f6ba45.html

--------
>>1. freeswtich对高清(HD)语音编码的支持
freeswitch支持 大部分高清语音编码，包括Speex,G.722,G.722.1(Siren) 及SILK,与之对比，asterisk 1.8版本之前只支持采样为8000的常用语音编码，1.10后asterisk开始从新架构其media codec模块，以全面支持高清等宽频语音编码。
2.有些语音编码以模块方式加载(G729等)，有的则属于freeswitch core部分(G711)，系统默认不加载所有语音编码，对于没有加载的编码，可以通过配置
modules.conf.xml配置，在fs_cli上 执行 "show codec" 会显示当前系统已经加载的编码：

type,name,ikey
codec,ADPCM (IMA),mod_spandsp
codec,AMR,mod_amr
codec,G.711 alaw,CORE_PCM_MODULE
codec,G.711 ulaw,CORE_PCM_MODULE
codec,G.722,mod_spandsp
codec,G.723.1 6.3k,mod_g723_1
codec,G.726 16k,mod_spandsp
codec,G.726 16k (AAL2),mod_spandsp
codec,G.726 24k,mod_spandsp
codec,G.726 24k (AAL2),mod_spandsp
codec,G.726 32k,mod_spandsp
codec,G.726 32k (AAL2),mod_spandsp
codec,G.726 40k,mod_spandsp
codec,G.726 40k (AAL2),mod_spandsp
codec,G.729,mod_g729
codec,GSM,mod_spandsp
codec,H.261 Video (passthru),mod_h26x
codec,H.263 Video (passthru),mod_h26x
codec,H.263+ Video (passthru),mod_h26x
codec,H.263++ Video (passthru),mod_h26x
codec,H.264 Video (passthru),mod_h26x
codec,LPC-10,mod_spandsp
codec,PROXY PASS-THROUGH,CORE_PCM_MODULE
codec,PROXY VIDEO PASS-THROUGH,CORE_PCM_MODULE
codec,Polycom(R) G722.1/G722.1C,mod_siren
codec,RAW Signed Linear (16 bit),CORE_PCM_MODULE
codec,Speex,mod_speex
codec,iLBC,mod_ilbc
以模块方式加载的编码在目录 src\mod\codecs下面，所以如果我们想添加自己的编码，在此目录下参考其他实现即可，freeswitch对新编码的添加接口也及其简单，主要为注册几个四个回调，init,encode,decode,destroy,然后通过 switch_core_codec_add_implementation 把这几个回调的实现注册进去。
3. 设置编码的优先级
vars.xml可以设置系统默认使用的编码，为全局设置，下面两个变量，一个表示呼入，一个表示呼出。

 <X-PRE-PROCESS cmd="set" data="global_codec_prefs=G722,PCMA,PCMU,GSM"/>
<X-PRE-PROCESS cmd="set" data="outbound_codec_prefs=G722,PCMA,PCMU,GSM"/>

同时，不同的协议类型（SIP，和H323等）可以设置自己的编码优先级，比如采用SIP协议时，可以在

sofia.conf.xml

 <settings>
 <param name="inbound-codec-prefs" value="$${global_codec_prefs}"/>
 <param name="outbound-codec-prefs" value="$${global_codec_prefs}"/>
</settings>

这里，SIP协议类型继承了vars.xml的全局设置（呼入，呼出）。

4. 对编解码转换的支持
(1)作为B2BUA，freeswitch支持大部分音频编码的转换，但无视频编码转换功能。
(2)对于语音编码 G721 / G728 / G719 / AMR，只支持转发，不支持转换。
(3)freeswitch支持的视频编码 （只转发）
H261 - H.261 Video
H263 - H.263 Video
H263-1998 - H.263-1998 Video
H263-2000 - H.263-2000 Video
H264 - H.264 Video
Provided by mod_h26X.
Theora passthrough.
Provided by mod_theora.
MP4 Video passthrough.
Provided by mod_mp4v.

(4)媒体代理
freeswitch对媒体的处理有三种方式：

a.默认方式:媒体通过freeswitch,
RTP被freeswtich转发，
freeswitch控制编码的协商并在协商不一致时提供语音编码转换能力，
支持录音，二次拨号等。

b.代理模式: 媒体通过freeswitch转发，但是不处理媒体
   RTP通过freewtich转发(只改动sdp c= ip)
   freeswtich不控制 sdp参数，只是转发。
   通话的终端必须有一致的语音或者视频编码，因为freeswitch此时不支持转码（适合视频编码）
   不支持录音， 二次拨号等功能
c.不转发也不处理媒体
此模式下freeswitch更像是一个信令proxy,媒体不会通过freeswitch,sdp消息体也不做修改，没有录音，二次拨号等功能。

三种方式在不同应用场景下各有优点，对于a,也是默认方式，更适合呼叫中心等富功能应用，但性能相比其他两个也是最差的，对于b，更适合处理nat问题，
可以考虑用这种模式做一个session border controlor,也适合于外部MCU配合做为视频会议,性能也明显好于a,对于 c，更像是一个信令代理，性能最高，但提供的功能有限。

