## Building a game

### External API

```java
/**
 * The BuilderParser interface is meant to represent a general parser that can write a built game to
 * a file. The file format is abstract, and implemented by concrete classes.
 *
 * @author alecliu
 */
public interface BuilderFileManager {

  /**
   * Primary entry point from the Builder to write a user-made game to a file.
   *
   * @param gameRecord configured game object representation
   * @throws RuntimeException if a game is misconfigured
   */
  void saveGame(GameRecord gameRecord) throws RuntimeException;


  /**
   * Update the language of messages returned by the parser.
   *
   * @param language desired language
   */
  void setLanguage(String language); // -> added post-planning phase

  /**
   * Fetch all available options for a category
   *
   * @param categoryType category type
   * @return list of available options
   */
  List<String> fetchOptions(Category categoryType);  // -> added post-planning phase

  /**
   * Fetches a list of all required parameters for a particular option
   *
   * @param categoryType category type
   * @param optionName   list of required parameters
   * @return list of all required parameter names
   * @throws NonexistentOptionException if the provided option does not exist in the category
   */
  List<String> fetchParametersForOption(Category categoryType, String optionName)
      throws NonexistentOptionException; // -> added post-planning phase

  /**
   * Validates if a given option was provided with the correct input type
   *
   * @param optionName option name
   * @param parameters map of values to parameters
   * @throws RuntimeException if the given information is invalid
   */
  void validateOption(Category categoryType, String optionName, Map<String, String> parameters)
      throws RuntimeException; // -> added post-planning phase

}
```

### Internal API

```java
/**
 * The Translator interface is a wrapper class around the message-related resources. It will fetch
 * the correct translation for messages using a common resource key. Additionally, it will manage
 * general translations between the resource files and the view.
 *
 * @author alecliu
 */
public interface Translator { // -> added post-planning stage

  /**
   * Fetches a translated message based on the resource key
   *
   * @param key resource key
   * @return translated message
   */
  String translateToUserSpace(String key);

  /**
   * Translates an outgoing list from the resource representation to the user-friendly
   * representation
   *
   * @param resourceList resource-based list
   * @return user-friendly list
   */
  List<String> translateToUserSpace(List<String> resourceList);

  /**
   * Translates an incoming string from user space to the resource representation
   *
   * @param value given value
   * @return corresponding resource representation
   * @throws NonexistentTranslationException if there is no suitable translation for the message
   */
  String translateFromUserSpace(String value) throws NonexistentTranslationException;

  /**
   * Translates an incoming map of parameters from user representations to resource
   * representations.
   *
   * @param parameters user-based representations of parameters
   * @return a map with the keys translated to their resource representations
   * @throws NonexistentTranslationException if there is no suitable translation for certain keys
   */
  Map<String, String> translateFromUserSpace(Map<String, String> parameters)
      throws NonexistentTranslationException;

  /**
   * Translate all actions and conditions in an incoming game from user-friendly representations
   * into resource representations.
   *
   * @param gameRecord game-record to be saved
   * @return resource-based GameRecord
   */
  GameRecord translateGameFromUserSpace(GameRecord gameRecord);

  /**
   * Configures the resource bundle to output the correct language
   *
   * @param language desired language (i. e. English)
   */
  void setLanguage(String language);

}
```

```java
/**
 * The LanguageLoader interface is responsible for fetching language resource bundles. This
 * interface can accept semantic language names like "English", then fetch the correct language
 * resource to use during translation.
 *
 * @author alecliu
 */
public interface LanguageLoader { // added post-planning

  /**
   * Convert a language into a language code. For example, "English(UnitedStates)" to "en-us".
   * Throws an exception if the language is not supported.
   *
   * @param language desired language
   * @return resource bundle associated with the language
   * @throws RuntimeException unsupported languages
   */
  ResourceBundle getLanguageResource(String language) throws RuntimeException;

}
```

## Loading a game

### External API

```java
/**
 * The RunnerLoader interface is responsible for fetching and loading games for the Game Runner
 * program. The RunnerLoader cooperates with the RunnerParser class initially to load in a Parser
 * representation from a file, then configure a ready-to-run game object.
 *
 * @author alecliu
 */
public interface RunnerLoader {


  /**
   * Load a game from a file.
   * Return a Game object that is ready to run.
   *    Includes Stages:
   *    * Game
   *    * Round(s)
   *    * Turn(s)
   *    * Phase(s)
   *        * Action(s)
   * If the file is not found, or the file is not a valid game file, throw a RuntimeException.
   * @param filename file name
   * @return configure game object
   * @throws RuntimeException if file is not a valid game file
   */
  Game loadGame(String filename) throws RuntimeException;

  /**
   * Load a game from a file, injecting information about the players and the number of copies of
   * the deck to be included. This allows for games to be loaded more flexibly for different party
   * sizes.
   *
   * @param filename file name of the game
   * @param players list of players to include
   * @param deckCopies number of copies of the deck to include
   * @return configured game object
   * @throws RuntimeException if the game file is not valid
   */
  Game loadGame(String filename, List<Player> players, int deckCopies)
      throws RuntimeException; // -> added post-planning phase

  /**
   * Update the language of messages returned by the parser.
   *
   * @param language desired language
   */
  void setLanguage(String language); // -> added post-planning phase
}

```

### Internal API

```java
/**
 * The RunnerParser interface is meant to represent a general parser that can read a built game from
 * a file. The file format is abstract, and implemented by concrete classes.
 *
 * @author alecliu
 */
public interface RunnerParser {

  /**
   * Load a Parser representation of an existing game from a file
   *
   * @param filepath provided file path
   * @return configured game
   */
  GameRecord loadGameFromJson(String filepath) throws RuntimeException;

  /**
   * Update the language of messages returned by the parser.
   *
   * @param language desired language
   */
  void setLanguage(String language); // -> added post-planning phase
}
```

### Notes

* Some methods are noted as added after the planning phase had ended. This was in reaction to
  unforeseen language challenges in parsing objects built with different languages. Additionally,
  most of the changes are to internal APIs, which reduce client impact.
* More importantly, no original API methods were modified to incorporate this change. The main
  pipeline of writing and reading a built game to a file still abides by the original plan.