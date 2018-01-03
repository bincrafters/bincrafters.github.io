---
layout: post
title: 'Thinking about conanfile.py'
tags: [Conan.io]
---

This is a short PSA to all Conan packagers to help avoid a category of pitfall we've seen several times.  When you start working with Conan, you discover that they use a python class as their descriptor format.  This is absolutely a great design, however, there are things that work in a normal python class, which won't work in a ConanFile. 

## The Trap: A Simple Example

```python

class MyPackageConan(ConanFile):
	name = "name"
	version = "1.0.0"
	something = ""
	some_dynamic_path = ""
	
    def source(self):
        self.something = "Hello"
		some_dynamic_path = find_some_dynamic_path()

    def build(self):
        print self.something # prints "Hello"
		use_some_dynamic_path(some_dynamic_path)

    def package(self):
        print self.something # prints "Hello"
		use_some_dynamic_path(some_dynamic_path)
```

If you have the recipe above and run `conan create .`, your recipe will behave as expected.  The `build()` and `package()` will successfully share state, and the example will be able to successfully build and package based on the `some_dynamic_path` variable that was set in the `source()` method. 

You might be happy and think you created a great package.  Unfortunately, it's flawed. 


## Different Conan Commands
The challenge is that there are many different Conan commands which utilize different methods from the recipe, often in isolation.  For example, if the binary is present, the `source()`, `build()`, methods won't be called at all when you run `conan package` command.  The recipe in the example above will not work with the `conan build` and `conan package` commands. Obviously, it's really annoying to have recipe's for which some commands work and not others.  The fact that the `conan create` recipe works fine adds to the problem a bit, because it means many new packagers won't discover the problem until some later date.  Often times, it's other package users who discover the problem.  

## Updating Your Mental Model
You should imagine that a new instance is created for each method execution, and the instance is destroyed. The `conan create` command doesn't work like this, but several others do.  So, if you think of it this way you will avoid the aforementioned pitfalls.  Here's some pseudocode that demonstrates it visually:

Here's how you probably think about it now: 

```python
class MyPackageConan(ConanFile):
	name = "name"
	version = "1.0.0"
	# etc...
	
	def source(self):
		# source stuff

	def build(self):
		# build stuff

	def package(self):
		# package stuff
```	
		
Here's how you should think about it instead: 

```python
class MyPackageConan(ConanFile):
	name = "name"
	version = "1.0.0"
	# etc...
	
	def source(self):
		# source stuff
```	


```python
class MyPackageConan(ConanFile):
	name = "name"
	version = "1.0.0"
	# etc...

	def build(self):
		# build stuff
```	

```python
class MyPackageConan(ConanFile):
	name = "name"
	version = "1.0.0"
	# etc...
	
	def package(self):
		# package stuff
		
```	

## Summary
It seems trivial to think about each method invocation is a separate instance, however most people dive in and start experimenting.  In this case, people often start testing with the `conan create` command and might get the idea that it's the only command that they need to think about.  As such, it gives these scientists a "false positive" that certain things work, and they go on experimenting with other things.  It's not a real "false positive" because it does "work", but new users "don't know what they don't know" about the other commands.  So, hopefully we've shed light on an otherwise shady topic. 