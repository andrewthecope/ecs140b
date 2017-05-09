# Lecture 6 (4/27)
#Ecs140b

## Haskell
* In some ways like Lisp, other ways nah

## Data Types
#### Boolean
true and false
&& and ||

#### Integer
`Int`
 (there’s also Integer for larger numbers)

#### Arithmetic
+
-
*
/
^ power
`div` whole number division
`mod` remainder  (these are prefixes like functions??)

#### Relational Operators
 >=
 >
 ==
 /= (not equals)
 <=
 <

#### Function names and variables
begin with lower case letters

#### Data Types
begin with uppercase letters

#### Comments
```
-- this is a comment

Theres also the literate style which has everything comments except things after > (for .lhs file), bur we don't do it
```


#### Guards (conditionals)
```
max3 x y z
	|  x >= y && x >= z  = x
	|  x >= z            = y
  |  otherwise         = z

-- otherwise not required, but do it anyway
```


#### Layout
* series of function definitions
* based on indentation
* put type declarations above function call (although you don’t need to)


#### Iteration
* No loops, just recursion
```
sumints :: Int -> Int
sumints n
	| n == 0     = 0
  | otherwise  = n + sumints (n - 1) 
```

```
factorial :: Int -> Int
factorial 
	| n == 0    = 1
  | otherwise = n * factorial (n - 1)
```


#### List
`[]` is an empty list
`[1, 2, 3]` is a list of three values
`['a','b','c']` is equivalent to “abc”
list of floats is also fine

**not allowed:** 
`[1,'b',3.0]` can’t mix up types

List = empty list or something cons’ed onto a list
->  the best way to process is through recursion

#### Cons
`1:[]`  
[1]

`'a':"bcd"` 
[abcd]

`1:2`   
ERROR: an only cons onto a list (this is allowed in lisp, but not Haskell

#### List functions
`head [1,2,3,4]` 
1

`tail [1,2,3,4` 
 [2,3,4]

`elem 2 [1,2,3]`
True

`length "avcde"`
5

`"ab" ++ "cde"` like append
“abcde”

`reverse "abcde"`
“edcba”

`zip "abc" [1,2,3]`
[(‘a’,1), (‘b’, 2), (‘c’, 3)]
creates list of tuples
tuple allows for different data types

#### Tuple Functions
`fst ('a',1)`
‘a’
`snd (‘a’,1)`
1

## Type Declaration for Lists
`mylen :: [Int] -> Int` Like Swift

### For Strings:
`mylen :: [Char] -> Int`
`mylen :: String -> Int`

### Is there a way to generalize?
* something like “list of atoms” or whatever
* more of a polymorphic type declaration

`mylen :: [a] -> Int` just put a (lowercase) variable in
	* anything that can be variable a will do. 

## A Note about General Types
* Sometimes if you have a general atom, you can’t assume that it has a notion of equality == 
* solve with qualifier
```
myelem :: (Eq a) => a ->[a] -> Bool
//note the => qualifier on a 
// not a new parameter, but describes a
// means a type can be tested for equality
// these are called "contexts" (which probably doesn't matter) 
```


## Type Inferencing
* But wait, if it can recommend the type, how smart is this thing?
* You can actually omit type declaration!!
* 



