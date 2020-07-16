### FoldingAtHome

Install client
`wget https://download.foldingathome.org/releases/public/release/fahclient/debian-testing-64bit/v7.4/fahclient_7.4.4_amd64.deb`
`sudo dpkg -i —force-depends fahclient_7.4.4_amd64.deb`

Edit config file
`sudo nano /etc/fahclient/config.xml`

```
<config>
  <!— Client Control —>
  <fold-anon v=‘true’/>

  <!— User Information —>
  <user v=‘halftone72’/>

  <!— Folding Slots —>
  <slot id=‘0’ type=‘CPU’>
    <paused v=‘true’/> 
  </slot>              
  <slot id=‘1’ type=‘GPU’>
    <paused v=‘true’/> 
  </slot>                      
</config> 
```

Stop service
`sudo /etc/init.d/FAHClient stop`

Move init script
`sudo mv /etc/init.d/FAHClient /usr/local/bin`

Create service file
`sudo nano /etc/systemd/system/fahclient.service`

Add contents to service file

```
[Unit]
Description=Folding@Home V7 Client
Documentation=https://folding.stanford.edu/home/the-software/

[Service]
Type=simple
PIDFile=/var/run/fahclient.pid
ExecStart=/usr/local/bin/FAHClient -v -u root start
ExecReload=/usr/local/bin/FAHClient -v -u root restart
ExecStop=/usr/local/bin/FAHClient -v -u root stop
KillMode=process

[Install]
WantedBy=multi-user.target
```

Modify file ownership and permissions
`sudo chown root:root /etc/systemd/system/fahclient.service`
`sudo chmod u=rw,go=r /etc/systemd/system/fahclient.service`

Reload systemd manager config
`sudo systemctl daemon-reload`

Check system status
`sudo systemctl status —full fahclient.service`

Setup service to auto-start on reboot
`sudo systemctl enable fahclient.service`

Stop and start service
`sudo systemctl stop fahclient.service`
`sudo systemctl start fahclient.service`

Use the web client to configure name and confirm GPU is picking up jobs
http://client.foldingathome.org

---

# Reference

FAH command line options
https://foldingathome.org/support/faq/installation-guides/linux/command-line-options/

FAH convert to systemd service
http://pedroivanlopez.com/install-fahclient-linux-systemd-service-unit/

