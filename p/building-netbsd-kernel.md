+++
date = "2016-02-10T07:43:27Z"
tags = ["kernel", "netbsd"]
title = "building netbsd kernel"

+++

The steps to build a netbsd kernel are:

* ```cd /usr/src/sys/arch/<ARCH>/conf``` , where <ARCH> is your machine's architecture such as 'i386', 'sparc', 'mac68k'.

* ````cp GENERIC <MYCONF>```, where <MYCONF> is your name for this configuration. You could use your hostname, the machine type, or even your first name. Keep to letters, numbers, and _ characters.

*  ```vi <MYCONF>``` Initially you can skip this stage. You can remove 
drivers for CPU types, hardware, and devices you do not have or use, or 
even enable options, such as on i386 commenting out the 'pc0' line and 
enabling the 'vt0' to gain virtual consoles. A good start to determining 
what hardware drivers you definitely need to keep is to read the output 
of "dmesg" or "dmesg | grep ' at '". For every line containing '<XXX> at 
<YYY>' you need to keep the entries for both <XXX> and <YYY>. You should 
also read options(4) for information on the different kernel 
configuration options.

* ``` config <MYCONF> ```
* ``` cd ../compile/<MYCONF> ```
* ``` make depend ```
* ``` make ```
* ``` su ```
* ``` mv /netbsd /netbsd.old ```
* ``` mv netbsd /netbsd ```
* ``` shutdown -r now ```

If you have any problems: You should boot your 'netbsd.old' kernel 
in single user mode. The procedure varies from port to port depending on 
the boot procedure, but on i386 it would be:


* Press SPACE when the first NetBSD message appears

* ```boot netbsd.old -s```
  
* Then swap your kernel back:
```
        "fsck /"
        "mount /"
        "mv netbsd.old netbsd"
        "exit"
```
