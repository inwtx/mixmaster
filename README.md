# Debian mixmaster remailer installation instructions.

I. In /root of your server:  
<b>&nbsp;&nbsp;&nbsp;sudo apt-get install haveged</b>  
<b>&nbsp;&nbsp;&nbsp;sudo apt-get install ssl-cert</b>  
<b>&nbsp;&nbsp;&nbsp;wget --no-check-certificate http://www.zen19351.zen.co.uk/mixmaster31/debian84_mixmaster_3.1-1_amd64.deb</b>  
<b>&nbsp;&nbsp;&nbsp;sudo dpkg -i ./debian84_mixmaster_3.1-1_amd64.deb</b>  
    
Mixmaster should now be installed.  
    
II. (Step II can be bypassed if installing on Unbuntu.)  
There are two ways of installing libcrypto.so.1.0.0  
1a. Download the package installer into /root if on Debian 9+.  
<b>&nbsp;&nbsp;&nbsp;wget --no-check-certificate https://github.com/inwtx/mixmaster/raw/master/debian-x64-libcrypto-so-1-0-0.deb</b>  
In /root, run the following:  
<b>&nbsp;&nbsp;&nbsp;sudo dpkg -i debian-x64-libcrypto-so-1-0-0.deb</b>  

1b. If the package doesn't install correctly for some reason, download this into /root if on Debian 9+.  
<b>&nbsp;&nbsp;&nbsp;wget --no-check-certificate https://github.com/inwtx/mixmaster/blob/master/libcrypto.so.1.0.0.tar.gz</b>  
<b>&nbsp;&nbsp;&nbsp;tar zxvf libcrypto.so.1.0.0.tar.gz</b>  
Copy the libcrypto.so.1.0.0 file to /usr/lib/x86_64-linux-gnu/ if directory exist. Otherwise copy it to /usr/lib/.  
<b>&nbsp;&nbsp;&nbsp;cp libcrypto.so.1.0.0&nbsp;&nbsp;/usr/lib/x86_64-linux-gnu</b>  
    
III.
Open and setup the /var/mixmaster/mix.cfg file.  
After setup, execute this to change white spaces to tabs:  
<b>&nbsp;&nbsp;&nbsp;unexpand -a mix.cfg</b>  
  
Go to /var/mixmaster:  
<b>&nbsp;&nbsp;&nbsp;cd /var/mixmaster</b>  
Execute this instruction to make sure owner is correct:  
<b>&nbsp;&nbsp;&nbsp;chown mix:mix *</b>  
  
Go to user mix:  
<b>&nbsp;&nbsp;&nbsp;su - mix</b>  
  
(The next instructions/modifications must always be executed while in user mix)  
  
Setup mixmaster statistics download cronjob:  
<b>&nbsp;&nbsp;&nbsp;crontab -e</b>   
Enter the next line:  
<b>&nbsp;&nbsp;&nbsp;0 6,12,23 * * * /usr/bin/mixmaster-getstats</b>   
  
Starting mixmaster the first time:  
<b>&nbsp;&nbsp;&nbsp;mixmaster -G</b>  
<b>&nbsp;&nbsp;&nbsp;mixmaster --update-stats</b>  
<b>&nbsp;&nbsp;&nbsp;mixmaster --update-pinger-list</b>  
<b>&nbsp;&nbsp;&nbsp;mixmaster -D</b>  
<b>&nbsp;&nbsp;&nbsp;exit</b>  
  
After the initial start, just start mixmaster with:  
<b>&nbsp;&nbsp;&nbsp;mixmaster -D</b>  
  
To exit user mix type:  
<b>&nbsp;&nbsp;&nbsp;exit</b>   
  
  
Example of my former inwtx.net mix.cfg file:
  
  
```
# mix.cfg -- installed Tue 27 Dec 15:30:00 CST 2021
# NOTE! Place tabs between config names and parameter
# Start with: mixmaster -D

SENDMAIL        /usr/sbin/sendmail -t

###EXTFLAGS testing

# Where to store non-remailer messages (all messages deleted here):
MAILBOX         mbox
#MAILABUSE      mbox.abuse
#MAILBLOCK      mbox.block
#MAILUSAGE      mbox.usage
#MAILANON       mbox.anon
#MAILERROR      mbox.error
#MAILBOUNCE     mbox.bounce

REMAIL          y
MIDDLEMAN       y

PASSPHRASE      MakeThisAnything
ALLPINGERSURL   https://raw.githubusercontent.com/remops/allpingers/master/allpingers.txt

##/usr/bin/mixmaster-getstats  # elvis' stats pgm - must be executed daily in .forward 'mix' cron

BINFILTER       y
AUTOBLOCK       y
AUTOREPLY       n

ERRLOG          error.log
VERBOSE         1
KEYLIFETIME     43d
KEYOVERLAPPERIOD        12d
KEYGRACEPERIOD  5d
MINREL          99

# Remailer name and addresses
REMAILERADDR    mix@inwtx.net
ANONADDR        mix@inwtx.net
COMPLAINTS      abuse@inwtx.net

SHORTNAME       inwtx
REMAILERNAME    inwtx Anonymous Remailer
ANONNAME        The inwtx Anonymous Remailer

# Supported formats:
MIX             y
PGP             n
UNENCRYPTED     n

# Maximum message size in kB (0 for no limit):
# (Note: Due to the small size of the VPS, this probably should be limited.)
SIZELIMIT       1024

# Usenet news:
NEWS            mail2news@neodome.net
ORGANIZATION    Anonymous Posting Service
MID             y

# Remailing strategy:
##MAILINTIME      1m
SENDPOOLTIME    5m
POOLSIZE        20
RATE            65
INDUMMYP        10
OUTDUMMYP       90
#INDUMMYP       0
#OUTDUMMYP      0

IDEXP           7d
PACKETEXP       7d
```
