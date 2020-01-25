# SSH Keys

### Check for existing keys

`ls ~/.ssh`

### Generate a new key pair

`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

Add a passphrase if desired for additional security. "your_email@example.com" is to help identify the key and can be any name - email is not required.

### Install public key to remote machine

`ssh-copy-id username@hostname`

This connects but does not log on, however, it will require the password (not passphrase) for the connecting user.

---
# Reference 

https://www.ostechnix.com/configure-ssh-key-based-authentication-linux/