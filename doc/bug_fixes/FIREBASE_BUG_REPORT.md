## Description

Summary of the feature's bug (without describing implementation details)

   * There is a bug with the Firebase winner statistics code that is causing the check win conditions function
    to crash before the winner is set. The runtime error is being caught by the program and the firebase errors are
    logged, but the game does not crash. This means that the game **wrongly** continues running even after it should have one


## Expected Behavior

Describe the behavior you expect


When a player wins, the game should end and the "playerTransitionPane" should be visible, with a message saying that the player
won. The game should not continue running after the player has won.

## Current Behavior

Currently, when a player wins the game and clicks "End Phase," the game will continue running and will sometimes
display errors from the next phase's conditons being checked. The game will not crash, but it will continue running. 

## Steps to Reproduce

Provide detailed steps for reproducing the issue.

 1. Play a game to completion. 

2. Click "End Phase" after winning the game

3. The game will continue running and will display errors from the next phase's conditions being checked.

*This is documented in [GameBugTest.java](..%2Fsrc%2Ftest%2Fjava%2Foogasalad%2Frunner%2Ffrontend%2FGameBugTest.java)
which is a test that plays a game to completion and then clicks "End Phase" after winning the game. The test
then checks to see if the game is still running, which it should not be. The test fails because the game is still running.*

*This test demonstrates the bug by launching a game that should have ended, but continues running. The test asserts that the "playerWinPane" is visible, 
which is the pane that should be shown when a player wins. The test currently fails.*



## Failure Logs

Include any relevant print/LOG statements, error messages, or stack traces.

```
java.lang.NullPointerException: Cannot invoke "com.google.cloud.firestore.Firestore.collection(String)" because "this.firestoreDb" is null
	oogasalad.service.Firebase.lambda$updatePlayerStats$1(Firebase.java:184)
	java.base/java.util.ArrayList.forEach(ArrayList.java:1511)
	oogasalad.service.Firebase.updatePlayerStats(Firebase.java:183)
	oogasalad.runner.view.CardViewManager.lambda$updatePlayers$1(CardViewManager.java:86)
	java.base/java.util.ArrayList.forEach(ArrayList.java:1511)
	oogasalad.runner.view.CardViewManager.updatePlayers(CardViewManager.java:75)
	oogasalad.runner.view.CardViewManager.lambda$getBoardCallback$0(CardViewManager.java:66)
	java.base/java.util.ArrayList.forEach(ArrayList.java:1511)
	oogasalad.runner.model.board.ConcreteBoard.notifyObservers(ConcreteBoard.java:176)
	oogasalad.runner.model.board.ConcreteBoard.setAllowedMoves(ConcreteBoard.java:120)
	oogasalad.runner.model.stage.Phase.step(Phase.java:43)
	oogasalad.runner.model.stage.Turn.step(Turn.java:32)
	oogasalad.runner.model.stage.Round.step(Round.java:39)
	oogasalad.runner.model.stage.Game.step(Game.java:83)
	oogasalad.runner.frontend.GameBugTest.beginGame(GameBugTest.java:47)
	oogasalad.runner.frontend.GameBugTest.start(GameBugTest.java:38)
	org.testfx.framework.junit5.ApplicationAdapter.start(ApplicationAdapter.java:37)
	org.testfx.toolkit.impl.ApplicationServiceImpl.lambda$start$0(ApplicationServiceImpl.java:49)
	java.base/java.util.concurrent.FutureTask.run(FutureTask.java:264)
	javafx.graphics/com.sun.javafx.application.PlatformImpl.lambda$runLater$10(PlatformImpl.java:457)
	java.base/java.security.AccessController.doPrivileged(AccessController.java:399)
	javafx.graphics/com.sun.javafx.application.PlatformImpl.lambda$runLater$11(PlatformImpl.java:456)
	javafx.graphics/com.sun.glass.ui.InvokeLaterDispatcher$Future.run(InvokeLaterDispatcher.java:96)
--- Trace of caller of unhandled exception in Async Thread ---
	java.base/java.lang.Thread.getStackTrace(Thread.java:1610)
	org.testfx.util.WaitForAsyncUtils$ASyncFXCallable.<init>(WaitForAsyncUtils.java:649)
	org.testfx.util.WaitForAsyncUtils.asyncFx(WaitForAsyncUtils.java:257)
	org.testfx.toolkit.impl.ApplicationServiceImpl.start(ApplicationServiceImpl.java:48)
	org.testfx.toolkit.impl.ToolkitServiceImpl.lambda$setupApplication$6(ToolkitServiceImpl.java:127)
	java.base/java.util.concurrent.FutureTask.run(FutureTask.java:264)
	java.base/java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:539)
	java.base/java.util.concurrent.FutureTask.run(FutureTask.java:264)
	java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1136)
	java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:635)
	java.base/java.lang.Thread.run(Thread.java:833)
```



## Hypothesis for Fixing the Bug

The Firebase object in ``CardViewManager.java`` is not being initialized properly. 
By commenting out the line (86) ``        myFirebase.updatePlayerStats(board.players()); ``
that updates the win statistics in the ``updatePlayers()`` function
the game no longer crashes. This means that the Firebase object is not being initialized properly.