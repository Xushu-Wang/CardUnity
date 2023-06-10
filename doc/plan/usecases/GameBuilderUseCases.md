### Generic Use Cases
* User sets new game name as "Rummy 1.1"
* User selects a standard 52 card deck
* User creates a new deck
* User declares one draw and one discard pile
* User enables custom piles on board
* User adds "Run" rules for custom piles
* User defines "Set" rules for custom piles
* User adds a new phase for a turn
* User adds "place 1 card" to allowed actions for a particular phase
* User adds "discard 1 card" to requirements for a particular phase
* User defines first player with "zero cards left" as win condition

### Error Cases
* User does not provide game name
* User continues without selecting a deck
* User does not provide the number of draw/discard piles
* User enables custom piles, but selects no rules
* User selects rules for custom piles, but disable custom piles
* User adds zero phases to a turn
* User exceeds maximum phases for a turn (if implemented)
* User does not specify allowed actions/requirements for a phase
* User does not specify a win condition