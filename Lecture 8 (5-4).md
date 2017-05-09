# Lecture 8 (5/4)
#Ecs140b

### Today
List manipulation in Haskell disguised as lecture about artificial intelligence and search

## Search
You get intelligent behavior by manipulation symbol structures (lists) and manipulating it until you get your structure that relates to the goal you are after

## Puzzles and Artificial Intelligence
puzzles and games thought to be hard (human-level) problems
* if you could solve chess, then we’ve made it!
		* Turns out, understanding language is much harder than these
		* “toy” domains are still useful to get intelligent behavior

**ex:** Tile Puzzle, Peg Puzzle, 
	* The way we solve these are called “state-space” search
		* From start space, there’s a finite set of moves to get to “goal state” (the solution)
		* moves = sequence of operations 
		* State-space search is exactly what Prolog does 


```   Peg Example
R_B          goal: B_R

4 operations: left, left jump, right, right jump.
    /        \ 
_RB         
BR_
B_R
```

-> Since there’s only so many moves you can try from one state, you can conceivably try them all (DFS, finite set of operations)

### Haskell Program to solve it
```
pegpuzzle start goal = reverse (statesearch [start] goal [])

statesearch :: [String] -> String -> [String] -> [String]
statesearch unexplored goal path
  | null unexplored              = []
	| goal == head unexplored      = goal:path
  | (not (null newstates))       = newstates
  | otherwise                    =
			statesearch (tail unexplored) goal path
		where newstates = statesearch(
							(generateNewStates (head unexplored))
							goal
							((head unexplored):path)

//generateNewStates is defined in file on canvas, in case you ever need it 
```

-> Nothing about this is specific to `pegpuzzle`, except that you are storing state as a string
	* To generalize further, you can pass the operators themselves (presumably Haskell supports some kind of function type)
	

-> In more complicated puzzle, we’d have keep track of states you’ve explored already, so you don’t have to do the whole thing again infinitely


## This is just List Manipulation!
-> Some homework assignments coming up after we finish the Clue Program


## Two most important principles of AI
	* Intelligence is search (Newell and Simon)
	* Search is to be avoided (Feigenbaum)
		* expensive computationally
-> Can you make search less expensive??

	* probably. we can use problem-specific knowledge to tell us how to choose the next node or state for exploration
		* can rate nodes as “good” or “near” the goal
		* This is called **heuristics:** Rules derived from problem itself that gets you there faster

## 8-tile puzzle
* If you always choose left, you won’t get the answer very quickly (can be solved in something like 4 moves)
* So then which one to you pick?
	* “Best-First Search” 
	* Num tiles out of place??? (better but still terrible)
	* Better: distance from correct place (manhattan distance)
		* That’s it. It gets you to the right answer right away

