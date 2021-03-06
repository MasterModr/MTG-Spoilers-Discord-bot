# MTG-Spoilers-Discord-bot
A Discord bot for automatically posting Magic: The Gathering card spoilers. Works with the Scryfall API.

## Commands
Command prefix is '!', no functionality implemented yet to adjust this.
### getall/getallcards [SETCODE]
Will send a message for every card from the set with the given setcode that hasn't been send in that channel yet.
### watch/startwatch [SETCODE]
Will start a watch for the set with the given setcode. This means the bot will watch for any unsent cards for that set and automatically send any new cards to the channel every half hour.
### unwatch/stopwatch [SETCODE]
Will stop the watch for the set with the given setcode if any is currently started. This will stop the bot from watching for unsent cards and stop it from sending any messages automatically.
### clear [SETCODE]
Will clear the list of any already sent cards from the set with the given setcode. This means the bot will stop excluding these cards from being send to the channel with the 'getall' and 'watch' commands, and send every card from that set again when using these commands.

## File Structure
```
* root parent directory
/ * [project root]
/ * [node_modules]
/ * auth.js
/ * data
/ / * watchedsetcodes.json
/ / * [channelId]-[setCode]-data.json files
```

[project root] here contains the root of this git project, so files like bot.js go on this level. Auth.js is the file containing your token to connect your bot to the Discord API, which. The /data directory contains all data files the bot needs to function, and these will all be generated automatically when the bot is running (including the data directory itself). Both auth.js and /data are gitignored.

## Data files
### watchedsetcodes.json
This file contains a list of entries telling the bot which channel is expecting cards from which set. Every entry has the following format:
```json
{
  "setCode": "xxx",
  "channelID": "xxxxxxxxxxxxxxxxxx"
}
```
The value of "setCode" here is the three letter abbreviation of the set (e.g. "m21"). The value of "channelID" is the Discord channel ID.
### [channelId]-[setCode]-data.json files
For every combination channelID-setCode that has cards sent to it, the bot will create one of these files, with the corresponding channelID and setCode in the filename. Each files is a simple list of IDs that Scryfall gives to every magic card. The ID used is the oracle_ID which is unique for every mechanically different card, but not for alternate arts. This means that only one unique art/frame for every card will be sent by the bot.
