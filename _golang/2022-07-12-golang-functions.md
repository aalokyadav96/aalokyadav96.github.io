---
layout: post
title: Golang &colon; Functions, Methods and Interfaces
tags:
- text
- golang
---

Functions, Methods, Procedures .. what else?

## Functions

	func()
	func(x int) int
	func(a, _ int, z float32) bool
	func(a, b int, z float32) (bool)

## Dynamic Functions
	func(prefix string, values ...int)
	func(a, b int, z float64, opt ...interface{}) (success bool)
	func(int, int, float64) (float64, *[]int)
	func(n int) func(p *T)