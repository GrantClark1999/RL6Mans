## About

RL6Mans is a Discord Bot that allows you to create multiple 6-Mans queues in the same server, with elegant reaction-based design.

## General Commands (Discord)

| Command              | Action                        |
| -------------------- | ----------------------------- |
| rl!help              | Displays all commands         |
| rl!queue             | Creates a new game            |
| rl!leave             | Leave any queue you are in    |
| rl!leaderboards      | Leaves any game you may be in |
| rl!getstats (player) | Shows the stats of the player |

## Host-Only Commands (Discord)

| Command | Action                        |
| ------- | ----------------------------- |
| rl!kick | Kicks a player from your game |

## Admin-Only Commands (Discord)

| Command                        | Action                                 |
| ------------------------------ | -------------------------------------- |
| rl!setwins (player) (wins)     | Sets the number of wins for a player   |
| rl!setlosses (player) (losses) | Sets the number of losses for a player |
| rl!prefix (newPrefix)          | View or change the current prefix      |
| rl!reset                       | Reset the leaderboards for your guild  |

## Gameplay

### **Starting a Queue**

To start queueing for a 6-mans, type `rl!queue`. You will become the host of that queue, and people of your rank or higher will be able to join your queue.

### **Registration**

When the queue starts, a message will be sent out for other users to register in your game.

&nbsp;&nbsp;&nbsp;&nbsp;Embed / Message:
  - The host of the queue
  - The role(s) that queue allows
  - The current registered players, along with their respective statuses and rank/roles
  - Reaction -> Action mapping

&nbsp;&nbsp;&nbsp;&nbsp;Reactions:
  - ✅ -> Join/Leave
  - 🟢 -> Ready/Not Ready

&nbsp;&nbsp;&nbsp;&nbsp;Next State:
  - [Mode Select](#mode-select) : When 6 people have joined the queue and have all readied-up

### **Mode Select**

&nbsp;&nbsp;&nbsp;&nbsp;Embed / Message:
  - Reaction -> Action mapping

&nbsp;&nbsp;&nbsp;&nbsp;Reactions:
  - 👑 -> Captains Mode
  - 🔄 -> Random Mode

&nbsp;&nbsp;&nbsp;&nbsp;Next State:
  - [Captains Mode](#captains-mode) : When at least 4 people have chosen captains mode
  - [Random Mode](#random-mode) : When at least 4 people have chosen random mode

#### **Captains Mode**

In this mode, two people from the queue will be chosen at random to be the team captains. One of the captains will be chosen at random to go first. That captain will choose 1 player to add to their team. The second captain will then choose 2 players to add to their team. The last player will be assigned to the first captain's team.

&nbsp;&nbsp;&nbsp;&nbsp;Embed / Message:
  - Show current teams
  - Show number emoji + player name for each unassigned player
  - Reaction -> Action mapping
  - When player is selected, edit embed with ❌ emoji to show they can no longer be selected.

&nbsp;&nbsp;&nbsp;&nbsp;Reactions:
  - 1️⃣, 2️⃣, 3️⃣, 4️⃣ -> One for each player

&nbsp;&nbsp;&nbsp;&nbsp;Next State:
  - [Play Game](#play-game) : When all players are assigned teams

#### **Random Mode**

In this mode, teams are assigned completely at random.

&nbsp;&nbsp;&nbsp;&nbsp;Embed / Message:
  - Show current teams

&nbsp;&nbsp;&nbsp;&nbsp;Reactions:
  - 🔄 -> Re-randomize teams
  - ▶ -> Play game

&nbsp;&nbsp;&nbsp;&nbsp;Next State:
  - [Random Mode](#random-mode) : When at least `4` players have chosen to re-randomize the teams.
  - [Play Game](#play-game) : When at least `4` players have chosen to play the game / accept the current teams.


### **Play Game**

Now, you play your Rocket League match. Report back when the game ends.

&nbsp;&nbsp;&nbsp;&nbsp;Embed / Message:
  - Instructions
  - Current Teams
  - Reaction -> Action mapping

&nbsp;&nbsp;&nbsp;&nbsp;Reactions:
  - ▶ -> Report winner / loser

&nbsp;&nbsp;&nbsp;&nbsp;Next State:
  - [Report](#report) : When at least `4` people have indicated that the match has ended.


### **Report**

Report the results of the last match. Will assign points based on match winner and update database.

&nbsp;&nbsp;&nbsp;&nbsp;Embed / Message:
  - Instructions
  - Reaction -> Action mapping

&nbsp;&nbsp;&nbsp;&nbsp;Reactions:
  - 🟠 -> Orange team won
  - 🔵 -> Blue team won

&nbsp;&nbsp;&nbsp;&nbsp;Next State:
  - [Continue?](#play-again)


### **Continue?**

Players can determine if they would like to play another match/series, or if they would like to stop.

&nbsp;&nbsp;&nbsp;&nbsp;Embed / Message:
  - Instructions
  - Reaction -> Action mapping

&nbsp;&nbsp;&nbsp;&nbsp;Reactions:
  - 🔄 -> New match/series
  - ⏹ -> End match/series

&nbsp;&nbsp;&nbsp;&nbsp;Next State:
  - [Play Game](#play-game) : When at least `4` people have chosen to do a new match/series
  - [End Game](#end-game) : When at least `4` people have chosen to end the current match/series.


### **End Game**

Ends the match/series and show the results of the series. Allows users to now start a new queue

&nbsp;&nbsp;&nbsp;&nbsp;Embed/Message:
  - Player list with respective MMR changes

&nbsp;&nbsp;&nbsp;&nbsp;Reactions: *none*

&nbsp;&nbsp;&nbsp;&nbsp;Next State: *none*