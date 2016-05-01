+++
date = "2016-03-13T07:03:27Z"
tags = ["rancher", "rancheros", "docker"]
title = "rancheros docker stuff"

+++

Run `ncdu` and figure out what is taking up all that space!

```
docker run -it -v /:/mnt:ro aerth/ncdu ncdu /mnt

```


The ncdu docker image is 8.061 MB
