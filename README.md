photo-mailer
============

Send photos often. 

###### Cron job

Everyday at 10 pm

```
0 22 * * * /usr/bin/photo-mailer  -s /home/praneshp/mailer_pics/  -c 1 > /dev/null
```

For noobs, generate [crons here](http://www.htmlbasix.com/crontab.shtml). 



###### Smtp
For configs, take a look at [this](http://rpi.tnet.com/project/faqs/smtp)
