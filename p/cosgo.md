
+++
date = "2016-04-16T00:00:00Z"
title = "cosgo - contact form server"

+++

Edit: Here is a link to a running cosgo instance: https://isupon.us

And newest version running: https://cosgo.herokuapp.com

Download: https://github.com/aerth/cosgo/releases/latest

While I was designing web sites, I noticed most of the logic in typical web sites happens *in the form*. For example:

  * Plain old Contact forms
  * "Request an estimate" for businesses
  * Surveys
  * *mail-order catalog* style purchasing

To upgrade your static site and implement a simple contact form means *installing and using PHP, Node.js, Ruby, CGI,* etc. So I created a contact form server that allows me to **"set it and forget it"**.

#### Cosgo aims to solve these problems:

  * I just want a **static HTML/CSS/JS web site** with a **customizable form** that **works**.
  * And I don't want to use any external components (unless I want to use an SMTP API like Sendgrid.)
  * And I don't want to install PHP, Apache, or anything else!


single instance is very standalone, and can very well be the only thing running on a server. You can `ssh` in and check your mailbox with `mutt -Rf cosgo.mbox`. Or you can `scp` it out whenever you like.

multiple instances of cosgo can exist behind nginx with fastcgi_pass, in `cosgo -fastcgi` mode. For example:

```

## Start 3 cosgo instances in fastcgi mode
cosgo -fastcgi -port 8081 &
cosgo -fastcgi -port 8082 &
cosgo -fastcgi -port 8083

## nginx would be configured to reverse proxy to fastcgi ports
# example.com > 8081
# example.net > 8082
# example.org > 8083

```

The config file is saved at ~/.cosgorc by default. It stores such things as `port`, `interface`, `sendgrid API key`, `mandrill API key`, and `logpath`.

Use the config like so: `cosgo -config -fastcgi` (run command twice)

#### Cosgo uses a couple spam-reduction techniques you may have heard about:
  * CSRF token
  * captcha code
  * email validation

#### Something probably not seen anywhere else is a new spam-reduction technique I am calling the "Dynamic POST Endpoint"
  * Every 42 minutes the POST endpoint changes. It is pretty much un-predictable.
  * With no static POST endpoint, it is a *little* tougher to launch a spam attack against cosgo powered sites.

#### Some things on the TODO list:
  * Feature: GPG encrypt the messages (in case of stolen mbox)
  * Feature: Add `GPG Public Key` field (allow easy replies)
  * Feature: Implement rate-limiting for visits and sends

Hope it works out for a lot of people! Upgrade **often**. Check https://github.com/aerth/cosgo/commits/master to see if you want to upgrade to the current ("master") version. Contributions are welcome. Submit an issue and/or pull request at https://github.com/aerth/cosgo
