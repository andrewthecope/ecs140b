# Lecture 2 (4/11) 
#Ecs140b

### Functional And Logic Programming
* about time we started programming

### Assignment #1
* Sudoku
	* Prolog is the ideal programming language for solving sudoku puzzle
	* logic / constraints / ect
	* posted on Canvas tonight 
	* due 6pm April 21st (friday) 
	* -> easier than first seems 
* Given:
	* test data (in list of list - rows), empty spaces given by _
	* can do it in a few seconds
	* might not have a solution, figure that out

	* more challenge tests are given, solve efficiently for extra credit

	* print function given, well at least I think it’s given
	
* Crude Solution :
``` in swi-prolog

sudokusolver.pl // 25 clauses

test0 :- L = [ect]
	sudoku(L),
	printSudoku(L)

?- test0. // and it prints
?- test0a. // very quickly
?- test0b. //more variables, slower
?- test0c. //flawed, can't be solved. 
false.

?- test1. //more variables, will be *much* slower

```


### How much more challenging are tests1, 2, and 3? 
much more.

-> Constraint Logic Programming
		* not allowed because it’s too easy
		* can be used for inspiration
		
## Non-Determininstic Programming
* generate and test approach to problem solving
```
find(X) :- generate(X), test(X).
```

```
sudoku(L) :- generate_sudoku_solution(L), test_solution(L).
```

-> computationally expensive. Depth First search with back track takes too long (fill with all ones, then every combination of solutions)
	* 9^52 solutions to test
		-> 7.35 * 10^31st years in worst case scenario

### How can we reduce this time?
1. “ push testing into the generator”
			* test one row is valid before testing any other row
			* only put a 1 in if you haven’t used it before
			* adding constraints for rows, columns, and group will make it manageable
  		
2. Create a small version of the problem -> scale up
	* solve smaller problem first, easier!

#### “MiniDoku”
	* List of three elements
	* [3, Y, 1] solves to 2 really quickly
	* unify the input so everything has unique names ~
```
?- [1,_,3] = [X1,X2,X3]. //equals is unification operator
X1 = 1,
X3 = 3. 	
```

```
sudoku(L) :- [X1,X2,X3] = L,
             worthy([X1,X2,X2]). 

//worthy means 1) they must be valid, 2) they must all be different

worthy(L) :- valid(L, diff(L).
valid([H]) :- validval(H).
valid([H|T]) :- validval(H), valid(T).

validval(1).
validval(2).
validval(3). //for big problem will be 1-9

//what does diff mean?

diff([H]).
diff([H|T]) :- not(member(Ht,T)), diff(T).

member(H, [H|T]).
member(X,[H|T]) :- member(X,T).
```

## Does it work? (spoiler: yes)
``` swi
?- sudoku([3,Y,1]).
Y = 2.

?- sudoku([3,_,1]).
true.

?- sudoku([X,1,Y].
X = 2,
Y = 3
X = 3,
Y = 2
false.

//can also solve X,Y,Z (will just give all possible solutions
```

* how do I unify something like this:
```
[[1,_,2],
 [2,_,1],
 [1,2,3]] = [[X1,X2,X3],[X4, ...ect 
```







