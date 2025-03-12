# Ultitrack
A repository for film watching in ultimate

## Main Features
* Analysis - player summaries, game summaries, tournament summaries, point summaries, etc. Make for quick and compact ways to review games.
* Data Management - imports from Statto and UA, as well as a custom stats format. Offer exports of the data for custom user processing. 
* Data Entry - side by side tool for reviewing film and syncing it with film. Provide ability to track offensive stats and defensive stats. Flesh out a Statto like interface for labeling both at the same time.
* Data Visualization - Supply users with lots of different charts, going a step beyond what is currently available. See the Stats section.
* Player Feedback Generation - create a way to create specific feedback for players, allowing for film clips and coaches notes to be composed into one. Allow players the ability to review their turnovers, goals, etc.


## User Views by LOE by end user.
- Low (goals, assists, turns, Ds, lines). Example would be a single coach at a tournament.
- Medium (each pass with players + throw locations), roughly a replication of Statto. Could be used in person or remotely.
- High (Adds in tracking of fouls, defensive tracking (labeling our defenders)). Would exist only in the web app.
- Ultra (adds in throw type, any additional requests). Web app exclusive.

## Routes to exist within the app
- Index 
  - Details the app and let's you decide amongst your teams, or create new ones.
- Stats Viz
  - All of the different stats views, as detailed in the stats section.
- Data Entry
  - Areas for entering stats, between low-ultra LOE. 
  - Also would allow for syncing stats taken in person to video.
- Analysis / Coach
  - Allow for filtering / searching of events.
  - Allow for creating clips and providing feedback for players.
  - Players could be directed here for feedback.
- Settings
  - Allows for building of rosters, adjusting selected LOE, inviting other coaches or users, etc.

## Stats - Data Viz and Data Searching
1. Specific Player 
    1. Throws chord map (who this player throws to)
    2. Heat maps for where the player catches passes, gets D’s, where they throw passes, throw goals from, catch goals from
    3. All throws a player has thrown on a map. Both pure XY and relative to the thrower.
    4. All throws a player has caught on a map. Both pure XY and relative to the thrower.
    5. All throws a player has defended on a map.
    6. All clips involving the player (film)
    7. All plays involving the player (film)
    8. All points involving the player (film)
    9. All possessions involving the player (film)
    10. All comments from a coach.
    11. Box and whisker plot for throw stuff.
    12. Radar chart for showing which players do the most.
    13. Dendogram (chart with nodes and lines) for each possession.
2. Team
    1. Heat maps for where we throw, D, throw assists and goals from, etc.
    2. Box and whisker plots for what kind of passes everyone catches and throws and defends. Filterable by throw result.
    3. How team players in different amounts of wind, different weather, different times of day.
    4. How team plays when it’s up, when it’s down, and on specific points of a game (e.g. point 13) - give teams a sense of how they preform over time. What throws we throw, if we get Ds, passes per possession, etc.
    5. How a team plays over the course of a year. Visualized by tournament or by games.
    6. Radar charts for players.
    7. Throwing matrix. Filtering by throw result.
    8. Big table of all of other stats.
    9. How long it takes the team to start moving with the disc.
3. Games
    1. Line chart for how much we are up or down
    2. Game profile - was it a blowout? A giveaway? A balanced game? Streaky? + was it a turnover fest, clean, etc
    3. Show all goals (option of hockey assist), Ds, turnovers.
    4. Our record against this team in general.
    5. Game summary walking through each pass.
4. Clips
    1. All clips containing a certain tag
    2. All clips containing a certain player
    3. All clips containing a certain group of players.
    4. All clips from a specific game

## Eco System
* Web Frontend - handles users and authentication. Provides viewing for all of the main features listed above. Expect Auth to use OAuth.

* Discord Bot - handles sending users specific clips and visualizations. Stretch goal.

* Backend Data Service - serves all of this data for users to view. Would feed both the discord bot and the front end. 

* Database - Cockroach DB

Would be targetting a deployment on K8s.

## Open Questions for Implementation 
Designing the format:
* what are the similarities between UA and Statto’s format? What do they not capture?
* How are we going to manage the differences? Do we design an “idealized” pass format and just have both try to match it? A: Yes! The UF2 (ultimate frisbee unified format)
### Dev Considerations
* How should we keep track of what visualizations are supported by what user LOE? Mark the lowest loe possible for each visual?
* Is LOE done by game, by team? By Possession? For example, what if you had film of some games and not others? What about partial film? Need to think this through.
* Should we consider letting users upload their own video? Lots of storage considerations. I think I prefer the youtube route. Need to see how that works with their ToS. 

## Musings
* For ultianalytics stats provide an estimate for yards. Two thoughtful estimate algos - yards of the field / number of passes in possession, OR if data exists, use the players average pass. Provide margins of error if estimates are used.
Building the Website:
* A good option for the player would be the YouTube embed: https://developers.google.com/youtube/iframe_api_reference#Loading_a_Video_Player
* Lets have the weather of the game be able to be input by the user, but also automatically found from a weather api.
* 