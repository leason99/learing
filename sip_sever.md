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

    說明：
     _：代表開頭
      X：代表0-9
     .：代表任意長度的字元
      _X.：指電話號碼是以數字開始不管任何長度

