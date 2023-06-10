## High level Game runner Data structure 

LinkedHashmap<"label",methodData> gameStartRules
LinkedHashmap<"label",methodData> gameEndRules
LinkedHashmap<"label",methodData> roundStartRules
LinkedHashmap<"label",methodData> roundEndRules
List<LinkedHashmap<"label",methodData>> turnPhases

List<Class<?>> gameRulesClasses
List<Class<?>> roundRulesClasses 
List<Class<?>> phaseRulesRuleClasses

List<Object> gameRulesInitializationInfo 
List<Object> roundRulesInitializationInfo 
List<Object> phaseRulesInitializationInfo 

Method Data gameEndCondition
Method Data roundEndCondition






LinkedHashmap<"label",methodData> RoundRules
(Convention for RoundRules: Please seperate Start and End rules with a (method call)/methodData referencing to GameController method gamePlayerTurnLoop. Parameter should be PhaseRules).

List<LinkedHashmap<"label",methodData> TurnPhaseRules>
(Convention for phase category class is to have phase end condition/s be final values in linkedhashmap)
(reason for this convention is for unconditioned phase end, can leverage optional access order property of LinkedHashMap to implicitily determine what nextphase move was played to end current phase)



List<LinkedHashmap<"Class",Object initializationInformation">> ClassInitializationInformation
// basically just hold information for initializing classes when neccesary, for unparameterized classes value should be null


((below)these should be ordered same way as in maps. basically just the implementing class names used for creating maps)
List<Class<?>> gameRulesClasses
List<Class<?>> roundRulesClasses
List<Class<?>> phaseRulesRuleClasses



## Method data Class/Object: 

public class MethodData {
    
    private final Method method;
    private final Object object; // dont worry about this
    private final Object parameters;

    public MethodData(Method method, Object parameters) {
      this.method = method;
      this.valueObject = valueObject;
    }

    public Method getMethod() {
      return method;
    }

    public Object getObject() {
      return object;
    }
    public void addObject(){
        this.object=object;
    }

    public Object getValueObject() {
      return valueObject;
    }
  }
}

## Completed filled out datastructure for this implementation: 

LinkedHashMap<String, MethodData> gameStartRules = new LinkedHashMap<>();
//none in this implementation

LinkedHashMap<String, MethodData> gameEndRules = new LinkedHashMap<>();
gameEndRules.put("getWinnerByPoints", new MethodData(SetWinnerByPoints.class.getMethod("getWinnerByPoints", ArrayList.class), new Object[] {"controllerInstanceVar: players"}));

LinkedHashMap<String, MethodData> roundStartRules = new LinkedHashMap<>();

roundStartRules.put("CreateDeck", new MethodData(CreateDeck.class.getMethod("createDeck", String.class, CardDeck.class), new Object[] {"GinRummyDeck"}));

roundStartRules.put("CreateDiscardPile", new MethodData(CreateDiscardPile.class.getMethod("createDiscardPile", CardDeck.class, CardPile.class, int.class), new Object[] {controllerInstanceVar: deck,controllerInstanceVar: discardPile,1}));

roundStartRules.put("DealCard", new MethodData(DealCard.class.getMethod("dealCards", CardDeck.class,List.class,int.class), new Object[] { controllerInstanceVar: deck, controllerInstanceVar: dealer, 7 }));

LinkedHashMap<String, MethodData> roundEndRules = new LinkedHashMap<>();
(Convention is to always have Reset Round and same method from controller class)

roundEndRules.put("AssignPlayerPointsBySetValuesMinusHandValues", new MethodData(AssignPlayerPointsBySetValuesMinusHandValues.class.getMethod("assignPlayerPointsBySetValuesMinusHandValues", ArrayList.class), new Object["controllerInstanceVar: players"]));

roundEndRules.put("ResetRound", new MethodData(Controller.class.getMethod("resetRound",ArrayList.class),new Object[new ArrayList<String>{controllerInstanceVar: points}]))

(this might be a little tricky to impliment, but should be array list of controller instance variables that stay the same through rounds)

List<LinkedHashMap<String,MethodData>> turnPhases= [phase1Map,phase2Map,phase3Map] (names of these maps are abitrary as long as in order)
(convention is for phase ending move to be last value in given phase map)
( Convention for end conditions is key will always be "UnconditionedEndCondition" or "ConditionedEndCondition")

(for this implementation phasrule parameters (second argument of newMethodData can just be blank initialized Object[]))
(later on I will derive a way to make calls to getter methods or something as param arguments to make this more dynamic)


LinkedHashMap<String, MethodData> phase1Map = new LinkedHashMap<>();

turnPhases.put("DrawCardFromDeck", new MethodData(DrawCardFromDeck.class.getMethod("drawCardFromDeck"), new Object[]));

turnPhases.put("DrawCardFromDiscardAndAllCardsAfter", new MethodData(DrawCardFromDiscardAndAllCardsAfter.class.getMethod("drawCardFromDiscardAndAllCardsAfter", CardPile.class, Card.class), new Object[]));

turnPhases.put("ConditionedEndCondition", new MethodData(PlayerGainedCards.class.getMethod("playerGainedCards", Integer.class, Integer.class), new Object[controllerInstanceVar: playerNumberOfCardsStartOfPhase,controllerInstanceVar: playerCurrentNumberOfCards]));

LinkedHashMap<String, MethodData> phase2Map = new LinkedHashMap<>();

turnPhases.put("PlaySet", new MethodData(PlaySet.class.getMethod("playSet", CardPile.class, CardPile.class), new Object[]));

turnPhases.put("PlayCardOnSet", new MethodData(PlayCardOnSet.class.getDeclaredMethod("playCardOnExistingSet", CardPile.class, CardPile.class, Card.class), new Object[]));

turnPhases.put("UnconditionedEndCondition",null);


LinkedHashMap<String, MethodData> phase3Map = new LinkedHashMap<>();

turnPhases.put("DiscardSingleCard", new MethodData(DiscardSingleCard.class.getMethod("discardSingleCard", Card.class, CardPile.class), new Object[]));

turnPhases.put("ConditionedEndCondition", new MethodData(PlayerLostCards.class.getMethod("playerLostCards", Integer.class, Integer.class), new Object[]));



List<Class<?>> gameRulesClasses = Arrays.asList(SetWinnerByPoints.class);

List<Class<?>> roundRulesClasses = Arrays.asList(CreateDeck.class,CreateDiscardPile.class, DealCard.class);

List<Class<?>> phaseRulesRuleClasses = Arrays.asList(DrawCardFromDeck.class, DrawCardFromDiscardAndAllCardsAfter.class, PlaySet.class, DiscardSingleCard.class);

List<Object> gameRulesInitializationInfo = null;
List<Object> roundRulesInitializationInfo =null;
List<Object> phaseRulesInitializationInfo = {List<String>{"controllerInstanceVar: deck","controllerInstanceVar: currentPlayerHand"},"controllerInstanceVar: discardPile", null,List<String> {"SameValueSet","RunOfValuesAndSameSuitSet"},List<String> {"SameValueSet","RunOfValuesAndSameSuitSet"},"controllerInstanceVar: discardPile",null};



Method Data gameEndCondition = new MethodData(PlayerReachPointGoal.class.getMethod("playerReachedPointGoal", ArrayList.class, Integer.class), new Object[null,500]) )

Method Data roundEndCondition = new MethodData(WinConditionPlayerHasNoCards.class.getMethod("playerHasNoCards", Player.class), new Object[]) )









