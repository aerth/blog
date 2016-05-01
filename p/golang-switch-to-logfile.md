+++
date = "2016-02-11T08:28:17Z"
tags = ["golang", "code"]
title = "golang switch to logfile"

+++


```

func OpenLog(){
f, err := os.OpenFile("./debug.log", os.O_RDWR | os.O_CREATE | 
os.O_APPEND, 0666)
if err != nil {
    log.Fatal("error opening file: %v", err)
		log.Fatal("MANDRILL_KEY is Crucial.")
		os.Exit(1)
}

log.SetOutput(f)
}

```

This function can be placed in main() like so:

```

	log.Printf("Starting Server on http://127.0.0.1:%s", *port)
	log.Println("Switching Logs to debug.log")
	OpenLog()
	log.Println("Server on", *port)

```
