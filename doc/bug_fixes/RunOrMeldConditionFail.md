## Description

Summary of the feature's bug (without describing implementation details)

* You are able to play invalid sets on the board and the game will let you advance in Gin Rummy,
  resulting in players winning when they shouldn't have.

## Expected Behavior

Describe the behavior you expect

* Upon submitting an invalid set, the game should display a popup message indicating the error for
  the player.

## Current Behavior

Describe the actual behavior
* Invalid sets are accepted by the board

## Steps to Reproduce

Provide detailed steps for reproducing the issue.
1. Load AlmostWin.json from /data/json/games/ginrummy/saved_examples/AlmostWin.json
2. Play the 4 onto either set on the table
3. Click "End Phase"

## Failure Logs

Include any relevant print/LOG statements, error messages, or stack traces.
* No failure logs because no errors were detected

## Hypothesis for Fixing the Bug

Describe the test you think will verify this bug and the code fix you believe will solve this issue.
* RunOrMeldCondition test is already implemented and will be examined for errors