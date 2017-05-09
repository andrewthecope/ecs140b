# Lecture 5 (4/25)
#Ecs140b

Leaving prolog behind (except program)

## Functional Programming
* evaluation of mathematical functions (things you can compute)
* **function**: correspondence between elements of an input domain and elements of a range

### Defining Characteristics of Function Programming
1. FP is statement (a state of a program does not change)
	* **state:** Data that can possibly changed by more than one piece of code. Need to consider data in every single state
		* state is a big challenge when thinking about concurrency 
		* state -> dependancies 
2. Consequently there are no side effects, a function doesn’t do anything but evaluate (return a value)
	* How do we manage IO (or something that needs side-effects to do anything)? There’s various ways he didn’t go into it
	* Side effects add complexity, particularly in big programs
3. Every function call with the same arguments returns the same result. Every time. 
	* principle called **referential transparency**
		* ax + b with given values will always be equal 
		* Don’t have to evaluate a function with the same arguments more than once (can just look it up)
		* only stuff that changes the return value of a function is arguments, nothing else
			* seems obvious, but sometimes global variables seem like a good idea

-> Haskell is a “pure” functional programming language.
			* no vars, no setq!  No side-effects! referential transparency!

### Can We Really Write a Program without Side-effects?
Yes.
* Lambda calculus proof says that anything that can be computed can be computed without side-effects

### *ex:* Quicksort:
* Haskell Quicksort is very concise, BUT can be slower/less space efficient
* He’s trying to tell us that it’s fine (doing a pretty good job)

## The Haskell Programming Language
* Haskell doesn’t allow side-effects except things you just need to 
	* Like IO, even then builds a little wall around those parts 
* Statically typed -> will need to declare type at some point

``` A sample Haskell Function (square)
square :: Int -> Int      //type declaration. Arg -> Return
square n = n ^ 2          //function definition
//name parameter = body

mypi :: Float
mypi = 3.14159        //function with no arguments is const


```

* `.hs` for haskell script or `.lhs` suffix. 


——————————

### Download and install the haskell platform (core installer is fine)


## Demo

```day1.hs

square :: Int -> Int
square n = n ^ 2

// in terminal:
$- ghci
$- :load day1
$- square 5
25
$- square (-1)
1
$- :quit
```