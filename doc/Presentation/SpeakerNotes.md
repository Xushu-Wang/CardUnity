* Overview: Runner
    * GameStage: contains all information relating to what occurs at what point. call step() method
      to move to next phase of game. Created using JSON file that is output from the builder.
    * Game Loop: iterates through the game -> round -> turn -> phase. Draw, play, and burn are
      examples of phases. Each phase is a separate part of a player's turn.
    * Board: contains data for all card piles/players. Maintains the current state of the game.
      All computer and player actions modify the board in someway
      (ie: through a transfer/creating a new card pile)
    * Player: contains hand
    * Frontend: allows current player to view cards and make actions that are defined in the phase.
      able to select different piles on the screen (ie: deck, discard). Triggers observers that
      relay actions to the backend and vice versa.

* Alternatives:
    * Current design: each phase allow users to move any card to any allowed card group
      and moves are validated only when user presses "next phase" button.
    * Alternative: validating each move synchronously as the player performs it.
    * Decision: we implemented asynchronous move validation because we felt it allowed our design to
      be more extendable
      and simpler to implement.