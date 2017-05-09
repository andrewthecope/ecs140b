# Lecture 4 (4/20)
#Ecs140b

## Another One. Project 2. 
# Clue
Try to figure out 1) who murderer is, 2) what room, 3) weapon
* Build board game assistant

### Minimum Requirements:
	* initialize the game setup easily
	* which rooms and weapons are used in this version of the game?
	* how many players?
	* the order of play (whose turn next?)
	* which cards am I holding?
	* and so on…

	* Keep track of questions asked already
	* keep track of answers to those questions

	* know when to make an accusation

* should have documentation
* shouldn’t have to use prolog at all (menu driven, or something, not prolog)

-> About a C or B

### The Next Level:
* take advantage of what can be inferred from the suggestions of other plays
* if a player x gave card to player y, then you know where card is
* Suggest which question to ask next (presumably to get accusation faster)

-> B to an A

### The A+ Level:
* build models of what the others players might know and use the models to asses how close they might be to winning
* advise me to make a suggestion that might throw other players off
* other stuff


Partner project
* tell Prof on canvas AJ is my partner on Monday, April 24th

## Due: Friday, May 5 at 6pm

#### How to deal with spaces:
* maybe keep track of proximity (because need to be in the room to ask)
* don’t hardcode exact locations
* You can also subvert people by asking them (they move to the accusation spot)



