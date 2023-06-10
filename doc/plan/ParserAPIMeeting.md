
# Converting Builder to GameObject
### (Shriya, Del, Ken, Andy) -- 4/10/2023


### GameBuilder obeject needs to be converted to a GameObject

At each level (Game, Round, Turn, Phase)
must convert each `CPUActionBuilder` to a Runner object with appropriate paramters

Del and Shriya wrote two interfaces:



* `ComputerActionInterface`
  * Steps that will automaticall be run by the computer before a stage in the game
  * For example, dealing cards before the game starts
 *  The parser will automatically convert `CPUActionBuilder` to `ComputerActionInterface` objects
  for each objects ``BeforeActions`` and ``AfterActions`` lists
    *  <mark>Paramters??</mark>
    * <mark> Valid Objects? </mark>
        


* `PlayerActionInterface`
  * These are rules that can be executed by a player during a given phase
  * The parser will automatically convert `CPUActionBuilder` to `PlayerActionInterface` objects
  during the **Phase** stage of the game
  * Each ``PhaseBuilder`` object from the builder includes the following paramters which will be 
  assigned to each `PlayerActionInterface` object within the generated `Phase` object
    * <mark>Paramters:</mark>
      * ``AllowedGroups`` Map of groups that can be interacted with during this phase
      * ``minTransfers`` Minimum number of transfers that must be made during this phase
      * ``MaxTransfer`` Maximum number of transfers that can be made during this phase
      * ``Direction`` Direction of transfer
    * <mark> Valid Objects? </mark>

