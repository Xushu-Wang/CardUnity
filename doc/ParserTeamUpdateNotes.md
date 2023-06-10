## Update from the Parser Team (4-4-23):

Where our stuff is:

* Our source code lives in main/java/filemanager
* Our resources live in main/resources/filemanager
* Our test code lives in test/java/filemanagertests

Updates for Builder team:

* You should initialize our parser like `BuilderParser bp = new BuilderJSONParser()` somewhere in
  your code
* To use our code to save a game, use `bp.saveGame(_,_)`
* We need a completed top level class so we can switch out mock placeholders

Updates for Runner team:

* You should initialize our code like `RunnerLoader rl = new RummyLoader()` somewhere in your code
* Don’t use RunnerParser, that’s an internal interface in the parsing process
* To use our code to load a game, use `rl.loadGame(_)`
* We need also need a completed top level class so we can switch out the mock placeholders
* Note that the `loadGame()` method is commented out because we don’t have know which concrete class
  to return yet

# Update from the Parser Team (4-20-23):

Updates for the Builder team:

* New methods were added to the BuilderParser interface to help you set up and validate inputs for
  player actions, computer actions, and conditions.
    * See: `fetchOptions()` and `validateOptions()` in the BuilderParser interface.
* I was nervous about passing around classes (like String.class, Integer.class) across the teams, so
  I've written methods that will validate parameters for you.
    * All you need to do is feed in the specific category, option name, and the value typed into the
      box.
* Another note: I added an internal enumeration (called Category, sorry I couldn't think of a better
  umbrella term) to describe the three different categories of "things" that we have: CONDITION,
  PLAYER_ACTION, and COMPUTER_ACTION.
    * You will have to import this enumeration into the Builder to use these methods - hopefully
      it's not to rough too do that.
* Here's how to use both methods:

When setting up the dropdown box for any category...

```java
    List<String> computerActionList = builderParser.fetchOptions(Category.COMPUTER_ACTION);

    List<String> playerActionList = builderParser.fetchOptions(Category.PLAYER_ACTION);
    
    List<String> conditionList = builderParser.fetchOptions(Category.CONDITION);
    
    // Then you should be able to initialize dropdown boxes with these lists!
```

When trying to validate a parameter...
```java
  // Assuming you can get a collection of name-value pairs, perhaps from a map
  Category currentCategory = Category.CONDITION; // this would be known, I assume you validate each section in batches
  String name = "Create Group" // or something retreived from your map
  String value = "Hand" // or something you retrieved from your map

  try {
    builderParser.validateOption(currentCategory, name, value);
  } catch (RuntimeException runtimeException) {
    // the method will throw exceptions if the option isn't valid - could be a few different messages but the handling is the same here
    displayPopup(runtimeException.getMessage());      
  }
  
  // All together, here is how you might validate a whole category...
 Category currentCategory = Category.CONDITION;
 for(String option : map.keySet()){
   try {
     builderParser.validateOption(currentCategory, option, map.get(option));
   } catch (RuntimeException runtimeException) {
     displayPopup(runtimeException.getMessage());
   }
 }
```
* Let me know if you have any questions!
