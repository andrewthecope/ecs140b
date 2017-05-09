# Lecture 9 (5/9)
#Ecs140b

## Questions about Midterm:
### Format:
Only Haskell and Prolog. In class material is fair game
* Haskell readings “should be conversant”
* Should we know how prolog works? “Absolutely”

* Will take up the entire period
* Will it feature material from homework assignment? “Absolutely”

* Haskell functions will be similar complexity as assignment. Nothing bigger than 5-6 lines

### “Let’s see… what would I put on the exam”
 (haven’t written the exam yet)
* Why functional programming (what’s the point, what’s not the point)
* Prolog (building upon 140a knowledge). How it actually works. 
* Know Prolog interpreter algorithm (“real conversant”)
* Here’s a little prolog program, here’s the interpreter. Trace the behavior.
* Non-deterministic programming, why it doesn’t work in the real world.
	* what does this do if N.det. What does this do if Det.
* Questions involving minidoku program
* Understand how unification works
* Might be a reference to Clue project 
* Know about State and Side-effects (why are they disdained from the functional programming point of view)
* Referential transparency (don’t typically ask history questions)
* Program efficiency versus Programmer productivity
	* Talk intelligently about that for a few seconds
* In either language, I would expect 7 or 8 line functions in either language that does some simple list processing
* How recursion works in terms of activation frames and call stack
* Tail recursion, I expect you to know about that.
* Type declarations in Haskell. Write one.
* Polymorphic datatypes in Haskell. Write one.
* Type inferencing
	 What about this? That it can do it? 
* Material From homework due tomorrow
* Peg Puzzle program. At least understand what’s going one. Maybe identify if something is wrong with it
* **won’t ask about**: Heuristics and stuff 


## Some More Handy Haskell Things
You can use `..` syntax to do simple shorthand expressions
```
Prelude> [1, 2 .. 10]
[1,2,3,4,5,6,7,8,9,10]

Prelude> ['a','b' .. 'j']
"abcdefghij"

Prelude> [0,5 .. 50]
[0,5,10,15 //ect
```

Here’s something else:
```
[sqrt n | n <- [1,3 .. 11]]

// create a list of values (take sqrt of n given that n is this list)

[sqrt n | n <- mylist] where mylist = [1,2..10]

//slightly more legible version of the same thing
```


## Lazy Evaluation
First a demonstration
```
multiply a b = a * b

>> :load may9
>> :type multiply
>> multiply 2 3
>> (multiply 2) 3   % This works because of partial eval.
 
% so this works too...
n 3 where n = multiply 2

%this too!
map (multiply 2) [1,2,3,4,5]
```


In **Lazy Evaluation**, haskell will evaluate one parameter at a time

* There’s some cool advantages to this:
	* y = [1,2..] evaluates, but doesn’t store actual values until used.