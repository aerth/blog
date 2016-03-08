+++
date = "2016-02-11T08:35:14Z"
tags = ["golang", "code"]
title = "easy cross compiling"

+++

Build for Mac OS X, Windows, Windows 64, linux-arm, netbsd-amd64, and a 
plethora of others. Modify to your needs, like anything else in the 
world.

The following code outputs these binary files:

```sh
$ ./build-archs.sh Version10
$ ls Version10/

Version10_freebsd-386
Version10_netbsd-386
Version10_osx-amd64 
Version10_freebsd-amd64 
Version10_netbsd-amd64 
Version10_windows-386.exe 
Version10_linux-386 
Version10_openbsd-386 
Version10_windows-amd64.exe 
Version10_linux-amd64 
Version10_openbsd-amd64 
Version10_linux-arm 
Version10_osx-386


```

```
#!/bin/sh
version="$1"
mkdir $1 > /dev/null 2>&1
name="../""$version""/""$version""_"

# CGO_ENABLED=1
GOOS=darwin GOARCH=amd64 go build -o "$name"osx-amd64

GOOS=darwin GOARCH=386 go build -o "$name"osx-386

GOOS=freebsd GOARCH=amd64 go build -o "$name"freebsd-amd64

GOOS=freebsd GOARCH=386 go build -o "$name"freebsd-386

GOOS=netbsd GOARCH=amd64 go build -o "$name"netbsd-amd64

GOOS=netbsd GOARCH=386 go build -o "$name"netbsd-386

GOOS=openbsd GOARCH=amd64 go build -o "$name"openbsd-amd64

GOOS=openbsd GOARCH=386 go build -o "$name"openbsd-386

GOOS=linux GOARCH=arm go build -o "$name"linux-arm

GOOS=linux GOARCH=amd64 go build -o "$name"linux-amd64

GOOS=linux GOARCH=386 go build -o "$name"linux-386

GOOS=windows GOARCH=amd64 go build -o "$name"windows-amd64.exe

GOOS=windows GOARCH=386 go build -o "$name"windows-386.exe

```


## Update:

Run this script before, to make sure we have the library and runtimes for each OS/ARCH

```
#!/bin/sh
# Copyright 2016 aerth@sdf.org
# MIT License

if [ -z "$1" ]; then
echo
echo Run this only once. Sleeping for 5 seconds, and starting the bootstraps.
echo Usage: $0 once
echo
sleep 1
exit 0
fi

if [ -z "$GOROOT" ]; then
echo
echo Set GOROOT !!!!
echo Usage: $0 once
echo
sleep 1
exit 0
fi
cd $GOROOT/src
sleep 5


echo \"Im merely remarking upon the paradox of asking a masked man who he is.\"
sudo GOOS=darwin GOARCH=386 ./make.bash --no-clean
sudo GOOS=darwin GOARCH=amd64 ./make.bash --no-clean
sudo GOOS=freebsd GOARCH=386 ./make.bash --no-clean
sudo GOOS=freebsd GOARCH=amd64 ./make.bash --no-clean
sudo GOOS=netbsd GOARCH=386 ./make.bash --no-clean
sudo GOOS=netbsd GOARCH=amd64 ./make.bash --no-clean
sudo GOOS=openbsd GOARCH=386 ./make.bash --no-clean
sudo GOOS=openbsd GOARCH=amd64 ./make.bash --no-clean
sudo GOOS=linux GOARCH=386 ./make.bash --no-clean
sudo GOOS=linux GOARCH=amd64 ./make.bash --no-clean
sudo GOOS=linux GOARCH=arm ./make.bash --no-clean
sudo GOOS=windows GOARCH=386 ./make.bash --no-clean
sudo GOOS=windows GOARCH=amd64 ./make.bash --no-clean


echo ""
echo ""
echo "ALL DONE! Go build!"
echo ""
echo ""
echo ""

```
