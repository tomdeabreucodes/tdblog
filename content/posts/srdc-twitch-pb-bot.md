+++
title = 'Creating a Customisable Speedrunning PB Bot on Twitch'
date = 2023-12-22T23:08:35Z
draft = true
+++

## The goal
Speedrunning is a niche rich with stats, and the one that counts for the most is your Personal Best (PB) time in your game of choice. While there are some exceptions, the standard is for communities to have their game set up on Speedrun.com (SRDC) a speedrunning leaderboard website. 

Established speedrunning communities often have a presence on Twitch - the leading livestreaming platform - where runner's will cheer on their favourite streamers from the sidelines via the chat.

Another staple of Twitch chat are the bots, automated assistants that perform helpful functions for the audience/streamer. One particular type of bot I saw in a couple of different communities, including ones I actively participated in, was PB bots. Commands used to retrieve the PB of the streamer. This piqued my interest and I saw potential in a more advanced version of this.

**I set out to create a PB bot which could be customised for any game on SRDC, while preventing hard coding and the constant reinvention of the wheel.**

## Approach
A simple REST API was the ideal solution in my opinion, with the public SRDC API as the data source and a minimal Django app to configure your desired games and categories, as well as handle and structure the data before sending it onwards for use on Twitch. While Twitch was my primary use case, it is trivial to adapt it for use on other ways, such as Discord.

## Tools
- Python
- Django
- Django Rest Framework
- Python Anywhere (Recommended for free hosting, but could be deployed anywhere the user chooses)

## The Code
The code for this project is open source under the MIT licence, and is intended for self hosting. Detailed setup instructions have been documented in the project's README.
TODO add link

## Features
As I mentioned, I had seen simple implementations of PB bots previously, but I saw opportunities for improvement. At the core of my project I wanted it to embed these key features:
- Easy customisation of games and categories you want your bot to include
- Additional customisation of display names used in queries (to accomodate common abbreviations e.g. Super Mario Bros. -> SMB)
- Ability to search both the streamer's PB (default behaviour) 
- Plus option to specify another runner's username
- Completely free to setup and use

## Usage
### Configuration
The configuration is an initial setup, where you choose the games, categories and command names. The user only needs to return to this if they want to update any of these details but they will otherwise be stored in a SQLite database in their instance of the bot.
This is completed in a *very* simple, albeit intuitive GUI shown below, achieved with Django templating.

### Commands
Once your command is set up in your general purpose Twitch bot of choice, chatters in your stream will now be able to easily query PBs without having to switch tabs or close the mobile app!
