+++
date = "2016-02-28T06:10:47Z"
tags = ["sh", "bash", "proxychains4", "SOCKS"]
title = "ssh tunnel apt-get SOCKS proxy"

+++

## For use behind a restrictive firewall.

Use SSH Tunnel for apt-get install (Debian)

```

$ cat bin/grab 
#!/bin/sh
echo Downloading $1 using proxychains4
sudo proxychains4 -q apt-get install -d $1
echo Installing $1 from .debs
sudo apt-get install $1

```

Set up proxychains4 for the SSH tunnel

```
$ tail /usr/local/etc/proxychains.conf 
#       proxy types: http, socks4, socks5
#        ( auth types supported: "basic"-http  "user/pass"-socks )
#
[ProxyList]
# defaults set to "tor"
#socks4 	127.0.0.1 9050
# but i use "ssh -D 1080 example.com" to set up a "poor man's VPN"
socks4	127.0.0.1 1080

```

Start the SOCKS proxy on 1080 and login to SSH server

```
$ cat bin/isp-relief 
#!/bin/sh
ssh -D 1080 $1

```

Use it


```

bin/isp-relief yourshellexample.com

```

```

bin/grab "pidgin pidgin-otr git golang"

```

This assumes you have set up a ~/.ssh/config file like so:

```

$ cat ~/.ssh/config

host example.com
IdentityFile ~/.ssh/id_rsa
user yourname
port 22

```

