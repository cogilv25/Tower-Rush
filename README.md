# Getting Started
This project was developed with [node.js v22.12.0](https://nodejs.org/en), however, as of the time of writing it should work on any version newer than this. Once installed copy the game directory anywhere you want, open a terminal, change the current directory to the game directory, and run the command `npm install`. Once that has complete use the command `node main.js` to start the server. From a browser connect to the IP of the PC running the server on port 8000 (This will look something like `192.168.1.100:8000`), create an account, create a lobby, have a friend join you, and play!

# The Game
## Introduction
The game is a very early prototype, but the basic concept is that 2 players must climb a tower where both players have a hunger bar that slowly ticks down, with the game restarting if either player reaches 0 hunger. There are 3 distinct stages to hunger or rather satiation and these affect the stats of the player from speed and jump height, to special abilities, these stages are referred to by the name of the character that represents them for ease of understanding.

## Thin Man
- Medium Jump Height
- Medium Speed
- Specials
	- Faze (Unimplemented) - Allows the character to be unharmed by objects that would normally hurt them for a period of time so long as they stay still.
	- Faze Dash (Implemented) - As before allows the character to "faze" through objects, buty this time for a very short period of time with a quick burst of speed in the direction they are facing.

## Medium Man
- Best Jump Height
- Best Speed
- Specials
	- Hodor (Unimplemented) - Allows the character to be hold a door open for a short period of time to let other characters through.
	- Double Jump (Unimplemented) - Using sheer force of will Medium Man is able to push the very air with enough gusto to propel himself upwards.

## Fat Man
- Worst Jump Height
- Worst Speed
- Specials
	- Float (Implemented) - Allows the character to blow himself up and float upwardsfor a short period of time.
	- Ground Pound (Unimplemented) - Uses his weight to impact the ground, breaking nearby breakable objects.

## Conclusion
As you may be able to tease from these descriptions, the challenge of the game rests in the fact that the players need to consider how they will distribute food between themselves in order to solve the puzzles they encounter. On top of this the game would be fairly fine tuned so that hunger drops rapidly and therefore decisions have to be made in a matter of seconds allowing mental traps to be created as well as points of triumph for the player as they start to see into the mind of the creator and predicte these mental games.

# Technical Details
Generally everything is fairly data-driven, I tried to keep data in seperate json files and further seperate these into what whas need by the client, server or both, combining multiple inputs at runtime where necessary. There are a few examples where I have hard coded things but the majority of things are configurable through the json files. All graphics and sounds are self-made.

## Sever Features
- Multi threaded, Multi Lobby, Multi Game Architecture (Unfinished but you can play multiple simultaneous games).
- Registration and login system using BCrypt to encrypt passwords which are then simply saved as json to a file.
- Somewhat optimized transfer of updates to clients, both x and y axis' are limited to 65535 so they could fit in 16 bit integers, some bit twiddling is done to compress things, for example limiting us to 4092 entities which has not been close an issue so far.. I would have not done this but for the fact my PC can run 16 instances of games serving up to 32 players, and I had hoped to increase this later.
- Automatic reconnection to an ongoing game if a user relogs.

## Game Features
- Hunger System
	- Edible cake (cake is infinite, as in it does not disappear when eaten).
	- Hunger "stages" decide character size and abilities.
- Character Abilities
	- All Characters - Crouch (Ctrl).
	- All Characters - Jump (Space).
	- Fat Man - Float (Hold X while standing still and not too close to anything).
	- Thin Man - Faze Dash (While in the air press X, this will only work if there is a valid "landing spot").
	- All Characters - Look at your companion (Hold Q).
- General
	- The doors and pressure plates use a fairly extendable system, if rough.


## Client Features
- Menus
	- Login / Register.
	- Lobby Selector.
	- Game.

- Assets
	- Some animations were made for the game.
	- Some sound effects were made for the game.
	- The hunger bar is plain html, css, and javascript.

- General
	- The framerate is directly tied to the incoming data rate, it's ok if the data rate keeps up but a simple lerp system was on my (very long) list!