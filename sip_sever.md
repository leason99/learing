#Sip server install

  `#apt-get install asterisk`

###設定帳戶(sip.conf)

  Vi  /etc/asterisk/sip.conf
  
```
[general]
context=public
[1001]
type=friend
secret=1001
context=my
host=dynamic
nat=yes
accept_outofcall_message=yes
outofcall_message_context=sms
[1002]
type=friend
secret=1002
context=my
host=dynamic
nat=yes
accept_outofcall_message=yes
outofcall_message_context=sms
```
*以上設置包含通話與訊息傳遞*

+  `[ ]`  :  每個section用“中括號”命定。Asterisk也允許以字母作名稱。
+ type :  對客戶端的定義，user是撥入用，peer是撥出用，friend是撥入、撥出兩者皆可，如type=friend。

+  secret:  註冊認證碼，若section內未設定secret則默認section不需密碼即可註冊。
+ qualify:   qualify=yes可以監視任何遠端設備(包括其他的Asterisk PBX)的延遲狀況，預設是在2秒內，超過2秒則不接通，若設定用戶[1234]      qualify=1000，則撥1234時若延遲超過1秒不接通，但並不限制[1234]用戶撥給其它用戶，接通與否則要視其它用戶的qualify設定。

+ nat:   用戶端是否在NAT下，若為YES可強迫Asterisk忽略號碼的連繫訊息，改用收到封包的IP位址訊息host
 host=dynamic將要求用戶註冊，以便Asterisk可以找到電話，若用戶端為固定IP或域名，則可設定host=“固定IP”、host=“域名”，用戶不須註冊。

+ canreinvite:  canreinvite=no讓RTP封包經由Asterisk 主機互通，而不是IP by IP直接互通。
    Asterisk在下列情形不會發送reinvite:
      client任一端設定canreinvite=no。
      client無法協議通話用的codec，Asterisk必須執行語音編碼轉換。
      client任一端設定nat=yes。
      Asterisk需要在通話時監聽DTMF。
      

+ Port 指定用戶端Server port，預設值為SIP的5060埠。

+ context 定義用戶電話的權限，以及如何處理該號碼的撥入撥出，sip.conf中設定的context名稱與extensions.conf中互相對應。
    
[參考連結 sip.conf & extensions.conf](http://blog.roodo.com/garywu0111/archives/cat_478625.html)
[sip.conf for linphone about qualify](http://www.voip-info.org/wiki/view/Asterisk+phone+linphone)

###設定動作(extensions.conf)

   Vi  /etc/asterisk/sip.conf

```
[default] 
exten => _.,1,Hangup()
[demo]
exten => 2600,1,Dial(IAX2/guest@pbx.digium.com/s@default)
same => n,Hangup()
[my]
exten => _[0-9a-zA-Z].,1,Dial(SIP/${EXTEN},30)
same => n,SendText(Welcome to Asterisk)
same  => _[0-9a-zA-Z].,n,Hangup()
[sms]
exten => _.,1,NoOp(SMS receiving dialplan invoked)
exten => _.,n,NoOp(To ${MESSAGE(to)})
exten => _.,n,NoOp(From ${MESSAGE(from)})
exten => _.,n,NoOp(Body ${MESSAGE(body)})
exten => _.,n,Set(ACTUALTO=${CUT(MESSAGE(to),@,1)})
exten => _.,n,MessageSend(${ACTUALTO},${MESSAGE(from)})
exten => _.,n,NoOp(Send status is ${MESSAGE_SEND_STATUS})
exten => _.,n,GotoIf($["${MESSAGE_SEND_STATUS}" != "SUCCESS"]?sendfailedmsg)
exten => _.,n,Hangup()
;
; Handle failed messaging
exten => _.,n(sendfailedmsg),Set(MESSAGE(body)="[${STRFTIME(${EPOCH},,%d%m%Y-%H:%M:%S)}] Your message to ${EXTEN} has failed. Retry later.")
exten => _.,n,Set(ME_1=${CUT(MESSAGE(from),<,2)})
exten => _.,n,Set(ACTUALFROM=${CUT(ME_1,@,1)})
exten => _.,n,MessageSend(${ACTUALFROM},ServiceCenter)
exten => _.,n,Hangup()
exten => _.,n,Hangup()
```
*以上設置包含通話與訊息傳遞*

    說明：
     _：代表開頭
      X：代表0-9
     .：代表任意長度的字元
      _X.：指電話號碼是以數字開始不管任何長度

------------------------------------
copy from: https://github.com/smallmuou/Blogs/blob/master/blogs/asterisk%E5%9C%A8macosx%E4%B8%8B%E7%BC%96%E8%AF%91.md
# Asterisk 技术点
2014-11-07

* brew install apple-gcc-4.2
* ./configure CC=gcc-4.2
* define RONLY 0x1


Q:process_sdp: ignoring 'video' media offer because port number is zero

A:说明视频编码不支持，core show codecs video查看支持的视频编码（linphone默认只支持vp8）

## NAT类型
[NAT分类](http://blog.163.com/hlz_2599/blog/static/1423784742012317102533915/)

## Linphone
###### Stun Server
当设置Stun Server后, Linphone会获取从Stun Server获取到公网IP和port，并在发送SIP时填充Contact，当没有设置时，则Asterisk会返回，填写Recieved和rport
<pre>
12:34:24.516868 IP xuwenfas-iPhone.63627 > 192.168.60.151.5060: SIP, length: 411
Eh...?..@..$......<.........REGISTER sip:192.168.60.151 SIP/2.0
Via: SIP/2.0/UDP 192.168.1.131:63627;branch=z9hG4bK.PcrNcrd8a;<font color="00ff00">rport</font>
From: < sip:112@192.168.60.151>;tag=~wyqkEm4k
To: sip:112@192.168.60.151
CSeq: 20 REGISTER
Call-ID: QuDP68~7EC
Max-Forwards: 70
Supported: outbound
Contact: < sip:112@192.168.1.131:63627>;+sip.instance="< urn:uuid:f402ede7-9815-42d5-b0c5-66d7dabf93ba>"
Expires: 3600
User-Agent: (belle-sip/1.3.3)


12:34:24.518448 IP 192.168.60.151.5060 > xuwenfas-iPhone.63627: SIP, length: 530
E.......?..E..<............OSIP/2.0 200 OK
Via: SIP/2.0/UDP 192.168.1.131:63627;branch=z9hG4bK.PcrNcrd8a;<font color="00ff00">received=192.168.60.147;rport=63627</font>
From: < sip:112@192.168.60.151>;tag=~wyqkEm4k
To: sip:112@192.168.60.151;tag=as16758747
Call-ID: QuDP68~7EC
CSeq: 20 REGISTER
Server: Asterisk PBX SVN-trunk-r423130
Allow: INVITE, ACK, CANCEL, OPTIONS, BYE, REFER, SUBSCRIBE, NOTIFY, INFO, PUBLISH, MESSAGE
Supported: replaces, timer
Expires: 3600
Contact: < sip:112@192.168.1.131:63627>;expires=3600
Date: Tue, 18 Nov 2014 00:25:29 GMT
Content-Length: 0


12:34:25.381597 IP xuwenfas-iPhone.63627 > 192.168.60.151.5060: SIP, length: 433
Eh......@..x......<.........REGISTER sip:192.168.60.151 SIP/2.0
Via: SIP/2.0/UDP 192.168.1.131:63627;branch=z9hG4bK.~kn9Nn2n7;rport
From: <sip:112@192.168.60.151>;tag=hQmZSm18L
To: sip:112@192.168.60.151
CSeq: 20 REGISTER
Call-ID: nPk8A34HWK
Max-Forwards: 70
Supported: outbound
<font color="00ff00">Contact: < sip:112@192.168.60.147:63627></font>;+sip.instance="< urn:uuid:f402ede7-9815-42d5-b0c5-66d7dabf93ba>"
Expires: 3600
User-Agent: LinphoneIPhone/2.2.3 (belle-sip/1.3.3)

</pre>

## rport
获得IP地址是在Via头中带上received参数。为了得到端口信息，也参考了这种方式，即在Via头中带上rport属性来指明端口信息。

如果是支持rport机制的服务器，它需要在接收到的请求中检查Via头是否包含一个没有值的rport参数。如果有，它需要在回应中带上rport的值，这与received的处理类似。
<pre>
12:09:59.566063 IP xuwenfas-iPhone.61710 > 192.168.60.151.5060: SIP, length: 433
Eh......@..I......<.......z.REGISTER sip:192.168.60.151 SIP/2.0
Via: SIP/2.0/UDP 192.168.1.131:61710;branch=z9hG4bK.ccoKJW05t;rport
From: <sip:112@192.168.60.151>;tag=CDqPrLUqI
To: sip:112@192.168.60.151
CSeq: 24 REGISTER
Call-ID: 81nl08JxWA
Max-Forwards: 70
Supported: outbound
Contact: <sip:112@192.168.60.147:61710>;+sip.instance="<urn:uuid:f402ede7-9815-42d5-b0c5-66d7dabf93ba>"
Expires: 3600
User-Agent: LinphoneIPhone/2.2.3 (belle-sip/1.3.3)


12:09:59.567578 IP 192.168.60.151.5060 > xuwenfas-iPhone.61710: SIP, length: 531
E../....?..N..<...........s/SIP/2.0 200 OK
Via: SIP/2.0/UDP 192.168.1.131:61710;branch=z9hG4bK.ccoKJW05t;received=192.168.60.147;rport=61710
From: <sip:112@192.168.60.151>;tag=CDqPrLUqI
To: sip:112@192.168.60.151;tag=as4b4f12a7
Call-ID: 81nl08JxWA
CSeq: 24 REGISTER
Server: Asterisk PBX SVN-trunk-r423130
Allow: INVITE, ACK, CANCEL, OPTIONS, BYE, REFER, SUBSCRIBE, NOTIFY, INFO, PUBLISH, MESSAGE
Supported: replaces, timer
Expires: 3600
Contact: <sip:112@192.168.60.147:61710>;expires=3600
Date: Tue, 18 Nov 2014 00:01:04 GMT
Content-Length: 0

</pre>

## SIP.conf
* autocreatepeer=yes 允许自动创建节点
* context=xx，指定拨号规则（定义在extension.conf中）
* directmedia 见canreinvite
* directrtpsetup
* canreinvite 重定向媒体流，在1.6.2后改为directmedia
	* yes - allow RTP media direct
	```This means that this SIP is _always_ able to receive direct RTP media,from any other peer, regardless of IP address or network route.```
	* no - deny re-invites(转发)
	```This means that this SIP peer is not able to receive direct RTP media,from any other peer, regardless of IP address or network route.```
	* nonat - allow reinvite when local, deny reinvite when NAT
	* update - use UPDATE instead of INVITE
	* update,nonat - use UPDATE when local, deny when NAT
	
* allow 允许编解码器
* allowguest 允许来电
* media_address 设定媒体流地址
* externip - 外网IP，与localnet配合用，当呼入的ip与localnet不在同一个网段，则用externip替换sdp中的ip
* localnet=192.168.2.0/255.255.255.0。。。可以有多个localnet（多网卡情况）
* nat
	* yes - forces RFC 3581 behavior and enables symmetric RTP support
	* no - only enables RFC 3581 behavior if the remote side requests it and disables symmetric RTP support
	* force_rport -  forces RFC 3581 behavior and disables symmetric RTP support
	* comedia - enables RFC 3581 behavior if the remote side requests it and enables symmetric RTP support.
	
	* force_rport+comedia = yes

## UPDATE
SIP的UPDATE（[RFC3311](https://tools.ietf.org/html/rfc3311)）消息是SIP扩展的一种机制，用以在通话尚未建立的时候更新媒体流状态的一种机制。

INVITE --- UPDATE --- REINVITE

## 会话流程
```When SIP initiates the call, the INVITE message contains the information on where to send the media streams. Asterisk uses itself as the end-points of media streams when setting up the call. Once the call has been accepted, Asterisk sends another (re)INVITE message to the clients with the information necessary to have the two clients send the media streams directly to each other.```

理解: 当SIP发起会话时，INVITE通过SDP携带媒体流传输需要的信息（IP、PORT），Asterisk会将自己作为媒体流接受者，一旦邀请被接受，Asterisk会发送带有媒体流信息的(re)INVITE给客户端，以便客户端之间建立P2P连接.
当以下条件不会发送(re)INVITE:

* canreinvite=NO
* 客户端使用不同的编解码器
* Dial包含 ''t'', ''T", "h", "H", "w", "W" or "L" (with multiple arguments) 

