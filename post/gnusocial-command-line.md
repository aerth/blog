+++
date = "2016-02-24T06:57:03Z"
tags = ["code", "gnusocial"]
title = "gnusocial command line"

+++

# Go: qo-quitter

### "A GNU Social client for the future"

So you are on your shell account, and want to read, post, follow new people, etc. go-quitter allows you to access your GNU Social node's API from your terminal window.

Very work in progress. The entire code base is under complete transformation as I am learning Go. As of v0.0.8 the command go-quitter is separated from the go-quitter library. The library still may have things like "os.Exit()" and "fmt.Println()" which should not be there. They are being removed eventually.



```
go get -v -u github.com/aerth/go-quitter/cmd/go-quitter

```
now try it out

```
# saves your credentials safely for use on your public shell server account
go-quitter config

# this gets the latest 20
qo-quitter read

# more commands!
go-quitter help
```


# Python: Anonquit

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
