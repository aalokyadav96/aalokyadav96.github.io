---
layout: post
title: Golang &colon; Compilation and other things
tags:
- text
- golang
---


When you compile, Go creates a temporary file in <code>`C:\Users\me\AppData\Local\go-build`</code> folder. Make sure to clean it to avoid waste.


### Direct Running

Run single file:
<code>go run filename</code>

In case of multiple files:
<code>go run filename</code>

### Building an Executable .exe

Simply type <code>go build</code>
and the go compiler will take all files and make an executable which you can run by typing it's name.

### Using Makefiles
<code>
	run:
</code><br>&nbsp;&nbsp;&nbsp;&nbsp;
<code>
		go run main.go routes.go db.go 
</code>

Then you can run or compile your code with 
<code>make run</code>


### Quirks

1. All files should have a package definition on the top. 
2. Anything that's not used, will give error.
3. Any global variable outside functions should be declared as <br><code>var variableName dataType</code><br> or <br><code>var variableName dataType = value</code> 
4. Filename clashes might occur. So, make sure you use a good naming convention. For example : stb_images.go