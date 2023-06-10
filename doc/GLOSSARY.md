
# Important Files

*[GinRummyCommands.md](GinRummyCommands.md)
contains a complete list of all the commands that can be used in the Gin Rummy game.*


*[ParserClasses.properties](..%2Fsrc%2Fmain%2Fresources%2FFileManager%2FParserClasses.properties)
contains a list of all the classes that can be parsed by the ``Parser``. All names on the left side of the file are the corresponding ``ActionRecord`` objects in the builder and the right side
contains the ``Action`` classes implemented in the Runner.*


* Complete Gin Rummy Game that can be parsed and executed by Runner [GinRummyTest.json](..%2Fdata%2Fjson%2FGinRummyTest.json)

# Important Terms


## Group

A group is a collection of cards. The group can be a ``hand``, ``deck``, ``discard``, or ``set``
(or other user specified groups using the Builder)

``Hand`` - A group of cards that a player can see and interact with.

``Deck`` - A group of cards that a player cannot see and cannot interact with except for the top card.
It will be used to draw from or deal.

``Discard`` - A group of cards that a player cannot see and cannot interact with except for the top card.
It will be used to store cards that have been thrown away by the player.

``Set`` - A valid group of cards that a player can interact with. For example, in Gin Rummy, a set is a valid ``meld`` or ``run``.
The critiera for a valid set are specified by the game rules in the Builder and vary from game to game.

* In Gin Rummy, there are two types of valid sets: melds and runs.
  * A ``meld`` is a set of three or four cards of the same rank (number) but different suits.
  * A ``run`` is a set of three or more cards of the same suit. The ranks (numbers) must be in a sequence.


In Gin Rummy and Rummy for example, the player's hand is a ``hand`` group, the deck is a ``deck`` group, and the discard is a ``discard`` group.

## Phase

A phase is a part of a Players turn. A turn is made up of multiple phases. For example, in Gin Rummy, a turn is made up of the following phases:

* Draw - The player draws a card from the deck or the discard pile.
* Play - The player plays a valid `meld` or `run` from their hand if possible, or ``hits`` onto an existing set.
  * ``Hit`` - The player adds a card to an existing set.
* Burn - The player burns a card from their hand to the discard pile.
* Check - The player checks to see if they have won the game.

The player can only move on to the next phase if the current phase is complete. For example, the player cannot discard a card until they have played a valid set or hit onto an existing set.

## Condition

A condition is a rule that must be met for a phase to be complete. For example, in Gin Rummy, the ``Draw`` phase is complete when the player has drawn a card from the deck or the discard pile.

## Game


A game is a collection of rounds.
A round is a collection of turns.
A turn is a collection of phases.
A phase is a collection of conditions.

The game also contains players and a game controller which keeps track of the order of turns,
the current phase in the turn, and can check if the round win condition or game win condition has been met.


## Game Stages

Each of the parts of the game are represented in the Rules Builder as a ``Stage``. All Stages implement the ``Stage`` Interface and inherit the ``AbstractStage`` class.
The stages are:

Each stage contains
* ``BeforeActions`` which is a ``ComputerActionList`` that contains the actions that the computer will take before the player takes their turn.
* ``AfterActions`` which is a ``ComputerActionList`` that contains the actions that the computer will take after the player takes their turn.



* ``GameStage`` - The game stage is the top level stage. It contains the game rules, the players, and the game controller.
* ``RoundStage`` - The round stage contains the round rules, the players, and the game controller.
* ``TurnStage`` - The turn stage contains the turn rules, the players, and the game controller.
* ``PhaseStage`` - The phase stage contains the phase rules, the players, and the game controller.
  * Phases also contain ``PlayerActions`` which are the actions that the player can take during the phase.
  * Phases contain ``Conditions`` which are the rules that must be met for the phase to be complete.



* ``GameStage`` - The game stage is the top level stage. It contains the game rules, the players, and the game controller.
* ``RoundStage`` - The round stage contains the round rules, the players, and the game controller.
* ``TurnStage`` - The turn stage contains the turn rules, the players, and the game controller.
* ``PhaseStage`` - The phase stage contains the phase rules, the players, and the game controller.
  * Phases also contain ``PlayerActions`` which are the actions that the player can take during the phase.
  * Phases contain ``Conditions`` which are the rules that must be met for the phase to be complete.

