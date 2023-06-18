---
layout: post
title:  "Golang mega tutorial :  Templates"
date:   2023-06-18 03:53:00
categories: Golang
---

in Go, there are 2 template packages: text/template and html/template.
You will need to read both documentations.

We will be using html/template for front-end.

create a folder named 'templates' in your root directory.

In your main.go, 
`import "html/template"`

after that, declare a global variable as:

`var tmpl = template.Must(template.ParseGlob(templates/*.html))`

`template.Must` returns error if some variable or template is missing.
<br>
`template.ParseGlob` indexes all the templates so that you do not have to read files again and again.

now in 'templates' folder, create a new file named `index.html` and put below HTML code in it.

<pre>
<code>
&lt;!DOCTYPE HTML&gt;
&lt;html&gt;
&lt;body&gt;
&lt;p&gt;{ { &period; } }&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
</code>
</pre>

then replace `fmt.Fprint(w, "Hello")` with 
`tmpl.Execute(w,index.html,"Hello")`

below is the final code:

<pre>
<code>
package main

import (
    "fmt"
    "net/http"
    "log"

    "github.com/julienschmidt/httprouter"
)

var tmpl = template.Must(template.ParseGlob(templates/*.html))

func Index(w http.ResponseWriter, r *http.Request, _ httprouter.Params) {
    tmpl.Execute(w,index.html,"Hello")
}

func main() {
    router := httprouter.New()
    router.GET("/", Index)

    log.Fatal(http.ListenAndServe("localhost:5000", router))
}
</code>
</pre>

you should see the same Hello on refreshing the browser. But this time, as HTML paragraph.