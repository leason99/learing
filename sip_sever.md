###Sip server install

apt-get install asterisk

設定帳戶(sip.conf)

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


設定動作(extensions.conf)
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

