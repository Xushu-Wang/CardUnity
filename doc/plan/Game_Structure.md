# Proposed Game Structure

* Some thoughts after 3/28 meeting...changes are absolutely welcome!
* Open issues:
    * Not sure how to specify allowed actions/requirements in the Setup Wizard, how to encode them
      into a config file, and how to read them out and initialize them
    * No clean way to move cards around - should get fixed when MVC loop is implemented for the
      overall game (probably a Command pattern)

## Java Classes

```java
/*
 * This is just the general information for the Game Runner side,
 * in the future the info will be divided into MVC loops, etc.
 *
 * This info should (in theory) describe all the necessary information for a game to run on its own
 * Hopefully, the setup features (like dealing initial cards) can happen during construction without
 * a specific dedicated structure in the Game
 */

public class Game {

  // Describes the phases associated with one player turn, may need another "Round" abstraction
  Turn gameTurn;

  // Describes the content on the board, as well as if rules for board "validity"
  Board gameBoard;

  // All active players in a game - open to be real or bots
  // The number of players is set up in realtime with a dialog - not in config files
  List<Player> currentPlayers;

  // Run one turn for all players
  public void runRound();
}
```

```java
public class Turn {

  // Describes sequence of phases for one turn
  List<Phase> turnPhases;

  // Run a turn for one player
  public void runTurn(Player player);

  public void advancePhase();
}
```

```java
public class Phase {

  // This part is still iffy, not sure how to specify these things yet
  List<GameAction> allowedActions;
  List<GameAction> requiredActions;

  // checks if a player is able to move on from a particular phase
  public boolean canContinue();
}
```

```java
public class Board {

  // Probably wrapping a deque object, with some functions disabled
  // For example, prohibit placing cards onto a DrawDeck
  DrawDeck drawDeck; // extends BoardDeck
  DiscardDeck discardDeck; // extends BoardDeck
  List<BoardDeck> placedGroups; // current sets/runs on table

  // checks if the overall board state is valid (all in sets/runs?)
  // The implementation of this method might be passed in as a lambda
  public boolean checkValid();

  // add a card to the board
  public void addCardToBoard(Card c, BoardDeck target);

  // remove the top card from a pile on the board (drawing) 
  public Card removeCardFromBoard(BoardDeck target);
}
```

```java
public class BoardDeck {

  Deque<Card> deckContents;

  // These functions can be overwritten in subclasses as necessary
  public void addToEnd(Card c);

  public void addToBeginning(Card c);

  public Card removeFromBeginning();

  public Card removeFromEnd();

  // shuffle the deck
  public void shuffle();

  // checks if self is valid
  public void checkValid();
}
```

```java
public class Player {

  String name;
  List<Card> currentHand;
  int score;

  // Note: There should be some central structure that moves cards around instead of individual methods
  public void addToHand(Card c);

  public Card removeFromHand(Card c);
}
```

## Possible Builder UI

* Builder UI looks like a setup wizard
* Setup occurs across multiple stages that the user navigates through
* Ideally, the setup wizard mirrors the structure of the actual runnable Game class (whatever that
  ends up being)
* When a user initiates the process of building a new game, we ask (in order):
    * Metadata
        * Name of the game
        * Max/min number of players
        * Color style? Idk
    * Deck definition
        * Select a deck - determines subsequent behaviors
        * Standard 52 card setup
        * Standard + 2 jokers
        * Custom deck (within reasonable limits)
    * Board definition
        * Overall, what makes a board "valid"
        * Rules for groups of cards of the table (sets, runs, etc.)
        * Maximum/minimum number of piles on the table
        * Presence of special decks (draw/discard/burn piles, etc.)
    * Turn definition
        * How a player "plays" one turn
        * Add an arbitrary number of action/checking phases
        * Each phase has:
            * A name
            * Allowed/banned actions
            * Requirements before moving on
        * (Game will run through this sequence every turn)
    * Win definition
        * How a player wins a game
        * Selects from a variety of possible conditions