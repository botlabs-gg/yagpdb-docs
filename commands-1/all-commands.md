## General ℹ️

### Help

**Aliases:** commands/h/how/command

Shows help about all or one specific command


**Usage:**
```
Help [command:Text]
```
### Info

Responds with bot information


**Usage:**
```
Info
```
### Invite

Responds with bot invite link


**Usage:**
```
Invite
```
## Tools & Utilities 🔨

### Prefix

Shows command prefix of the current server, or the specified server


**Usage:**
```
Prefix [Server ID:Whole number]
```
### Calc

**Aliases:** c/calculate

Calculator 2+2=5


**Usage:**
```
Calc <Expression:Text>
```
### Ping

I prefer tabletennis (Shows the bots ping to the discord servers)


**Usage:**
```
Ping
```
### CurrentTime

**Aliases:** ctime/gettime

Shows current time in different timezones. [Available timezones](https://pastebin.com/ZqSPUhc7)


**Usage:**
```
CurrentTime <Offset:Whole number>
CurrentTime <Zone:Text>
CurrentTime

```
### MentionRole

**Aliases:** mrole

Sets a role to mentionable, mentions the role, and then sets it back
Requires the manage roles permission and the bot being above the mentioned role

**Usage:**
```
MentionRole <Role:Text> [Message:Text]
```
### ListRoles

List roles and their id's, and some other stuff on the server


**Usage:**
```
ListRoles
```
### Poll

Create a reaction poll.


**Usage:**
```
Poll <Topic:Text - Description of the poll> <Option1:Text> <Option2:Text> [Option3:Text] [Option4:Text] [Option5:Text] [Option6:Text] [Option7:Text] [Option8:Text] [Option9:Text] [Option10:Text]
```
### Undelete

**Aliases:** ud

Views your recent deleted messages, or all users deleted messages (with "-a" and manage messages perm) in this channel


**Usage:**
```
Undelete
```
```
[-a all:Switch]

```
### ViewPerms

Shows you or the targets permissions in this channel


**Usage:**
```
ViewPerms [target:Mention/ID]
```
### Stats

Shows server stats (if public stats are enabled)


**Usage:**
```
Stats
```
### CustomCommands

**Aliases:** cc

Shows a custom command specified by id or trigger, or lists them all


**Usage:**
```
CustomCommands <ID:Whole number>
CustomCommands <Trigger:Text>
CustomCommands

```
### Logs

**Aliases:** log

Creates a log of the last messages in the current channel
This includes deleted messages within an hour

**Usage:**
```
Logs [Count:Whole number]
```
### Whois

**Aliases:** whoami

shows information about a user


**Usage:**
```
Whois [User:User]
```
### Nicknames

**Aliases:** nn

Shows past nicknames of a user


**Usage:**
```
Nicknames [User:User]
```
### Usernames

**Aliases:** unames/un

Shows past usernames of a user


**Usage:**
```
Usernames [User:User]
```
### Remindme

**Aliases:** remind

Schedules a reminder, example: 'remindme 1h30min are you alive still?'


**Usage:**
```
Remindme <Time:Duration> <Message:Text>
```
### Reminders

Lists your active reminders


**Usage:**
```
Reminders
```
### CReminders

Lists reminders in channel, only users with 'manage server' permissions can use this.


**Usage:**
```
CReminders
```
### Delreminder

**Aliases:** rmreminder

Deletes a reminder.


**Usage:**
```
Delreminder <ID:Whole number>
```
### Role

Give yourself a role or list all available roles, the roles have to be set up in the control panel first, under 'rolecommands'


**Usage:**
```
Role [Role:Text]
```
## Fun 🎉

### Define

**Aliases:** df

Look up an urban dictionary definition


**Usage:**
```
Define <Topic:Text>
```
### Weather

**Aliases:** w

Shows the weather somewhere


**Usage:**
```
Weather <Where:Text>
```
### Topic

Generates a chat topic


**Usage:**
```
Topic
```
### CatFact

**Aliases:** cf/cat/catfacts

Cat Facts


**Usage:**
```
CatFact
```
### Advice

Get advice


**Usage:**
```
Advice [What:Text]
```
### Throw

Cause you are a rebel


**Usage:**
```
Throw [Target:User]
```
### Roll

Roll dices, specify nothing for 6 sides, specify a number for max sides, or rpg dice syntax


**Usage:**
```
Roll <Sides:Whole number>
Roll <RPG Dice:Text>
Roll

```
### CustomEmbed

**Aliases:** ce

Creates an embed from what you give it in json form: https://discordapp.com/developers/docs/resources/channel#embed-object


**Usage:**
```
CustomEmbed <Json:Text>
```
### WouldYouRather

**Aliases:** wyr

Get presented with 2 options.


**Usage:**
```
WouldYouRather
```
### TopServers

Responds with the top 15 servers I'm on


**Usage:**
```
TopServers [Skip:Whole number - Entries to skip]
```
### TakeRep

**Aliases:** -/tr/trep/-rep

Takes away rep from someone


**Usage:**
```
TakeRep <User:User> [Num:Whole number]
```
### GiveRep

**Aliases:** +/gr/grep/+rep

Gives rep to someone


**Usage:**
```
GiveRep <User:User> [Num:Whole number]
```
### SetRep

**Aliases:** SetRepID

Sets someones rep, this is an admin command and bypasses cooldowns and other restrictions.


**Usage:**
```
SetRep <User:Mention/ID> <Num:Whole number>
```
### DelRep

Deletes someone from the reputation list completely, this cannot be undone.


**Usage:**
```
DelRep <User:Mention/ID>
```
### RepLog

**Aliases:** replogs

Shows the rep log for the specified user.


**Usage:**
```
RepLog <User:Mention/ID> [Page:Whole number]
```
### Rep

Shows yours or the specified users current rep and rank


**Usage:**
```
Rep [User:User]
```
### TopRep

Shows top 15 rep on the server


**Usage:**
```
TopRep [Offset:Whole number]
```
### sentiment

**Aliases:** sent

Does sentiment analysys on a message or your last 5 messages longer than 3 words


**Usage:**
```
sentiment [text:Text]
```
### 8Ball

Wisdom


**Usage:**
```
8Ball <What to ask:Text>
```
### Soundboard

**Aliases:** sb

Play, or list soundboard sounds


**Usage:**
```
Soundboard [Name:Text]
```
### cah create

**Aliases:** c

Creates a cards against humanity game in this channel, add packs after commands, or * for all packs. (-v for vote mode without a card czar)


**Usage:**
```
create [packs:Text - Packs seperated by space, or * for all of them]
```
```
[-v Vote mode, players vote instead of having a cardczar:Switch]

```
### cah end

Ends a cards against humanity game thats ongoing in this channel


**Usage:**
```
end
```
### cah kick

Kicks a player from the ongoing cards against humanity game in this channel


**Usage:**
```
kick <user:Mention/ID>
```
### cah packs

Lists available packs


**Usage:**
```
packs
```
## Debug & Maintenance 🖥

### CurrentShard

**Aliases:** cshard

Shows the current shard this server is on (or the one specified


**Usage:**
```
CurrentShard [serverid:Whole number]
```
### MemberFetcher

**Aliases:** memfetch

Shows the current status of the member fetcher


**Usage:**
```
MemberFetcher
```
### Yagstatus

**Aliases:** status

Shows yagpdb status, version, uptime, memory stats, and so on


**Usage:**
```
Yagstatus
```
### roledbg

Debug debug debug autorole assignment


**Usage:**
```
roledbg
```
## Moderation 👮

### Ban

**Aliases:** banid

Bans a member, specify a duration with -d


**Usage:**
```
Ban <User:Mention/ID> [Reason:Text]
```
```
[-d Duration:Duration]

```
### Kick

Kicks a member


**Usage:**
```
Kick <User:Mention/ID> [Reason:Text]
```
### Mute

Mutes a member


**Usage:**
```
Mute <User:User Mention> <Duration:Duration> <Reason:Text>
Mute <User:User Mention> <Reason:Text> <Duration:Duration>
Mute <User:User Mention> <Duration:Duration>
Mute <User:User Mention> <Reason:Text>
Mute <User:User Mention>

```
### Unmute

Unmutes a member


**Usage:**
```
Unmute <User:User Mention> [Reason:Text]
```
### Report

Reports a member to the server's staff


**Usage:**
```
Report <User:Mention/ID> <Reason:Text>
```
### Clean

**Aliases:** clear/cl

Delete the last number of messages from chat, optionally filtering by user, max age and regex.
Specify a regex with "-r regex_here" and max age with "-ma 1h10m"
Note: Will only look in the last 1k messages

**Usage:**
```
Clean <Num:Whole number>
Clean <Num:Whole number> <User:User Mention>
Clean <User:User Mention> <Num:Whole number>

```
```
[-r Regex:Text]
[-ma Max age:Duration]
[-i Regex case insensitive:Switch]

```
### Reason

Add/Edit a modlog reason


**Usage:**
```
Reason <ID:Whole number> <Reason:Text>
```
### Warn

Warns a user, warnings are saved using the bot. Use -warnings to view them.


**Usage:**
```
Warn <User:User Mention> <Reason:Text>
```
### Warnings

**Aliases:** Warns

Lists warning of a user.


**Usage:**
```
Warnings <User:Mention/ID>
```
### EditWarning

Edit a warning, id is the first number of each warning from the warnings command


**Usage:**
```
EditWarning <Id:Whole number> <NewMessage:Text>
```
### DelWarning

**Aliases:** dw

Deletes a warning, id is the first number of each warning from the warnings command


**Usage:**
```
DelWarning <Id:Whole number>
```
### ClearWarnings

**Aliases:** clw

Clears the warnings of a user


**Usage:**
```
ClearWarnings <User:Mention/ID>
```
### automod toggle

**Aliases:** t

Toggles a ruleset on/off


**Usage:**
```
toggle <ruleset name:Text>
```
## Rolemenu 🔘

### RoleMenu Create

**Aliases:** c

Set up a role menu, specify a message with -m to use an existing message instead of having the bot make one

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.


**Usage:**
```
Create <Group:Text>
```
```
[-m Message ID:Whole number]
[-nodm Disable DM:Switch]
[-rr Remove role on reaction removed:Switch]
[-skip Number of roles to skip:Whole number]

```
### RoleMenu Remove

Removes a rolemenu from a message, the message won't be deleted but the bot will now not do anything with reactions on that message

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.


**Usage:**
```
Remove <Message ID:Whole number>
```
### RoleMenu Update

**Aliases:** u

Updates a rolemenu, toggling the provided flags and adding missing options, aswell as updating the order.

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.


**Usage:**
```
Update <Message ID:Whole number>
```
```
[-nodm Disable DM:Switch]
[-rr Remove role on reaction removed:Switch]

```
### RoleMenu ResetReactions

**Aliases:** reset

Removes all reactions on the specified menu message and re-adds them, can be used to fix the order after updating it.

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.


**Usage:**
```
ResetReactions <Message ID:Whole number>
```
### RoleMenu EditOption

**Aliases:** edit

Allows you to reassign the emoji of an option, tip: use ResetReactions afterwards

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.


**Usage:**
```
EditOption <Message ID:Whole number>
```

jonas@DESKTOP-FS4STM5 MINGW64 /d/gp/src/github.com/jonas747/yagpdb/cmd/yagpdb
$ go build

jonas@DESKTOP-FS4STM5 MINGW64 /d/gp/src/github.com/jonas747/yagpdb/cmd/yagpdb
$ ./yagpdb.exe -gencmddocs -bot
INFO[0000] YAGPDB is initializing...
WARN[0000] No datadog info provided, not connecting to datadog aggregator
DEBU[0000] Added event handler                           evt=invalidate_guild_config_cache stck="pubsub.AddHandler:pubsub.go:49"
INFO[0000] Listening for bot leaves and join
INFO[0001] Registered patreon premium source
## General ℹ️

### Help

**Aliases:** commands/h/how/command

Shows help about all or one specific command


**Usage:**
```
Help [command:Text]
```

### Info

Responds with bot information


**Usage:**
```
Info
```

### Invite

Responds with bot invite link


**Usage:**
```
Invite
```

## Tools & Utilities 🔨

### Prefix

Shows command prefix of the current server, or the specified server


**Usage:**
```
Prefix [Server ID:Whole number]
```

### Calc

**Aliases:** c/calculate

Calculator 2+2=5


**Usage:**
```
Calc <Expression:Text>
```

### Ping

I prefer tabletennis (Shows the bots ping to the discord servers)


**Usage:**
```
Ping
```

### CurrentTime

**Aliases:** ctime/gettime

Shows current time in different timezones. [Available timezones](https://pastebin.com/ZqSPUhc7)


**Usage:**
```
CurrentTime <Offset:Whole number>
CurrentTime <Zone:Text>
CurrentTime

```

### MentionRole

**Aliases:** mrole

Sets a role to mentionable, mentions the role, and then sets it back
Requires the manage roles permission and the bot being above the mentioned role

**Usage:**
```
MentionRole <Role:Text> [Message:Text]
```

### ListRoles

List roles and their id's, and some other stuff on the server


**Usage:**
```
ListRoles
```

### Poll

Create a reaction poll.


**Usage:**
```
Poll <Topic:Text - Description of the poll> <Option1:Text> <Option2:Text> [Option3:Text] [Option4:Text] [Option5:Text] [Option6:Text] [Option7:Text] [Option8:Text] [Option9:Text] [Option10:Text]
```

### Undelete

**Aliases:** ud

Views your recent deleted messages, or all users deleted messages (with "-a" and manage messages perm) in this channel


**Usage:**
```
Undelete
```
```
[-a all:Switch]

```

### ViewPerms

Shows you or the targets permissions in this channel


**Usage:**
```
ViewPerms [target:Mention/ID]
```

### Stats

Shows server stats (if public stats are enabled)


**Usage:**
```
Stats
```

### CustomCommands

**Aliases:** cc

Shows a custom command specified by id or trigger, or lists them all


**Usage:**
```
CustomCommands <ID:Whole number>
CustomCommands <Trigger:Text>
CustomCommands

```

### Logs

**Aliases:** log

Creates a log of the last messages in the current channel
This includes deleted messages within an hour

**Usage:**
```
Logs [Count:Whole number]
```

### Whois

**Aliases:** whoami

shows information about a user


**Usage:**
```
Whois [User:User]
```

### Nicknames

**Aliases:** nn

Shows past nicknames of a user


**Usage:**
```
Nicknames [User:User]
```

### Usernames

**Aliases:** unames/un

Shows past usernames of a user


**Usage:**
```
Usernames [User:User]
```

### Remindme

**Aliases:** remind

Schedules a reminder, example: 'remindme 1h30min are you alive still?'


**Usage:**
```
Remindme <Time:Duration> <Message:Text>
```

### Reminders

Lists your active reminders


**Usage:**
```
Reminders
```

### CReminders

Lists reminders in channel, only users with 'manage server' permissions can use this.


**Usage:**
```
CReminders
```

### Delreminder

**Aliases:** rmreminder

Deletes a reminder.


**Usage:**
```
Delreminder <ID:Whole number>
```

### Role

Give yourself a role or list all available roles, the roles have to be set up in the control panel first, under 'rolecommands'


**Usage:**
```
Role [Role:Text]
```

## Fun 🎉

### Define

**Aliases:** df

Look up an urban dictionary definition


**Usage:**
```
Define <Topic:Text>
```

### Weather

**Aliases:** w

Shows the weather somewhere


**Usage:**
```
Weather <Where:Text>
```

### Topic

Generates a chat topic


**Usage:**
```
Topic
```

### CatFact

**Aliases:** cf/cat/catfacts

Cat Facts


**Usage:**
```
CatFact
```

### Advice

Get advice


**Usage:**
```
Advice [What:Text]
```

### Throw

Cause you are a rebel


**Usage:**
```
Throw [Target:User]
```

### Roll

Roll dices, specify nothing for 6 sides, specify a number for max sides, or rpg dice syntax


**Usage:**
```
Roll <Sides:Whole number>
Roll <RPG Dice:Text>
Roll

```

### CustomEmbed

**Aliases:** ce

Creates an embed from what you give it in json form: https://discordapp.com/developers/docs/resources/channel#embed-object


**Usage:**
```
CustomEmbed <Json:Text>
```

### WouldYouRather

**Aliases:** wyr

Get presented with 2 options.


**Usage:**
```
WouldYouRather
```

### TopServers

Responds with the top 15 servers I'm on


**Usage:**
```
TopServers [Skip:Whole number - Entries to skip]
```

### TakeRep

**Aliases:** -/tr/trep/-rep

Takes away rep from someone


**Usage:**
```
TakeRep <User:User> [Num:Whole number]
```

### GiveRep

**Aliases:** +/gr/grep/+rep

Gives rep to someone


**Usage:**
```
GiveRep <User:User> [Num:Whole number]
```

### SetRep

**Aliases:** SetRepID

Sets someones rep, this is an admin command and bypasses cooldowns and other restrictions.


**Usage:**
```
SetRep <User:Mention/ID> <Num:Whole number>
```

### DelRep

Deletes someone from the reputation list completely, this cannot be undone.


**Usage:**
```
DelRep <User:Mention/ID>
```

### RepLog

**Aliases:** replogs

Shows the rep log for the specified user.


**Usage:**
```
RepLog <User:Mention/ID> [Page:Whole number]
```

### Rep

Shows yours or the specified users current rep and rank


**Usage:**
```
Rep [User:User]
```

### TopRep

Shows top 15 rep on the server


**Usage:**
```
TopRep [Offset:Whole number]
```

### sentiment

**Aliases:** sent

Does sentiment analysys on a message or your last 5 messages longer than 3 words


**Usage:**
```
sentiment [text:Text]
```

### 8Ball

Wisdom


**Usage:**
```
8Ball <What to ask:Text>
```

### Soundboard

**Aliases:** sb

Play, or list soundboard sounds


**Usage:**
```
Soundboard [Name:Text]
```

### cah create

**Aliases:** c

Creates a cards against humanity game in this channel, add packs after commands, or * for all packs. (-v for vote mode without a card czar)


**Usage:**
```
create [packs:Text - Packs seperated by space, or * for all of them]
```
```
[-v Vote mode, players vote instead of having a cardczar:Switch]

```

### cah end

Ends a cards against humanity game thats ongoing in this channel


**Usage:**
```
end
```

### cah kick

Kicks a player from the ongoing cards against humanity game in this channel


**Usage:**
```
kick <user:Mention/ID>
```

### cah packs

Lists available packs


**Usage:**
```
packs
```

## Debug & Maintenance 🖥

### CurrentShard

**Aliases:** cshard

Shows the current shard this server is on (or the one specified


**Usage:**
```
CurrentShard [serverid:Whole number]
```

### MemberFetcher

**Aliases:** memfetch

Shows the current status of the member fetcher


**Usage:**
```
MemberFetcher
```

### Yagstatus

**Aliases:** status

Shows yagpdb status, version, uptime, memory stats, and so on


**Usage:**
```
Yagstatus
```

### roledbg

Debug debug debug autorole assignment


**Usage:**
```
roledbg
```

## Moderation 👮

### Ban

**Aliases:** banid

Bans a member, specify a duration with -d


**Usage:**
```
Ban <User:Mention/ID> [Reason:Text]
```
```
[-d Duration:Duration]

```

### Kick

Kicks a member


**Usage:**
```
Kick <User:Mention/ID> [Reason:Text]
```

### Mute

Mutes a member


**Usage:**
```
Mute <User:User Mention> <Duration:Duration> <Reason:Text>
Mute <User:User Mention> <Reason:Text> <Duration:Duration>
Mute <User:User Mention> <Duration:Duration>
Mute <User:User Mention> <Reason:Text>
Mute <User:User Mention>

```

### Unmute

Unmutes a member


**Usage:**
```
Unmute <User:User Mention> [Reason:Text]
```

### Report

Reports a member to the server's staff


**Usage:**
```
Report <User:Mention/ID> <Reason:Text>
```

### Clean

**Aliases:** clear/cl

Delete the last number of messages from chat, optionally filtering by user, max age and regex.
Specify a regex with "-r regex_here" and max age with "-ma 1h10m"
Note: Will only look in the last 1k messages

**Usage:**
```
Clean <Num:Whole number>
Clean <Num:Whole number> <User:User Mention>
Clean <User:User Mention> <Num:Whole number>

```
```
[-r Regex:Text]
[-ma Max age:Duration]
[-i Regex case insensitive:Switch]

```

### Reason

Add/Edit a modlog reason


**Usage:**
```
Reason <ID:Whole number> <Reason:Text>
```

### Warn

Warns a user, warnings are saved using the bot. Use -warnings to view them.


**Usage:**
```
Warn <User:User Mention> <Reason:Text>
```

### Warnings

**Aliases:** Warns

Lists warning of a user.


**Usage:**
```
Warnings <User:Mention/ID>
```

### EditWarning

Edit a warning, id is the first number of each warning from the warnings command


**Usage:**
```
EditWarning <Id:Whole number> <NewMessage:Text>
```

### DelWarning

**Aliases:** dw

Deletes a warning, id is the first number of each warning from the warnings command


**Usage:**
```
DelWarning <Id:Whole number>
```

### ClearWarnings

**Aliases:** clw

Clears the warnings of a user


**Usage:**
```
ClearWarnings <User:Mention/ID>
```

### automod toggle

**Aliases:** t

Toggles a ruleset on/off


**Usage:**
```
toggle <ruleset name:Text>
```

## Rolemenu 🔘

### RoleMenu Create

**Aliases:** c

Set up a role menu, specify a message with -m to use an existing message instead of having the bot make one

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.


**Usage:**
```
Create <Group:Text>
```
```
[-m Message ID:Whole number]
[-nodm Disable DM:Switch]
[-rr Remove role on reaction removed:Switch]
[-skip Number of roles to skip:Whole number]

```

### RoleMenu Remove

Removes a rolemenu from a message, the message won't be deleted but the bot will now not do anything with reactions on that message

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.


**Usage:**
```
Remove <Message ID:Whole number>
```

### RoleMenu Update

**Aliases:** u

Updates a rolemenu, toggling the provided flags and adding missing options, aswell as updating the order.

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.


**Usage:**
```
Update <Message ID:Whole number>
```
```
[-nodm Disable DM:Switch]
[-rr Remove role on reaction removed:Switch]

```

### RoleMenu ResetReactions

**Aliases:** reset

Removes all reactions on the specified menu message and re-adds them, can be used to fix the order after updating it.

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.


**Usage:**
```
ResetReactions <Message ID:Whole number>
```

### RoleMenu EditOption

**Aliases:** edit

Allows you to reassign the emoji of an option, tip: use ResetReactions afterwards

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.


**Usage:**
```
EditOption <Message ID:Whole number>
```
