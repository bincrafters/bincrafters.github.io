---
layout: post
title: 'Thinking About Conanfile'
tags: [Conan.io]
---

This is a short PSA to all Conan packagers to help avoid a category of pitfall we've seen several times.  When you start working with Conan, you discover that they use a python class as their descriptor format.  This is absolutely a great design, however, there are things that work in a normal python class, which won't work in a Conanfile. 

It's not a normal class
Python does not load your `conanfile.py` into memory, and then execute each method sequentially.  It looks like it does in the logs, but it doesn't.  A new instance is created for each method execution.  The documentation provides guidelines on things you should not do because of this behavior (such as share runtime state between method calls) but it's still easy to fall into normal OOP patterns.  So, here's some pseudocode that you can use to update your mental model.  We hope it will help other packagers avoid common pitfalls. 

Here's how you probably think about it

```python
class MyPackageConan(conanfile):
	name = "name"
	version = "1.0.0"
	# etc...
	
	def source(self):
		# source stuff

	def build(self):
		# source stuff

	def package(self):
		# source stuff
```	
		
Here's how you could think about it instead, because this is how Conan loads and executes it: 

```python
class MyPackageConan(conanfile):
	name = "name"
	version = "1.0.0"
	# etc...
	
	def source(self):
		# source stuff
```	


```python
class MyPackageConan(conanfile):
	name = "name"
	version = "1.0.0"
	# etc...

	def build(self):
		# source stuff
```	

```python
class MyPackageConan(conanfile):
	name = "name"
	version = "1.0.0"
	# etc...
	
	def package(self):
		# source stuff
		
```	

## Summary
It seems trivial to understand that each method invocation is a separate instance, however we still see people making mistakes like this, which indicates that more educational content on the topic might have some value to some reaaders. 