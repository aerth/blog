+++
date = "2016-02-24T06:57:03Z"
tags = ["code", "gnusocial"]
title = "gnusocial command line"

+++

#qo-quitter

### A GNU Social client for the future

```
go get -v -u github.com/aerth/go-quitter

```
now try it out

```
go-quitter config # saves your credentials safely
qo-quitter read fast
watch -n 60 GNUSOCIALNODE=quitter.se go-quitter read fast
go-quitter mentions 
go-quitter post hello world
go-quitter post # enters post mode, better handling of URL-unsafe symbols like ! or #
GNUSOCIALUSER=test GNUSOCIALPASS=test GNUSOCIALNODE=quitter.se go-quitter post Wow.
GNUSOCIALUSER=test GNUSOCIALPASS=test GNUSOCIALNODE=quitter.se go-quitter post \#hashtags work\! Symbols arent as easy\!
```


## "I want to post real quick using python3!"

anonquit is a python3 script i found and it was all in spanish so I made an english 
branch because i dont know how real translations would work.

```
git clone https://github.com/aerth/anonquit
cd anonquit
# now set up account with:
anonquit -a 

```

Hey let me know what you think.
