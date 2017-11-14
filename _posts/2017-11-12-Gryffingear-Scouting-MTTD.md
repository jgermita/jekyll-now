---
layout: post
title: Gryffingear Scouting at the 2017 Madtown Throwdown
---

This post will look at the key features of Gryffingear's scouting system for the 2017 Madtown Throwdown. This scouting system was integral in making informed strategy decisions throughout qualification matches, during alliance selections, and into eliminations matches. 

The scouting system draws heavy inspiration from teams 2659 and 987 and is built on the groundwork laid by Gryffingear alumni Brian Romero, Javier Serna, and Christian Perry during the 2017 competition season. 

# Goals

The goals of this system were as follows:

1. Collects only the data that matters - quantify qualities that most teams should be more or less proficient at (# of gears scored in matches in 2017), collect yes/no's for boolean qualities (climbing) or "icing on the cake" qualities that fewer teams have (ability to hit 40KPA during the match).
2. Make data entry dead simple - Don't make it a chore to get data from the scouts to the scouting system.
3. Automate as much analysis as possible - matches are played far faster than any human can compile data and produce meaningful metrics and analysis. Automate this data analysis and aggregation.

Goal #1 was accomplished through analysis of how we've played the game thus far. After playing through this game at several events, we have a good grasp at what data is useful for strategic decisions and what is just noise. In the future, this would be accomplished through effective strategic analysis of the game. 

Goal #2 was simple. 2017 competition season saw the rise of Google Forms in our scouting workflow. Google Forms allows us to not reinvent the data-entry wheel by riding on Google's massive infrastructure to collect our data from multiple sources (scouts). The one caveat to our solution is that it relies on scouts using their own data connections to do their jobs. Luckily Forms doesn't transfer too much data up or down, but the problem isn't totally eliminated.

Goal #3 was accomplished using Google Sheets and the powerful formula and query language baked in. Thanks to assistance and advice from various teams, our competition season scouting system further bridged the gap between the data entered and the data aggregated and analyzed.

The MTTD iteration of this system builds on our competition season's solutions to these problems. 

# Overview

## Data Entry

![Google Form](https://i.imgur.com/K3ftppqm.png)

Google Forms is used heavily in data entry. The link to the scouting form for a specific event is shared with the scouting team at the beginning of each event. 

![Raw data in Google Sheet](https://i.imgur.com/pgAJbWcl.png)

After entry, data is automatically sent by Forms to a Google Sheet. All further data analysis references this one sheet. 

![Pit scouting data](https://i.imgur.com/b3o71zql.png)

If needed, pit scouting data like drivetrain type, mechanisms, and robot pictures are also entered into a separate sheet in the same Google Sheets document.

## Analysis and Aggregation

![all team data](https://i.imgur.com/qZjtY2Il.png)

Data on each specific team is eventually summarized by the AllTeamData sheet. This takes all scouted match data and generates metrics such as min, max, and averages on all values. All magic happens thanks to this sheet. 

![team summary sheet](https://i.imgur.com/ZXy4imPl.png)

This view is what I used most frequently as a coach. It uses data from the AllTeamData and Pit Scouting sheets and presents it in large and easy to read format (semi-optimized for mobile) so that I can run queries on specific teams and quickly bring up their data. What used to take hours under our 2016 scouting system took a mere 5 seconds with the 2017 offseason system.

![auto picklist](https://i.imgur.com/YwmLyApl.png)

The next most useful feature of the new system. By using the ATD sheet, each team is scored on a weighted sum of their average gears, climb percentage, died percentage, and other metrics. Doing this, we can automatically generate a pick list to use during alliance selections. Our third pick ended up being a team from the APL. The APL view also has cells that allow us to indicate whether or not teams are picked or should be skipped so that the next major component of the system can work.

![Whiteboard View](https://i.imgur.com/Xr3VgxAl.png)

Whiteboard View! Filling a long-time need in FRC to have a clear, easy to read, "whiteboard" type view, this allows us to communicate to our alliance selections representative from the stands. This was brought up on a 10.1" tablet and displayed to our reps from over 50ft away. This view also has options for "ACCEPT", "DENY", or "DEFER" so that we can fully communicate to our representative. Inspiration for this was drawn by numerous mishaps by my teams as well as countless others to clearly communicate these on-the-fly picks to their rep.

A short demo of APL and Whiteboard are shown below:
[![demo](https://img.youtube.com/vi/iK8YCYPBgzU/0.jpg)](https://www.youtube.com/watch?v=iK8YCYPBgzU&feature=youtu.be)

