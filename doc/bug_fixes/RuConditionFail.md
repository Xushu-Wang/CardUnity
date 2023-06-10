## Description

Summary of the feature's bug (without describing implementation details)

* When the run condition fails, it returns the wrong error message.
* Quotes the empty condition error message, when it should quote the run error message.

## Expected Behavior

Describe the behavior you expect

* The error message should say "All sets must be runs"

## Current Behavior

Describe the actual behavior
* The error message says "All sets must be empty"

## Steps to Reproduce

1. Load a game that uses the Run condition
2. On a turn, place a set that creates an invalid run
3. Observe the processed error message

## Failure Logs

Include any relevant print/LOG statements, error messages, or stack traces.
* Currently is: "[ERROR] 2023-05-02 23:30:43.461 [JavaFX Application Thread] CardViewManager - Phase failed because All sets must be empty"
* Should be: "[ERROR] 2023-05-02 23:30:43.461 [JavaFX Application Thread] CardViewManager - Phase failed because All sets must be runs"

## Hypothesis for Fixing the Bug

Describe the test you think will verify this bug and the code fix you believe will solve this issue.
* RunConditionTest should also include an exception error message