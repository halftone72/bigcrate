# Misc notes
	

### Steam alternative drive

You may move ~/.steam to another partition, say /mnt/games/steam, then create symbolic link.
ln -s /mnt/games/steam ~/.steam



---

````
From my own experience:
 • backup your _.dotfiles_ and _/etc_ in a git repository; Keybase is good for this, GitLab too.
 • _borgbackup_ your server.
 • harden your _sshd_config_, _pg_hba.conf_ and whatever else, don't rely on one thing to protect the others.
 • get familiar with your firewall, _fail2ban_, _SELinux_ if it's installed and other layers such as a web application firewall or network intrusion detection system (this is a pretty heavy layer on its own, _pfSense_, _snort_, _suricata_, etc -- doesn't have to be that, just 'not nothing'; _shadowd_ is smaller).
 • learn _bash_ (enough to write your own conditions/flow control, at least), explore other old-and-gold unix programs like awk/sed, tr, cut, etc; I like https://man.cx for man pages. You can usually _/whatever_ and get it.
 • always document what you did (someone else said this); just take notes as you go through docs, you're going to read them (and re-google them) anyway.
 • google a lot; explore programs you never intend to use; read about some language that you may never use.
 • digital ocean's guides are great; vultr too.
 • self-hosting is worth it, even if you forego the r5xx/6xx/7xx server and just get yourself a RaspberryPi/Pine64. You'll save money on scaling up your homelab and you'll gain more experience from the actual fear of others hacking "yours". Those little boards pay for themselves (vs VPS) within a year.
 • Ansible is neat; containers too.
 • If you have 2 ethernet ports, isolate internet traffic.
Those things have helped me a lot. My own notes have saved me multiple times. I'm with the person who argued against a VPS. The only reason I'd suggest it instead of having your own is the electricity costs of a 24/7 server. If you rent/don't worry about it, jump into the deep end.
Edit: Other Services
 • _keybase_: It's awesome.
 • _matrix-synapse_/_coturn_: chat server, great protocol.
 • _gitlab_/_gitea_/_gogs_: your own git server.
 • https://repl.it: not something you host, but languages you try.
 ````
