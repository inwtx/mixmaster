# Debian 9 mixmaster remailer installation instructions.

Note: Due to the changes to latest openssl, this mixmaster installation will only install on Debian 9.  It will not install on any other version of Debian.

In /root/:  
Get some things mixmaster needs if not already there.
```
sudo apt-get update
sudo apt-get install build-essential libpcre3 libpcre3-dev wget zlib1g-dev libncurses5-dev curl perl dc bc bison libssl-dev libbison-dev ssl-cert haveged
sudo apt-get install sudo gcc make
```
Install openssl-1.0.1u.tar.gz. This will not override the openssl your system currently has.
```
wget --no-check-certificate https://www.openssl.org/source/openssl-1.0.1u.tar.gz
tar xvf openssl-1.0.1u.tar.gz
cd openssl-1.0.1u
./config --prefix=/usr/local --openssldir=/usr/local/openssl
make
make test
sudo make install
```
Change the name of the above install to openssl101u to keep the system from adopting it as your primary openssl.
```
mv /usr/local/bin/openssl /usr/local/bin/openssl101u
```
In /home/mix:
```
wget --no-check-certificate https://github.com/inwtx/mixmaster/releases/download/v.1/D9mixmaster4096-master.zip
tar zxvpf mixmaster-3.1.debian9.tar.gz
cd mixmaster4096
./Install
```
