
+++
date = "2016-04-20T00:00:00Z"
title = "Go and plan 9"

+++

## Similarities

  * Colors
  * Mascots
  * Coding Styles
  * Some of the Authors
  * Philosophy

## Issues when combined

---insert explosion gif---

  * It seems Go and plan 9 don't like each other at the moment?
  * No real git, whatever. Always on "master" branch.

## Awesome!

  * Go is one of the few languages that one can write plan 9 software in.
  * plan 9 is a great Go programming environment.
  * I don't know much C and I don't plan on learning it.

## Installing Go on plan 9

April 2016: https://github.com/golang/go/issues/15234

See this link: http://comments.gmane.org/gmane.os.plan9.general/77606

And this one: http://9legacy.org/9legacy/doc/go/faq.html 

Watch some youtube videos.

## From 9front pdf

```
# automatically converted ca certs from mozilla.org
hget https://curl.haxx.se/ca/cacert.pem >/sys/lib/tls/ca.pem
# shell script that emulates git commands
hget http://9front.org/extra/rc/git >$home/bin/rc/git
chmod 775 $home/bin/rc/git
# fetch the repository
git clone https://go.googlesource.com/go
cd go
git checkout go1.4.2    # amd64 only: bootstrap 1.6 with 1.4.3
# build go
cd src
./make.rc
# install documentation
go get golang.org/x/tools/cmd/godoc

```


## Or try grabbing the bootstrap (prebuilt binary)

```
hget https://storage.googleapis.com/go-builder-data/gobootstrap-plan9-386.tar.gz > gobootstrap-plan9-386.tar.gz
# wait some time
tar xzf gobo*
cd gobo*
cd bin
go
# go 1560: suicide: sys: trap: fault read addr=0x4 pc=0x000bd985

```

## Or try Building go 1.4.3 from source

Open up `include/plan9/386/u.h` and comment the line that has a typedef for intptr. (thanks sirnewton_01)

```
cd src
./make.rc

```

Add this line to your $home/lib/profile:

```

// Add after the `webfs` line, in the `case terminal`.
bind -b /usr/go14/bin /bin
GOPATH=/usr/glenda/src/gopath
bind -b $GOPATH/bin /bin

```

Restarting!

` fshalt 1 `

Once booted it up, try out  `go version`

Should Output: ` go version go1.4.3 plan9/386 `

If you have the git rc script installed, You can now `go get`

`go get -v github.com/aerth/hashsum/cmd/hashsum`




[The one on the left](https://file.isupon.us/selif/go-plan9.png)


