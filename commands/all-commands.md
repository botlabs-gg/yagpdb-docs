# All Commands

## Legend

`<required arg>` `[optional arg]`

Text arguments containing multiple words needs be to put in quotes ("arg here") or backticks (\`arg here\`) if it's not the last argument and there's more than 1 text argument.

For example with the poll command if you want the question to have multiple words: `-poll "what's your favourite colour" red blue green2`

Most Debug & Maintenance commands, or commands without any meaningful description are meant for bot owner or serverAdmin only!

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

### Calc

**Aliases:** c/calculate

Calculator 2+2=5

**Usage:**

```
Calc <Expression:Text>
```

### CReminders

Lists reminders in channel, only users with 'manage server' permissions can use this.

**Usage:**

```
CReminders
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

### CustomCommands

**Aliases:** cc

Shows a custom command specified by id or trigger, or lists them all

**Usage:**

```
CustomCommands <ID:Whole number>
CustomCommands <Trigger:Text>
CustomCommands
```

```
[-file Sends responses in a file:Switch]
[-color Use syntax highlighting (GO):Switch]
```

### DelReminder

**Aliases:** rmreminder

Deletes a reminder. You can delete reminders from other users provided you are running this command in the same guild the reminder was created in and have the Manage Channel permission in the channel the reminder was created in.

**Usage:**

```
DelReminder <ID:Whole number>
```

```
[-a All:Switch]
```

### Fixscheduledccs

???

**Usage:**

```
fixscheduledccs
```

### ListRoles

List roles, their id's, color hex code, and 'mention everyone' perms (useful if you wanna double check to make sure you didn't give anyone mention everyone perms that shouldn't have it)

**Usage:**

```
ListRoles
```

```
[-nomanaged Don't list managed/bot roles:Switch]
```

### Logs

**Aliases:** log

Creates a log of the last messages in the current channel. This includes deleted messages within an hour (or 12 hours for premium servers)

**Usage:**

```
Logs [Count:Whole number]
```

### Nicknames

**Aliases:** nn

Shows past nicknames of a user. Only shows up to the last 25 nicknames.

**Usage:**

```
Nicknames [User:User]
```

### Ping

Shows the latency from the bot to the discord servers. Note that high latencies can be the fault of ratelimits and the bot itself, it's not a absolute metric.

**Usage:**

```
Ping
```

### Poll

Create very simple reaction poll. Example: `poll "favorite color?" blue red pink`

**Usage:**

```
Poll <Topic:Text - Description of the poll> <Option1:Text> <Option2:Text> [Option3:Text] [Option4:Text] [Option5:Text] [Option6:Text] [Option7:Text] [Option8:Text] [Option9:Text] [Option10:Text]
```

### Prefix

Shows command prefix of the current server, or the specified server

**Usage:**

```
Prefix [Server ID:Whole number]
```

### Reminders

Lists your active reminders

**Usage:**

```
Reminders
```

### Remindme

**Aliases:** remind/reminder

Schedules a reminder, example: 'remindme 1h30min are you alive still?'

**Usage:**

```
Remindme <Time:Duration> <Message:Text>
```

### ResetPastNames

Reset your past usernames/nicknames.

**Usage:**

```
ResetPastNames
```

### Role

Toggle a role on yourself or list all available roles, they have to be set up in the control panel first, under 'rolecommands'

**Usage:**

```
Role [Role:Text]
```

### Settimezone

**Aliases:** setz/tzset

Sets your timezone, used for various purposes such as auto conversion. Give it your country.

**Usage:**

```
Settimezone [Timezone:Text]
```

```
[-u Display current:Switch]
[-d Delete TZ record:Switch]
```

### Stats&#x20;

Shows server stats (if public stats are enabled). This command is only available if collecting statistics is enabled bot not user side. Disabled for YAGPDB.

**Usage:**

```
Stats
```

### ToggleTimeConversion

**Aliases:** toggletconv/ttc

Toggles automatic time conversion for people with registered timezones (setz) in this channel, its on by default, toggle all channels by giving it `all`

**Usage:**

```
ToggleTimeConversion [flags:Text]
```

### Undelete

**Aliases:** ud

&#x20;Views the first 10 recent deleted messages. By default, only the current user's deleted messages will show. You can use the `-a` flag to view all users delete messages, or `-u` to view a specified user's deleted messages. Both `-a` and `-u` require Manage Messages permission. Note: `-u` overrides `-a` meaning even though `-a` might've been specified along with `-u` only messages from the user provided using `-u` will be shown.

**Usage:**

```
Undelete
```

```
[-a a:Switch - from all users]
[-u u:Mention/ID - from a specific user]
[-channel channel:Channel - Optional target channel]
```

### Usernames

**Aliases:** unames/un

Shows past usernames of a user. Only shows up to the last 25 usernames.

**Usage:**

```
Usernames [User:User]
```

### ViewPerms

Shows you or the targets permissions in this channel

**Usage:**

```
ViewPerms [target:Mention/ID]
```

### Whois

**Aliases:** whoami

Shows information about a user

**Usage:**

```
Whois [User:Member]
```

## Fun 🎉

### Define

**Aliases:** df

Look up an urban dictionary definition, default paginated view.

**Usage:**

```
Define <Topic:Text>
```

```
[-raw raw:Switch - Raw output]
```

### Weather

**Aliases:** w

Shows the weather somewhere

**Usage:**

```
Weather <Where:Text>
```

### Topic

Generates a conversation topic to help chat get moving.

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

### DogFact

**Aliases:** dog/dogfacts

Dog Facts

**Usage:**

```
DogFact
```

### Advice

Don't be afraid to ask for advice!

**Usage:**

```
Advice [What:Text]
```

### Throw

Throwing things is cool.

**Usage:**

```
Throw [Target:User]
```

### Roll

Roll dices, specify nothing for 6 sides, specify a number for max sides, or rpg dice syntax. Example: `-roll 2d6`

**Usage:**

```
Roll <Sides:Whole number>
Roll <RPG Dice:Text>
Roll
```

### CustomEmbed

**Aliases:** ce

Creates an embed from what you give it in json form: [https://docs.yagpdb.xyz/others/custom-embeds](https://docs.yagpdb.xyz/others/custom-embeds) Example: `-ce {"title": "hello", "description": "wew"}`

**Usage:**

```
CustomEmbed <Json:Text>
```

### SimpleEmbed

**Aliases:** se

A more simpler version of CustomEmbed, controlled completely using switches.

**Usage:**

```
SimpleEmbed
```

```
[-channel :Channel - Optional channel to send in]
[-content :Text - Text content for the message]
[-title :Text]
[-desc :Text - Text in the 'description' field]
[-color :Text - Either hex code or name]
[-url :Text - Url of this embed]
[-thumbnail :Text - Url to a thumbnail]
[-image :Text - Url to an image]
[-author :Text - The text in the 'author' field]
[-authoricon :Text - Url to a icon for the 'author' field]
[-authorurl :Text - Url of the 'author' field]
[-footer :Text - Text content for the footer]
[-footericon :Text - Url to a icon for the 'footer' field]
```

### WouldYouRather

**Aliases:** wyr

Get presented with 2 options.

**Usage:**

```
WouldYouRather
```

### Xkcd

An xkcd comic, by default returns random comic strip

**Usage:**

```
Xkcd [Comic number:Whole number]
```

```
[-l Latest comic:Switch]
```

### Howlongtobeat

**Aliases:** hltb

Game information based on query from howlongtobeat.com. Results are sorted by popularity, it's their default. Without -p returns the first result. Switch -p gives paginated output using Levenshtein distance sorting max 20 results.

**Usage:**

```
HowLongToBeat <Game-Title:Text>
```

```
[-c c:Switch - Compact output]
[-p p:Switch - Paginated output]
```

### TopServers

Responds with the top 15 servers I'm on

**Usage:**

```
TopServers [Skip:Whole number - Entries to skip]
```

```
[-id serverID:Whole number]
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
Rep [User:User]c
```

### TopRep

Shows top 15 rep on the server

**Usage:**

```
TopRep [Offset:Whole number]
```

### Sentiment

**Aliases:** sent

Does sentiment analysis on a message or your last 5 messages longer than 3 words

**Usage:**

```
Sentiment [text:Text]
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

### SoundboardReset

**Aliases:** sbclose/sbreset

Reset Soundboard Player

**Usage:**

```
SoundboardReset
```

### cah Create

**Aliases:** c

Creates a Cards Against Humanity game in this channel, add packs after commands, or \* for all packs. (-v for vote mode without a card czar).

**Usage:**

```
Create [packs:Text - Packs seperated by space, or * for all of them.]
```

```
[-v Vote mode - players vote instead of having a card czar.:Switch]
```

### cah End

Ends a Cards Against Humanity game that is ongoing in this channel.

**Usage:**

```
End
```

### cah Kick

Kicks a player from the ongoing Cards Against Humanity game in this channel.

**Usage:**

```
Kick <user:Mention/ID>
```

### cah Packs

Lists all available packs.

**Usage:**

```
Packs
```

## Debug & Maintenance 🖥

### Allocstat

Memory statistics.

**Usage:**

```
allocstat
```

### Banserver

;))

**Usage:**

```
banserver <server:Whole number>
```

### Ccreqs

Returns the number of concurrent requests currently going on

**Usage:**

```
ccreqs
```

### Createinvite

Maintenance command, creates a invite for the specified server

**Usage:**

```
createinvite <server:Whole number>
```

### CurrentShard

**Aliases:** cshard

Shows the current shard this server is on (or the one specified

**Usage:**

```
CurrentShard [serverid:Whole number]
```

### Dcallvoice

Disconnects from all the voice channels the bot is in

**Usage:**

```
dcallvoice
```

### Findserver

**Aliases:** findservers

Looks for a server by server name or the servers a user owns

**Usage:**

```
findserver
```

```
[-name name:Text]
[-user user:Mention/ID]
```

### Generatepremiumcode

**Aliases:** gpc

Generates premium codes

**Usage:**

```
generatepremiumcode <Duration:Duration> <NumCodes:Whole number> <Message:Text>
```

### Globalrl

Tests the global ratelimit functionality

**Usage:**

```
globalrl
```

### IsGuildUnavailable

Returns wether the specified guild is unavilable or not

**Usage:**

```
IsGuildUnavailable <guildid:Whole number>
```

### Leaveserver

;))

**Usage:**

```
leaveserver <server:Whole number>
```

### Memstats

;))

**Usage:**

```
memstats
```

### Roledbg

Debug debug debug autorole assignment

**Usage:**

```
Roledbg
```

### Setstatus

Sets the bot's status and streaming url

**Usage:**

```
setstatus [status:Text]
```

```
[-url url:Text]
```

### Sleep

Maintenance command, used to test command queueing

**Usage:**

```
sleep
```

### State Botmember/Guild/Member

Responds with state debug info

**Usage:**&#x20;

```
state botmember
state guild
state member
```

### Stateinfo

Responds with state debug info

**Usage:**

```
stateinfo
```

### Testreddit

Tests the reddit feeds in this server by checking the specified post

**Usage:**

```
testreddit <post-id:Text>
```

### Toggledbg

Toggles Debug Logging

**Usage:**

```
toggledbg
```

### Topcommands

Shows command usage stats

**Usage:**

```
topcommands [hours:Whole number]
```

### Topevents

Shows gateway event processing stats for all or one shard

**Usage:**

```
topevents [shard:Whole number]
```

### Topgames

Shows the top games on this server

**Usage:**

```
topgames
```

```
[-all all:Switch]
```

### Unbanserver

;))

**Usage:**

```
unbanserver <server:Text>
```

### Viewperms

Shows you or the targets permissions in this channel

**Usage:**

```
ViewPerms [target:Mention/ID]
```

### Yagstatus

**Aliases:** status

Shows yagpdb status, version, uptime, memory stats, and so on

**Usage:**

```
Yagstatus
```

## Moderation 👮

### Ban

**Aliases:** banid

Bans a member, specify a duration with -d and specify number of days of messages to delete with -ddays (0 to 7)

**Usage:**

```
Ban <User:Mention/ID> [Reason:Text]
```

```
[-d Duration:Duration]
[-ddays Days:Whole number]
```

### Unban

**Aliases:** unbanid

Unbans a user. Reason requirement is same as ban command setting.

**Usage:**

```
Unban <User:Mention/ID> [Reason:Text]
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

[Will not delete messages older than 2 weeks.](https://discord.com/developers/docs/resources/channel#bulk-delete-messages)\
\
Delete the last number of messages from chat, optionally filtering by user, max age and regex or ignoring pinned messages.\
**Warning:** Using `clean <userId> <amount>` does not work. This is because the user ID is interpreted as the amount. As it is over the limit of 100, it is treated as invalid. You can use `clean <amount> <userId>` instead or mention the user. Specify a regex with "-r regex\_here" and max age with "-ma 1h10m" You can invert the regex match (i.e. only clear messages that do not match the given regex) by supplying the `-im` flag.\
Note: Will only look in the last 1k messages

**Usage:**

```
Clean <Num:Whole number>
Clean <Num:Whole number> <User:User Mention>
Clean <User:User Mention> <Num:Whole number>
```

```
[-r r:Text - Regex]
[-im im:Switch - Invert regex match]
[-ma ma:Duration - Max age]
[-minage minage:Duration - Min age]
[-i i:Switch - Regex case insensitive]
[-nopin nopin:Switch - Ignore pinned messages]
[-a a:Switch - Only remove messages with attachments]
[-to to:Whole number - Stop at this msg ID]
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

**Aliases:** dw/delwarn/deletewarning

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

### TopWarnings

**Aliases:** topwarns

Shows ranked list of warnings on the server.

**Usage:**

```
TopWarnings [Page:Whole number]
```

```
[-id List UserIDs:Switch]
```

### GiveRole

**Aliases:** grole/arole/addrole

Gives a role to the specified member, with optional expiry

**Usage:**

```
GiveRole <User:Mention/ID> <Role:Text>
```

```
[-d Duration:Duration]
```

### TakeRole

**Aliases:** rrole/takearole/trole

Removes the specified role from the target

**Usage:**

```
RemoveRole <User:Mention/ID> <Role:Text>
```

### automod Rulesets

**Aliases:** r/list/l

Lists all rulesets and their status

**Usage:**

```
Rulesets
```

### automod Toggle

**Aliases:** t

Toggles a ruleset on/off

**Usage:**

```
Toggle <ruleset name:Text>
```

### automod Logs

**Aliases:** log

Shows the log of the last triggered automod rules, optionally filtering by user

**Usage:**

```
Logs [skip:Whole number]
```

```
[-user :Mention/ID]
```

### automod ListViolations

**Aliases:**  Violations/ViolationLogs/VLogs/VLog

Lists Violations of specified user /n old flag posts oldest violations in first page ( from oldest to newest ).

**Usage:**

```
ListViolations <User:Mention/ID> [Page Number:Whole number]
```

```
[-old Oldest First:Switch]
```

### automod ListViolationsCount

**Aliases:**  ViolationsCount/VCount

Lists Violations summary in entire server or of specified user optionally filtered by max violation age. Specify number of violations to skip while fetching using -skip flag ; max entries fetched 500.

**Usage:**

```
ListViolationsCount [User:Mention/ID]
```

```
[-ma Max Violation Age:Duration]
[-skip Amount Skipped:Whole number]
```

### automod DeleteViolation

**Aliases:**  DelViolation/DelV/DV

Deletes a Violation with the specified ID. ID is the first number of each Violation in the ListViolations command.

**Usage:**

```
DeleteViolation <ID:Whole number>
```

### automod ClearViolations

**Aliases:**  ClearV/ClrViolations/ClrV

Clears Violations of specified user optionally filtered by Name, Min/Max age and other conditions. By default, more recent violations are preferentially cleared.

**Usage:**

```
ClearViolations <User:Mention/ID> [Violation Name:Text]
```

```
[-ma Max Violation Age:Duration]
[-mina Min Violation Age:Duration]
[-num Max Violations Cleared:Whole number]
[-old Preferentially Clear Older Violations:Switch]
[-skip Amount Skipped:Whole number]
```

## Rolemenu 🔘

alias: `rmenu`

### RoleMenu Create

**Aliases:** c

Set up a role menu. Specify a message with -m to use an existing message instead of having the bot make one

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

### RoleMenu EditOption

**Aliases:** edit

Allows you to reassign the emoji of an option, tip: use ResetReactions afterwards.

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.

**Usage:**

```
EditOption <Message ID:Whole number>
```

### RoleMenu Listgroups

**Aliases:** list/groups

Lists all role groups.

**Usage:**

```
Listgroups
```

### RoleMenu Remove

Removes a rolemenu from a message. The message won't be deleted and the bot will not do anything with reactions on that message

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.

**Usage:**

```
Remove <Message ID:Whole number>
```

### RoleMenu ResetReactions

**Aliases:** reset

Removes all reactions on the specified menu message and re-adds them. Can be used to fix the order after updating it.

To get the id of a message you have to turn on developer mode in discord's appearances settings then right click the message and copy id.

**Usage:**

```
ResetReactions <Message ID:Whole number>
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

## Tickets 🎫

alias: `ticket`

### Tickets Open

**Aliases:** create/new/make

Opens a new ticket

**Usage:**

```
Open <subject:Text>
```

### Tickets AddUser

Adds a user to the ticket in this channel

**Usage:**

```
AddUser <target:Member>
```

### Tickets RemoveUser

Removes a user from the ticket

**Usage:**

```
RemoveUser <target:Member>
```

### Tickets Rename

Renames the ticket

**Usage:**

```
Rename <new-name:Text>
```

### Tickets Close

**Aliases:** end/delete

Closes the ticket

**Usage:**

```
Close [reason:Text]
```

### Tickets AdminsOnly

**Aliases:** adminonly/ao

Toggle admins only mode for this ticket

**Usage:**

```
AdminsOnly
```

## Events 🎟

alias: `event`

### Events Create

**Aliases:** new/make

Creates an event, You will be led through an interactive setup

**Usage:**

```
Create
```

### Events Edit

Edits an event

**Usage:**

```
Edit <ID:Whole number>
```

```
[-title :Text - Change the title of the event]
[-time :Text - Change the start time of the event]
[-max :Whole number - Change max participants]
```

### Events List

**Aliases:** ls

Lists all events in this server

**Usage:**

```
List 
```

### Events Delete

**Aliases:** rm/del

Deletes an event, specify the event ID of the event you wanna delete

**Usage:**

```
Delete <ID:Whole number>
```

### Events StopSetup

**Aliases:** cancelsetup

Force cancels the current setup session in this channel

**Usage:**

```
StopSetup
```
