# Debian mixmaster remailer installation instructions.

In /root of your server:  
wget --no-check-certificate https://github.com/inwtx/mixmaster/blob/master/Debian_x64_mixmaster_3.1-1_amd64.tar.gz  
tar zxvf Debian_x64_mixmaster_3.1-1_amd64.tar.gz  
sudo dpkg -i ./Debian_x64_mixmaster_3.1-1_amd64.deb  
    
Mixmaster should now be installed.  
    
Download this if on Debian 10+.  
wget --no-check-certificate https://github.com/inwtx/mixmaster/blob/master/libcrypto.so.1.0.0.tar.gz  
tar zxvf libcrypto.so.1.0.0.tar.gz  
Copy the libcrypto.so.1.0.0 to /usr/lib/x86_64-linux-gnu/  
cp libcrypto.so.1.0.0 /usr/lib/x86_64-linux-gnu/libcrypto.so.1.0.0  
    
Open and setup the /var/mixmaster/mix.cfg file.  
After setup, execute this:  
unexpand -a mix.cfg  
    
Go to user mix:  
su - mix  
    
Starting mixmaster the firse time:  
mixmaster -G  
mixmaster --update-stats  
mixmaster --update-pinger-list  
mixmaster -D  
exit  
  
 
