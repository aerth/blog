+++
categories = ["x", "y"]
date = "2016-02-08T02:29:34Z"
tags = ["code", "golang"]
title = "golang setup"

+++

# Golang post-install

## Setting $GOPATH

I use this in my ~/.zshrc or ~/.bashrc or system-wide in /etc/profile on 
a new user, or new computer. I don't mess with it ever:
```
export GOPATH=$HOME/work # set gopath

export PATH=$PATH:$GOPATH/bin # put go programs in your path
```


Now I test with something simple, and useful: sift, a fast grep 
alternative.

```
go get -v -u github.com/svent/sift
testing
echo $PATH | sift $GOPATH
```

New projects are in namespaces, ``` cd $GOPATH/src/github.com ``` and 
``` mkdir $USER ``` then and you may create a new folder for a new 
project. If you were to enter the project directory and type ``` go 
build ``` you will see a new binary program in the source directory. But 
if you type ``` go install ``` you will find the new program in your 
$PATH !



