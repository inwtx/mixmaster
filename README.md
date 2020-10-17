# Debian mixmaster remailer installation instructions.

I. In /root of your server:  
<b>&nbsp;&nbsp;&nbsp;wget --no-check-certificate https://github.com/inwtx/mixmaster/raw/master/Debian_x64_mixmaster_3.1-1_amd64.deb</b>  
<b>&nbsp;&nbsp;&nbsp;sudo dpkg -i ./Debian_x64_mixmaster_3.1-1_amd64.deb</b>  
    
Mixmaster should now be installed.  
    
II. (Step II can be bypassed if installing on Unbuntu.)
There are two ways of installing libcrypto.so.1.0.0  
1. Download the package installer into /root if on Debian 10+.  
&nbsp;&nbsp;&nbsp;wget --no-check-certificate https://github.com/inwtx/mixmaster/raw/master/debian-x64-libcrypto-so-1-0-0.deb  
In /root, run the following:  
&nbsp;&nbsp;&nbsp;sudo dpkg -i debian-x64-libcrypto-so-1-0-0.deb  

2. If the package doesn't install correctly for some reason, download this into /root if on Debian 10+.  
&nbsp;&nbsp;&nbsp;wget --no-check-certificate https://github.com/inwtx/mixmaster/blob/master/libcrypto.so.1.0.0.tar.gz  
&nbsp;&nbsp;&nbsp;tar zxvf libcrypto.so.1.0.0.tar.gz  
Copy the libcrypto.so.1.0.0 file to /usr/lib/x86_64-linux-gnu/ if directory is present. Otherwise copy to /usr/lib/.  
&nbsp;&nbsp;&nbsp;cp libcrypto.so.1.0.0&nbsp;&nbsp;/usr/lib/x86_64-linux-gnu/  
    
III.
Open and setup the /var/mixmaster/mix.cfg file.  
After setup, execute this to change white spaces to tabs:  
&nbsp;&nbsp;&nbsp;unexpand -a mix.cfg  
  
Go to /var/mixmaster:  
&nbsp;&nbsp;&nbsp;cd /var/mixmaster  
Execute this instruction to make sure owner is correct:  
&nbsp;&nbsp;&nbsp;chown mix:mix *  
  
Go to user mix:  
&nbsp;&nbsp;&nbsp;su - mix  
    
Starting mixmaster the first time:  
&nbsp;&nbsp;&nbsp;mixmaster -G  
&nbsp;&nbsp;&nbsp;mixmaster --update-stats  
&nbsp;&nbsp;&nbsp;mixmaster --update-pinger-list  
&nbsp;&nbsp;&nbsp;mixmaster -D  
&nbsp;&nbsp;&nbsp;exit  
  
  
After the initial start, just start mixmaster with:  
&nbsp;&nbsp;&nbsp;mixmaster -D  
