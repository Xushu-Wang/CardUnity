# Gin Rummy Game


## GameStage

### BeforeActions
*List any `ComputerAction` Object present in this list and its paramters*

* `CreateGroup`
  * Parameters: "group_tag":"deck"
* `PlaceDeck`
  * Parameters: "group_tag":"deck"
* `CreatePlayer`
  * Parameters: "name":"del"
* `CreatePlayer`
  * Parameters: "name":"shriya"
* `CreatePlayer`
  * Parameters: "name":"ken"
* `CreateGroup`
  * Parameters: "group_tag":"Discard"
* `Transfer`
  * Parameters:
    * "source_tag":"Deck"
    * "destination_tag":"Hand"
    * "amount":"7"
* `Transfer`
  * Parameters:
    * "source_tag":"Deck"
    * "destination_tag":"Discard"
    * "amount":"1"


### AfterActions
*List any `ComputerAction` Object present in this list and its paramters*
* None
### Rounds

**Gin Rummy has one `RoundStage` object**


## RoundStage

### BeforeActions
*List any `ComputerAction` objects present in this list and its paramters*

* None


### AfterActions
*List any `ComputerAction` objects present in this list and its paramters*

* None

###Turn
**Gin Rummy has one Turn Object**

## TurnStage


### BeforeActions
*List any `ComputerAction` objects present in this list and its paramters*

* None
### AfterActions
*List any `ComputerAction` objects present in this list and its paramters*

* `CheckWin`
    * Parameters: none


### Phases
*List any `Phase` objects present in this list and its paramters*

* Draw
* Play
* Burn


## Phases

### Draw

* beforeActions
    * None
* afterActions
    * None
* playerActions
    * `FromHandTransfer`
        * Parameters: "group_tag":"discard""
    * `FromHandTransfer`
        * Parameters: "group_tag":"deck"
* condition
    * `TransferAmountCondition`
        * Parameters: "count":"1"

### Play

* beforeActions
    * None
* afterActions
    * None
* playerActions
    * `CreateGroup`
        * Parameters:
            * "group_tag":"set"
    * `FromHandTransfer`
        * Parameters:
            * "group_tag": "set"
* condition
    * `RunOrMeldCondition`
        * Parameters:
            * "group_tag":"set"


### Burn


* beforeActions
    * None
* afterActions
    * None
* playerActions
    * `FromHandTransfer`
        * Parameters: "group_tag":"discard""
* condition
    * `TransferAmountCondition`
        * Parameters: "count":"1"






