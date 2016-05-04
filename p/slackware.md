
+++
date = "2016-05-01T05:31:56Z"
title = "slackware scripts"

+++

Here it is: `git clone https://github.com/aerth/sh.git`

youtube-list downloads and installs youtube-dl if you don't have it 
already.

ssh-tunnel makes it easy to SOCKS5 on SSH.

suprslack - simple SlackBuilds and security upgrades

```

|-- README
|-- bin
|   |-- icanhazip
|   `-- youtube-list
|-- install.sh
|-- rc.d
|   |-- adminer
|   |-- hdmi-hi
|   |-- hdmi-low
|   |-- iptables
|   |-- network-time
|   |-- ssh-tunnel
|   `-- vga-1440
`-- sbin
    |-- mariadb_init
    `-- suprslack

```


Here is nice to add to your /etc/rc.d/rc.inet1 
It asks you on boot whether you want to DHCP or not.

Find the DHCP section and these lines:

```

        echo "do dhcp?"
        read CONTINUEDHCP
        if [ "$CONTINUEDHCP" == "yes" ]; then
        echo "/etc/rc.d/rc.inet1:  /sbin/dhcpcd -t ${DHCP_TIMEOUT[$i]:-10} ${DHCP_OPTIONS} ${1}" | $LOGGER
        /sbin/dhcpcd -t ${DHCP_TIMEOUT[$i]:-10} ${DHCP_OPTIONS} ${1}
        fi

```
