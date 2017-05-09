# Lecture 7 (5/2)
#Ecs140b

* talk about Haskell style
* tail recursion (if time)


So far we’ve been writing programs with | guards 
	* also `if... then...else` construct if you want
	* another approach…. pattern matching

# Pattern Matching in Haskell
* when you call a function, Haskell looks for matching function
```
nonzero n
  | n == 0  = False
  | otherwise = True

//can be written more prolog-y
nonzero 0 = False
nonzero _ = True
 
```

## Patterns Can be
* a literal value: ‘x’, 24, True
* a variable: x, foo
* a wildcard: _ 
* a tuple pattern: (p1,p2,pn) 
* **lists:**
	->  (<headoflist>:<tailoflist>) 
		* matching is like prolog

* a constructor patthern over lists will either be [] or will have the form (p:ps)
* this is used all the time

``` Examples in built-in Haskell Functions
head :: [a] -> a
head (x:_) = x

tail :: [a] -> [a]
tail (_:xs) = xs

null :: [a] -> Bool
null [] = True
null (_:_) = False
```


## More Examples
``` length
mylength inlist
	| null inlist    = 0
	| otherwise      = 1 + mylenth (tail inlist)
//Can be converted into...

mylength [] = 0
mylength (_:xs) = 1 + mylength xs
```


```  sum of list
mysum inlist 
	| null inlist   = 0
  | otherwise     = (head inlist) + mysum (tail inlist)
//Can be converted into

mysum [] = 0
mysum (x:xs) = x + mysum xs
```

``` member (called elem in Haskell)
myelem  item inlist
	| null inlist = False
	| item == head inlist = True
	| otherwise           = myelem item (tail inlist)
//can be converted into...

myelem item [] = False
myelem item (y:ys)
	| item == y  = True
	| otherwise = myelem item ys
myelem item (_:ys) = myelem y ys
```

## Note: Can’t use same pattern matching variable twice:
```
Cant do:
myelem y (y:ys) = True
//because matching y with two different values, 
// not like prolog!

-> So that's why we say:
myelem item (y:ys)
	| item == y  = True
	| otherwise = myelem item ys
```



# Tail Recursion
```stack for recursive factorial function (in java/C++)
?- fact 3
------------
fact 0
1 + fact 0
2 * fact 1
3 * fact 2
-------------
//activiation frame used for every call. fact 100000000 will take up a lot of frames
- common complaint about recursive approaches to things
```

-> this is not what Haskell does: 

* Most languages employ **strict evaluation**. Something on stack is evaluated right away (or another stack)
* Haskel doesn’t evaluate until it needs to. If it doesn’t evaluate, it is called a **thunk**. 
		* Thunks can be nested, last in first out behavior.
		* but not on the call stack
-> **Lazy Evaluation**

-> We want 0(1) space for these functions, but don’t want iteration
Note that recursion can be expressed like this:
```
n * (n -1) * (n -2) ... 1
```

So if you have a running total (maybe a variable called `product`) you wouldn’t have to stack things up.

### This is called *Tail Recursion*:

``` keep track of running product in helper function (initialize to 1)
fact_tr n = fact_tr_helper n 1

fact_tr_helper n product 
	| n == 0      = product
	| otherwise   = fact_tr_helper (n - 1) (product * n)

```

### Result on Stack
```
fact_tr 4
fact_tr_helper 4 1 
fact_tr_helper 3 4
fact_tr_helper 2 12
fact_tr_helper 1 24
face_tr_helper 0 24
24

//not defined with itself (not growing in increasingly longer clauses). Not postponing any computation, so no O(n) stack size.
```

### Why are no computations postponed?
*  if you have `n * fact  (n -1)` you can’t do operation until you evaluate fully
* compare with `fact_tr_helper (n - 1) (product * n)`, you can evaluate at every step 
		* ~~~~~ I need to think about this more….
* 




