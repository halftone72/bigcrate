# SnapRAID

http://www.havetheknowhow.com/Configure-the-server/Install-SnapRAID.html

https://www.snapraid.it/faq

### Create directory and get files ready to compile (version 11.3 as of 13 January)

```
mkdir ~/snapraid
sudo chmod a+w ~/snapraid
cd ~/snapraid
wget https://github.com/amadvance/snapraid/releases/download/v11.3/snapraid-11.3.tar.gz
tar -xzf snapraid-11.3.tar.gz
```

### Compile

```
cd ~/snapraid/snapraid-11.3
./configure
make
make check
```

Errors may display. allow to run all the way through. Watch for

```
Everything OK
===== Regression test completed with SUCCESS!
===== Please ignore any error message printed above, they are expected!
===== Everything OK
make[1]: Leaving directory '/home/halftone72/snapraid/snapraid-11.3'
```

Install
`sudo make install`

Copy config file snapraid.conf to /etc/snapraid.conf

Save, then sync
`sudo snapraid sync`

Scrub data for errors
`sudo snapraid scrub`
