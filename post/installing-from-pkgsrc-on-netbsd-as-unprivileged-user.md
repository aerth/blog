+++
date = "2016-02-12T07:03:39Z"
tags = ["netbsd", "pkgsrc"]
title = "installing from pkgsrc on netbsd as unprivileged user"

+++

$ cat ~/.zshrc

```

                                                                              
# aerth local mk.conf                                                           
export MAKECONF=$HOME/etc/mk.conf                                               
export PREFIX=$HOME/pkg                                                         
                                                                                
# aerth gopath                                                                  
export GOPATH=$HOME/work                                                        
export PATH=$HOME/bin:$GOPATH/bin:$HOME/usr/pkg/bin:$PATH                       
export GOARCH=amd64                                                             
export GOOS=netbsd                                                              
                                                                                
# aerth local goroot                                                            
export GOROOT=$HOME/usr/pkg/go                                                  
                                                                                
PATH=${PATH}:/sys/sdf/bin                                                       
MANPATH=${MANPATH}:/sys/sdf/man     

```


