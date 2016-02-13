###Sip server install

apt-get install asterisk

設定帳戶(sip.conf)

  Vi  /etc/asterisk/sip.conf

>[general]
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
