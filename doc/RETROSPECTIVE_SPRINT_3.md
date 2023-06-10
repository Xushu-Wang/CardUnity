# OOGASalad Retrospective Discussion
### TEAM 1
### Names - Del, Shriya, Alec, Ken, Emily, Sophie, Andy, Russel, Ted, Tim


## Project's current progress

* At this point in the project, each of the three parts of the product are working independantly, but a full integration has not been completed.
* The builder can take user input and generate a `GameBuilderRecor` object based on data in the UI
* The parser can take the ``GameBuilderRecord`` object and generate a JSON file
* The RunnerLoader can parse the JSON file and create a GameStage object
* The Runner can generate a UI based for the game

*However, currently, the builder does not have all of the avaiaible game rules implemented as selectors into the UI. Likewise, the GameRunner does not have implemented methods for all of the possible rules in the JSON file so a Gin Rummy game can not be executed based on a JSON file at this time.*


## Current level of communication
Our group commuicates well. We have been meeting regularly 2-3 times a week as a full group as well as using a GroupMe chat that we made. Sub teams meet more frequently.


## Satisfaction with team roles

* For the most part, the work load has been pretty evenly split among the group members. We broke the project into three parts. This made the project seem less dauting than one or two pieces.

## Teamwork that worked well

* Thing #1

We have spent more time doing "housekeeping" such as creating and resolving issues on GitLab to keep track of what needs to be done. This has helped us to stay on track and make sure that everyone is aware of what needs to be done.

* Thing #2

We have worked to refine the exception handling and language support for the project
The parser is now more robust because it can handle exceptions and errors in the JSON file. The RunnerLoader can now handle exceptions and errors in the JSON file.
There is also now a foundation for multiple language support for error messages that can extended from the parser to the rest of the proejct. Documentation for this can
found in the `i18n` package in filemanager.


## Teamwork that could be improved

* Thing #1

  We had a number of team meetings in the initial planning phase where we worked out how the game data would be encoded and transfered from the backend to the frontend. Once we started coding, the Parser team met with the Builder team to discuss the specific formatting of the objects and the JSON file. However, the parser team didn't meet with the runner team until later in the week. At that point the Runner team had come come up with a slightly different implementation of the condition checking than the Builder team was anticipating. This caused us to have to reconcile the two designs which slowed down the process. **Making sure that everyone is on the same page about implemetnation level details before splitting up into groups is something that we need to work on**


* Thing #2

When we split into sub teams, the workload was not proprotional to the number of people on each team. Obviously, this is somewhat difficult to anticipate before actually writing any code, but we had to redistribute team members from the Builder to the Runner team. For the next sprint, we will try to use what we learned from the first phase of the project to make the workload more even.


## Teamwork to improve next Sprint

For the next sprint, we want to focus on using additional markdown files to keep the team on track. We also want to start this sprint by refactoring our code, adding Javadoc comments, and writing tests, and consolidating some packages with duplicate names. This wasn't a priority for the first deadline for the midpoint presentation, but for the final project it is important to start refining our code and documenting our work before moving on to add more features. 


# Extensions

## Player Profile
- Username
- Password
- Email (depending on external database)
- Number of games played - stats
    - Wins/Losses
    - broken down by game type and total
- Number of games made - stats
    - Number of times played
    - broken down by total and also by number of different players played
- Deleted Games
    - JSON files of deleted games
    - restore feature
- FOR ADMIN ONLY
    - view other player's profiles
    - can delete them

## Player Roles
1. Admin
    - Delete all games
    - Delete all users
    - Make games
    - Play any games

2. Premium Member
    - Delete their own games
    - Make their own games
    - Play any number of games

3. Regular Member
    - Can make and play their own games
    - Can delete their own games
    - Can only play 3 of other people's games

4. Guest
    - Cannot make or delete any games
    - Can only play 3 games
