+++
date = "2016-02-12T08:54:14Z"
tags = ["golang", "code"]
title = "golang ports"

+++

So there are a bunch of command line programs out there that are common between unix varieties.

Some not as common as others.

You may recognize:

``` cat ```, ```echo```, ```grep```

Here is a list of simple utilities, but in Golang!

```

package cat

import (
	"github.com/yuya-takeyama/argf"
	"io"
	"os"
)

func Cat(args []string) (int, error) {
	r, err := argf.From(args)
	if err != nil {
		return 2, err
	}
	_, err = io.Copy(os.Stdout, r)
	if err != nil {
		return 2, err
	}
	return 0, nil
}

```

# These are big

https://github.com/aisola/go-coreutils

https://github.com/EricLagergren/go-coreutils

https://github.com/surma/gobox

https://github.com/lopopolo/unixtools
