---
layout: post
title: Golang &colon; Miscellaneous
tags:
- text
- golang
---


type

nil

_

:= is not always applicable

<code>tmpl := template.ParseFiles() </code>will give error
need to use <code>var tmpl = template.ParseFiles() </code>
