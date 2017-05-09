# Lecture 3 (4/18)
#Ecs140b

* Talk about first project on Thursday
* Today: key implementation issues for logic paradigm
* OH: right after class on Thursdays (3-4:30 or so)

## More Prolog Review
### How does Prolog do what it does?
* The ECS 50 style of how computers deal with languages doesn’t apply here

* Prolog interpreter is sort of non-deterministic (not really)
* show how it work deterministically
* show how unification is done

Recall: the algo we used before
* before we just said “find a match!” 
* but how does it actually work? (more complicated than just string matching)
	* Matching is essential to logic progreamming
	* Matching easy when no variables involved, but with variables it is much more complicated
``` Unification Algorithm
goal: find substitution that makes it true (denoted by /theta)

Input: Two terms T1 and T2 to be unified
Output: /theta, the mgu of T1 and T2, or failure

Algorithm: 
- Initialize the substitutions /theta to be empty
- Initialize the stack to contain the equation T1 = T2

while stack is not empty and no failure, do
	pop X(left)=Y(right) from the stack

	switch: 
		X is a variable that does not occur in Y:
			- substitute Y for X in the stack and in /theta 
  			- add X = Y to /theta

		Y is a variable that does not occur in X: 
			- substitute X for Y i the stack and in /theta 
			- add Y=X to /thea

		X and Y are identical constants or variables:
			- continue

		X is f(X1...Xn) and Y is f(Y1...Yn) for some factor f and n > 0:
			-push Xi and Yi, i=1...n on the stack

	if failure, output failure
	else output /theta 

```


* Theta now holds all substitutions, so go through and do it
* So go through that unification process every time you find a matching

## How is this used in the Prolog Interpreter?
* powerPoint contains this process moving through mini-doku
* it’s a whole thing.

* it makes wrong choices. Does that make it non-deterministic?
	* nah, because it chooses the left-most goal

-> Let’s move on to something a little bit different

# Prolog as Database
* Prolog is sort of like a query language
	* specification of a set of relations given as facts and rules

* How do we update the database? (which is sometimes a bad idea, other times not)

`asset` and `retract`

```
?- assert(<some clause>).
% adds the clause to the corresponding procedure. 
% -adds to end of procedure with that name.
- may vary by implementation (swi-prolog is last)

?- asserta(<some clause>).
% adds clause to beginning of procedure

?- assertz(<some clause>).
% adds clause to end of procedure
```


```
?- retract(<some clause>).
finds first match in database and removes it (top to bottom)
```


### To make this work, you MUST declare predicate as `dynamic`

```
:- dynamic <pred_name>/<arity>, ..., <pred_name><arity>.
% arity is number of arguments

ex (miniDoku): 
:- dynamic validval/1.

```


### Things to Note:
* computationally expensive (assert compiles its clause, retract has to decompile the program to unify its clause before retracting)
* Also just sort of bad style; hard to understand; side-effects :( 

* Sometimes you gotta do what you gotta do (in HW…)


