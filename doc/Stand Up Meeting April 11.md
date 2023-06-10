## Stand Up Meeting: 

### Tuesday April 11, 2023

## Builder Team:

* Tim:

Adding in ability to create phases. Extensible to allow more moves/group checks easily. (ADd on to array). 
* UI to allow users to add to list of phases within each round
* Changed Structure of overall UI. ``Navigator`` class to act as controller to move between panes. 
* When the user clicks submit ``Navigator`` fetches data from all screens and saves into record class

Emily:

* Created MockUI record classes (to be modified by parser
* Used by Parser
* Parser team can update these and the UI will be changed to corresponde
* Added "submit" button which creates the `GameBuilderRecord` object



## Parser Team:

* Need to update ``MockUI`` object to correspond to new Record classes
* Try to change Record file into `GameObject`




## Runner Team:



Shriya:

* Seperated `ComputerActions` from `PlayerActions`
* Wrote tests for Conditions (for end of Phases)

Andy: 

* Merged branch to master
* Wrote examples for how the Runner backend will interact with the runner frontend
	* In ``ObserverPattern`` file	

	
Sophie: 

* Working on Aesthetics of UI 
* Next Steps: Will work on integration with backend

Ted: 

 * Creating chatGPT API to give user tips in game
 * Thinking about condition checking for phases in game runner backend


Next Steps: 

Coordinate with Builder UI 