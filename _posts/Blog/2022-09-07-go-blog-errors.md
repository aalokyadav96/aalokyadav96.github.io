---
layout: mego
title: "Golang mega tutorial - part 2 Handling Errors"
categories: ["tutorial"]
permalink: "golang-web-mega-tutorial-part-ii-handling-errors"
tags:
- tutorial
---


Our program worked!

You successfully printed 'Hello' in your browser.

But we ignored failures.
What if :

	-  the server didn't start
	-  the .env file doesn't exist

did you think about these issues? You should have. 
If you did, I appreciate that, pat yourself on the back.

## Emergency Emergency

Ok, let's change our code to be ready to handle errors.

<pre><code>
...
func main() {
...
	err := http.ListenAndServe(":4000",nil)
	if err != nil {
		log.fatal("Err: The server didn't start")
	}
...
}
...
</code>
</pre>

quite a unique error handling syntax. well, better than multiple try catch statements.
You will get used to it later.


## Creating makefiles

Now you might ask, 'why makefiles?' well, because it's easy to do 'make run' than writing the names of every single file in ' go run filenames' command.

If you are a fan of CMAKE, you can do similar setup. 

create a file named <em>makefile</em> and add the below content:

<pre><code>
run:
	go run main.go

</code></pre>

Now, we can just type 'make run' in cmd and make will take care of the run command.
We will later add a lot of file names and conditions.
