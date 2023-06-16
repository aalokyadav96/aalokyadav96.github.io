---
layout: post
title:  "Golang mega tutorial : Create a Blog in Go and Redis"
date:   2023-06-16 02:58:00
categories: Golang
---

Hi 

I am assuming you have both Go and Redis installed.
If not, you can go to their websites and find a suitable installer that works for you.

I am using Go 1.18 as this is supported on Windows 8.1.

Redis : try Redis for windows or their online free redis server.

Go provides built-in http server but that does not resolve URL parameters so, we will be using httprouter as it is one of the the smallest and fastest web framework for go.

You can use "chi" or "httprouter" both have similar syntax.

let's get the hello world server running:
create a file named main.go in a new folder
and copy the below code in the file.
<pre>
<code>
package main

import (
    "fmt"
    "net/http"
    "log"

    "github.com/julienschmidt/httprouter"
)

func Index(w http.ResponseWriter, r *http.Request, _ httprouter.Params) {
    fmt.Fprint(w, "Hello")
}

func main() {
    router := httprouter.New()
    router.GET("/", Index)

    log.Fatal(http.ListenAndServe("localhost:5000", router))
}
</code>
</pre>
Now, open the command line `cmd` or terminal in the current folder.

and type `go mod init megablog`
after that, type `go mod tidy`

the init command will create a mod file and the tidy command will install all the dependencies or imports we have added.
see below
<pre>
<code>
F:\gotestcode>go mod init megablog
go: creating new go.mod: module megablog
go: to add module requirements and sums:
        go mod tidy

F:\gotestcode>go mod tidy
go: finding module for package github.com/julienschmidt/httprouter
go: found github.com/julienschmidt/httprouter in github.com/julienschmidt/httprouter v1.3.0

</code>
</pre>

now go to the terminal 
and type `go run main.go` and press enter

open your favourite browser and go to URL : `localhost:5000` or `127.0.0.1:5000`.
you will see the "Hello" message. Congratulations, it is working.