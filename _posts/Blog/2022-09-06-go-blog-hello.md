---
layout: mego
title: "Golang mega tutorial - part 1 hello-world"
categories: ["tutorial"]
permalink: "golang-web-mega-tutorial-part-i-hello-world"
tags:
- tutorial
---


## Install Golang

Go to The Golang Website and download the appropriate file for your operating system.
I am using Windows 8.1, but I have Linuxified my system. So, everyone will find the tutorial easy to follow.

## Create your first Go program

Create a file named <em>main.go</em> and write the code given below.

<pre><code>
package main

func main() {
	print("Hi")
}
</code></pre>

now, save it and open your console / terminal / commandPrompt

type _go run main.go_ and press enter.

you should see "Hi" printed on the standard output

Okay, so what is this code! 
The 'package X' is a mandatory condition for any golang file and it should be the first line in every file. This tells the compiler that this file belongs to the main package.  You can name your package anything.

Then there is main function. Unlike C/C++, we write the word 'func' before function name. all else should be self explanatory.

## Importing Packages

You import packages using 'import packageName' below the package name declaration. Quite similar to Python but with a little twist.

Import populates the module namespace to be used in the file

Lets consider the below self explanatory examples:

<pre><code>

import "os"	// imports 'os' module 
import  (	// another way of importing multiple packages
	. "math"	// imports math module in global namespace
	rndm "rand"	// imports the 'rand' random module with rndm as alias

	"github.com/lib/pq"	// imports pq module from a remote repository
)
</code></pre>


you can read more about it in golang documentation


## Create an HTTP server

Now, let's create a web server. We will update our main.go file.

Go has a package called "net/http" that handles all the web serving tasks. We will import it to start our web server

<pre><code>
package main

import (
	"fmt"
	"net/http"
)

func main() {
	http.HandleFunc("/", Index)

	http.ListenAndServe(":4000",nil)	
}

func Index(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w,"Hello")
}
</code></pre>


## Environment variables


create a '.env' file and add the below variable to it.

PORT=4000

Now, add the below function to our main.go file
<pre>
<code>
import "os"
...
 func GetPort() string {
 	var port = os.Getenv("PORT")
 	if port == "" {
 		port = "4000"
 		fmt.Println("INFO: defaulting to " + port)
 	}
	fmt.Println("on port :  " + port)
 	return ":" + port
}
...
</code>
</pre>
also, update our main function as

<pre><code>
...
func main() {
	port := GetPort() 
	http.HandleFunc("/", Index)
	http.ListenAndServe(GetPort(),nil)	
	fmt.Println("Listening on Port : ", port)
}
...
</code></pre>

now run it and go to localhost:4000 OR 127.0.0.1:4000 in your favourite browser.

You should see Hello on your webpage