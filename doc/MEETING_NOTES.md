### 3/23 Meeting

- discussed the different types of trick taking games and the differences between some more complex games like rummy, gin rummy, and gin
- found a general structure that works to generate both trick taking games and more some more complex strategy games
    - pick up
    - organize
    - put down card
    - evaluate??



### 3/26 Meeting

#### Parts of the Project:

* Builder View    - glorified scratch editor with places for input (dropdowns, etc.)
* Building Model  - stores data from view, puts logic to it to interpret it
* Game Parser     - creates (many) data files that will describe this customized game
* Controller      - takes the data files, interprets them, and creates a Game Runner
* Game Runner     - runs the games based on given logic from file
* Game View       - visualizes the game from the Game Runner

#### Notes:
* Created game flow
  * Chose to make a complex card game with the base game of Rummy
* Have initial code flow with strategies 
* Defined major parts of the project
  * Wrote API for each major part



### 3/28 Meeting

#### Parts of the Game:
* Start with 7 cards per person
* Possible multiple decks of cards (repeat cards)
* Special cards:
  * Wild card
  * Joker cards
* Pick up:
  * Pick up from the deck
  * Pick up from the discard pile
  * Question/concern: what if we run out of cards to pick up?
    * Shuffle feature?
* Organize:
  * trying to make a group
    * either pick up a new deck or the discard pile
  * when you find a set, you can play it out
  * when you can add (any number of cards) to an existing set
* Lay down:
  * put one card into the discard pile 
* GOAL OF GAME: get rid of all your cards
  * last card must be discarded, not played (enforcement of stages)
* Error messages:
  * customized error messages for user to create, and will pop up when rules are violated

#### Personalization of the game set up:
* Number of players
* Number of cards per player
* What is considered a set (set maker?)
* Win conditions

#### Notes:
* Discussed what type of game we should 
  * Fluxx possibility
    * Able to have rules coded with the cards so that the rules can be read from the card
    * Issue, what is considered a variation?
      * variations are too hard
  * Card game possibility
    * Original
    * too complicated... to many generalizations
    * Narrow version
      * Start with one specific game
      * make it modular (user is SUPER restricted on what they can customize)
      * make blocks that take in parameters
  * Choice of Gin
    * Played Gin
    * Discussion of API

#### Positions/Roles Initial Thoughts (totally not conforming):
* Tim - good with UI, wants to help with either the builder UI or the Game Runner UI
* Ted - wants to work on UI
* Sophie - general front end / UI or controller
* 

#### Class Notes:
* pom.xml files
* different data structures
* demoed the example parser
* 