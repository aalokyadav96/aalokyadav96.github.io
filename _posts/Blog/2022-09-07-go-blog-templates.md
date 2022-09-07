---
layout: mego
title: "Golang mega tutorial - part 3 Templates"
categories: ["tutorial"]
permalink: "golang-web-mega-tutorial-part-iii-templates"
tags:
- tutorial
---

There is a concept called 'Separation of concerns".
It states that Design and Logic should be separate.

Also there is The UNIX Philosophy that says, "every function should do one task and do it perfectly"
You can read more about it [here on Wikipedia](https://en.wikipedia.org/wiki/Unix_philosophy)


"Expect the output of every program to become the input to another, as yet unknown, program."

Throughout our tutorial, we will be following this philosophy. Also, we will return only one value per function. 
(Go to hell multiple return values!)

Okay, enough ranting, let's start!

## Templates

Go has 2 templating packages. one for text, other for html.

They are almost the same. the only difference is that html/template escapes evil inputs and automatically secures HTML output against certain attacks which we will later discuss.

now, create a 'templates' folder and create an 'index.html' file in that.

inside that index.html file, write the below code:

<pre><code>
<!DOCTYPE HTML>
&lt;p&gt;&#123;&#123;.&#125;&#125;&lt;/p&gt;

</code></pre>

<b>NOTE : If you would skip DOCTYPE declaration, the webpage will be treated like a text file. There will be no forms, no HTML tags, CSS. Only pure text</b>

So, moral of the story, do not forget <!DOCTYPE HTML>


that &#123;&#123;.&#125;&#125; notation means : 'anything returned by the server goes here'

now, let's move to our main function.
As we are doing SoC<sup>Separation of concerns</sup>, we will refactor our code.

so, our new main file looks like this. You can discard your previous code and start with this one.

<pre><code>
package main

import (
  	"fmt"
	"os"
	"log"
	"net/http"
	<mark>"html/template"</mark>
)

<mark>var tmpl = template.Must(template.ParseGlob("templates/*.html"))</mark>
<mark>
func main() {
	HandleRoutes()
}</mark>
func HandleRoutes() {
	http.HandleFunc("/", Index)
	err := http.ListenAndServe(GetPort(),nil)
	if err != nil {
		log.Fatal("Err: Server not started")
	}
}

func Index(w http.ResponseWriter, r *http.Request) {
//	fmt.Fprintf(w,"Hello")
<mark>	tmpl.ExecuteTemplate(w,"index.html","Hello")</mark>
}

 func GetPort() string {
 	var port = os.Getenv("PORT")
 	if port == "" {
 		port = "4000"
 		fmt.Println("INFO: defaulting to " + port)
 	}
	fmt.Println("on port :  " + port)
 	return ":" + port
}

</code></pre>

run it and see that the output hello is there.

## Understanding the code

Okay, it seems overwhelming, let's do it one by one.

'html/template' : the module which handles templates

<code>var tmpl = template.Must(template.ParseGlob("templates/*.html"))</code>

<em>template.Must</em> : "Makes sure that the file exists"
<em>template.ParseGlob</em> : "Parses all the files inside the templates folder, so, you don't have to do it again and again"

As you can see, we have emptied the main function and created a specific HandleRoutes() function for the specific task.

You can check out the documentation for all the other things we can do with templates. (Actually you can't do much with Golang templates.)

<b>I wish they had used Liquid Templating by Shopify just like Flask does</b>
(The only reason I dread Golang)


should be enough, see ya in next chapter