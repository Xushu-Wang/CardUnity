## Design Plan
### Names - Del, Shriya, Alec, Ken, Emily, Sophie, Andy, Russel, Ted, Tim
## Team Number 1



### Write your design goals 

The goal of this application is to design a program that can build a card game which can 
have rules that are configurable by a user and can be played by multiple players. 

The rules of the game will be configurable by the user through a ``Builder`` companion program. The user will be able to create
conditions to specify requirements for different `Phases` of each round, turn, and game, such as checking the number of 
cards in a players hand at the end of a turn to see if the player has won.


The user will specify ``Groups`` that appear in a given game (such as a "Hand", "Deck", "Discard" etc.).
In addition, the user will also be able to specify various conditions that must be met for each ``Group``
during each ``Phase``. Such as checking that the board in a game is valid before allowing a player to complete their turn.

* What is encapsulated? 

The encapsulation of the game is the game itself. The game will be able to be played by multiple players and will have a
set of rules that are configurable by the user. The game builder will be completely separate from the game runner itself and will
export a JSON file that will be used to run the game. The game runner will be able to read the JSON file which contains the rules and conditions
of the game and will create a ``GameController`` object to run the game. The ``GameController`` will be able to run the game and will
loop through each of the players turns until the game is over.

Within the  ``GameBuilder`` and ``GameRunner`` there is also encapsulation between their respective front and backends.


* What is flexible? 

This design is very flexible because any number of games can be created and saved as a JSON file. 
Builder and Runner are also completely separate from each other and can be run independently of each other. Allowing 
games to be previously generated and run at a later time.

The user can create a large variety of different games by changing the rules and conditions of the game and which 
Phases are enabled for each round, turn, and game.

### Design's primary architecture
* What is closed

The API is closed to the user. The user will not be able to access the API directly. The user will be able to create a game
by using the ``Builder`` companion program. The user will be able to run a game by using the ``Runner`` companion program.

The Builder will generate a JSON file that will be used by the Runner to run the game. The Runner will be able to read the JSON file.

* What is open

Even though the builder and runner are separate programs, they are both able to communicate with each other. 
This means that the functionality of the builder and runner can be extended in the future by adding new features to the
JSON file. The parser in the game runner will be able to read the new JSON file. It will be important in the development
of this program to keep the list of conditions in the builder up to date with and consistent with the runner.

### Abstractions 
* What abstractions will you create? 

``Groups`` Represents a group of cards. This type will be used to create
subclasses including:

* ``Hand``

* ``Deck``

* ``Discard``

* ``Set``

``Phases`` Represents a phase of the game. This type will be used to store 
conditions for each phase of a turn.

``Conditions`` Represents a condition that must be met for a given phase. 

``Players`` Represents a player in the game. 

``Turns`` Represents a turn in the game. 

``Round`` Represents a round in the game. Will include 
a "BeforeRound" and "AfterRound" condition set and a ``Turn`` object
to specify what each player in the rounds turn will do.

``Game`` Represents the game. Will include a ``Round`` object to specify


``GameController`` Represents the game controller which 
contains information describing all the win conditions for the game, 
instructions for setup, rounds, turns and phases. It will also store 
the Player objects and loop through them to run the game.

``GameBuilder`` Represents the game builder. 

``GameRunner`` Represents the game runner. 

``Parser`` Represents the parser.

### Functionality


* What are some key commonalities within the game genre you chose? 

The final version of the program will be able to build a variety of card games including
Gin, Gin Rummy, Rummy, and Trick taking games such as Hearts, Spades, and Euchre.

Gin/Gin Rummy and Rummy are both games that are played with a deck of cards. The goal of the game is to get rid of all of your cards
by matching them with cards in the discard pile. The game is played in rounds and each round is played in turns. Each turn a player
draws a card from the deck and then discards a card from their hand. The game ends when a player has no cards left in their hand.

Trick taking games are also played with a deck of cards. The goal of the game is to win the most tricks. The game is played in rounds
and each round is played in turns. Each turn a player plays a card and then the next player plays a card. The game ends when all
cards have been played.

* What are some key differences within the game genre you chose?

Trick taking games are structured slightly differently than the Gin variants because the win condition 
is on a per-round basis (the "Trick") rather than a condition checked at the end of each player's turn.

However, by allowing the ``GameBuilder`` to specify which ``Phases`` are enabled for each round, turn, and game, the program will be able to
check at the end of a turn for the Gin variants and at the end of a round for the trick taking games.


### API
* For each API you plan to build, provide a rough paragraph high-level design overview. 

#### Builder

The Builder will be able to create a JSON file that will be used by the Runner to run the game. The Builder will be able to create
a ``GameController`` object that will be able to run the game. The ``GameController`` will be able to run the game and will
loop through each of the players turns until the game is over. 

The ``GameBuilderUI`` will use an API to interface with the ``GameModel`` which 
will store the information describing all the win conditions and phases for the game in a ``GameModel`` object. The ``GameBuilderUI`` will also use an API to interface with the ``GameView`` which will display the information describing all the win conditions and phases for the game in a ``GameModel`` object.

The ``GameBuilderParser`` will then read this ``GameModel`` object and 
convert it into a JSON file which can be saved and exported.



#### Runner

The Runner will be able to read a JSON file that was created by the Builder. The Runner will be able to create a ``GameController`` object
that will be able to run the game. The ``GameParser`` will create a ``GameController`` object that will be able to run the game.

The ``GameController`` will be able to loop through each of the players turns until the game is over.
The ``GameController`` will use an API to interface with the ``GameModel`` and a separate
API to interface with the ``GameView``

* Include a picture of how the modules are related (these pictures can be hand drawn and scanned, saved from an online CRC card tool, written in Markdown, created with a standard drawing program, or screenshots from a UML design program).

![3081CB4B-D1DA-494F-8AB6-1AC7FC4EF160_1_105_c.jpeg](..%2Fdata%2F3081CB4B-D1DA-494F-8AB6-1AC7FC4EF160_1_105_c.jpeg)