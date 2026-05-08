# Dirty Frag Checker

[Dirty Frag](https://github.com/V4bel/dirtyfrag) is comprised of two vulnerabilities. One in esp ipsec, and one in the rxrpc functionality. 

This repo splits them out into their own files, and renders them functionally harmless. 
These two exploits just prove that you can use the various exploits, rather than overwriting anything important like `su`

This will just choose `/etc/motd`, `/etc/hostname` or `/etc/machine-id` and attempt to use the exploit against them. 

This is ideal for production workloads to check whether or not your mitigation has actually worked or not. 


## Building 

```sh
gcc -O0 -Wall -o rxrpc rxrpc.c -lutil
gcc -O0 -Wall -o ipsec espipsec.c -lutil 
```

## Usage
Both of these only take one `argv` arg, which is the file to write arbitrary (no shell code here) bytes to. 

After, remember to do:
```sh
echo 1 > /proc/sys/vm/drop_caches 
```

To flush the page cache so the changes go away.

