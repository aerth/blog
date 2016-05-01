
+++
date = "2016-04-16T00:00:00Z"
title = "seconf - secure configuration library"

+++

You know how you start a program and it needs environmental variables with some AWS keys or something?

Or a configuration file, read once at startup and left just laying around.

Well seconf adds a layer of protection to this area of the program.  

To someone who grabs a misplaced backup or something, it will be an encrypted file.

To you, running your program, it will be a seamless experience.

See it in action:

  https://github.com/aerth/cosgo
  https://github.com/aerth/go-quitter/cmd/go-quitter
  https://github.com/aerth/secenv
  https://github.com/aerth/seconf


This really needs some testing in the real world! I have been using it for a couple sites for over a month (april 2016)

And go-quitter has been using it since it existed, they were built together.

Enjoy!
