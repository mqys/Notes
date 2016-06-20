# Content


## Send EMail
```
#!/usr/bin/python
# -*- coding: utf-8 -*-

from datetime import datetime, timedelta
from email.mime.text import MIMEText
from email.header import Header
from email.utils import formataddr
import smtplib
import os
import sys

# date
date = datetime.now()
datestr = date.strftime('%Y-%m-%d')

# run cmd
if len(sys.argv) < 2:
    exit()
cmd = sys.argv[1]
# print(cmd)
res = os.popen(cmd).read()
# print(res)

# send email
sender = 'send.py@gw1ss.prod.mediav.com'
receivers = ['pengnan-sal@360.cn', '1305111800@qq.com']
subject = datestr + 'Cmd: '+cmd

msg = MIMEText(res, 'plain', 'utf-8')
msg['Subject'] = Header(subject, 'utf-8').encode()
msg['From'] = formataddr((Header('send.py', 'utf-8').encode(), sender))
msg['To'] = formataddr((Header('Receivers', 'utf-8').encode(), receivers))

# server = smtplib.SMTP('localhost')
# server.sendmail(sender, receivers, msg.as_string())
# server.quit()

try:
    smtpObj = smtplib.SMTP('localhost')
    smtpObj.sendmail(sender, receivers, msg.as_string())
    smtpObj.quit()
except smtplib.SMTPException:
    print "Error: 无法发送邮件"
```