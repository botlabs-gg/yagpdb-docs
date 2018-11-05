# All commands

## General ℹ️

### Help

**Aliases:** commands/h/how/command

Help [command:Text]



Shows help about all or one specific command


### Info

**Aliases:**

Info



Responds with bot information


### Invite

**Aliases:**

Invite



Responds with bot invite link


## Tools & Utilities 🔨

### Prefix

**Aliases:**

Prefix [Server ID:Whole number]



Shows command prefix of the current server, or the specified server


### Calc

**Aliases:** c/calculate

Calc <Expression:Text>



Calculator 2+2=5


### Ping

**Aliases:**

Ping



I prefer tabletennis (Shows the bots ping to the discord servers)


### CurrentTime

**Aliases:** ctime/gettime

CurrentTime <Offset:Whole number>
CurrentTime <Zone:Text>
CurrentTime




Shows current time in different timezones. [Available timezones](https://pastebin.com/ZqSPUhc7)


### MentionRole

**Aliases:** mrole

MentionRole <Role:Text> [Message:Text]



Sets a role to mentionable, mentions the role, and then sets it back
Requires the manage roles permission and the bot being above the mentioned role

### ListRoles

**Aliases:**

ListRoles



List roles and their id's, and some other stuff on the server


### Poll

**Aliases:**

Poll <Topic:Text - Description of the poll> <Option1:Text> <Option2:Text> [Option3:Text] [Option4:Text] [Option5:Text] [Option6:Text] [Option7:Text] [Option8:Text] [Option9:Text] [Option10:Text]



Create a reaction poll.


### Undelete

**Aliases:** ud

Undelete

[-a all:Switch]


Views your recent deleted messages, or all users deleted messages (with "-a" and manage messages perm) in this channel


### ViewPerms

**Aliases:**

ViewPerms [target:Mention/ID]



Shows you or the targets permissions in this channel


### Stats

**Aliases:**

Stats



Shows server stats (if public stats are enabled)


### CustomCommands

**Aliases:** cc

CustomCommands <ID:Whole number>
CustomCommands <Trigger:Text>
CustomCommands




Shows a custom command specified by id or trigger, or lists them all


### Logs

**Aliases:** log

Logs [Count:Whole number]



Creates a log of the last messages in the current channel
This includes deleted messages within an hour

### Whois

**Aliases:** whoami

Whois [User:User]



shows information about a user


### Nicknames

**Aliases:** nn

Nicknames [User:User]



Shows past nicknames of a user


### Usernames

**Aliases:** unames/un

Usernames [User:User]



Shows past usernames of a user


### Remindme

**Aliases:** remind

Remindme <Time:Duration> <Message:Text>



Schedules a reminder, example: 'remindme 1h30min are you alive still?'


### Reminders

**Aliases:**

Reminders



Lists your active reminders


### CReminders

**Aliases:**

CReminders



Lists reminders in channel, only users with 'manage server' permissions can use this.


### Delreminder

**Aliases:** rmreminder

Delreminder <ID:Whole number>



Deletes a reminder.


### Role

**Aliases:**

Role [Role:Text]



Give yourself a role or list all available roles


## Fun 🎉

### Define

**Aliases:** df

Define <Topic:Text>



Look up an urban dictionary definition


### Weather

**Aliases:** w

Weather <Where:Text>



Shows the weather somewhere (add ?m for metric: -w bergen?m)


### Topic

**Aliases:**

Topic



Generates a chat topic


### CatFact

**Aliases:** cf/cat/catfacts

CatFact



Cat Facts


### Advice

**Aliases:**

Advice [What:Text]



Get advice


### Throw

**Aliases:**

Throw [Target:User]



Cause you are a rebel


### Roll

**Aliases:**

Roll <Sides:Whole number>
Roll <RPG Dice:Text>
Roll




Roll dices, specify nothing for 6 sides, specify a number for max sides, or rpg dice syntax


### CustomEmbed

**Aliases:** ce

CustomEmbed <Json:Text>



Creates an embed from what you give it in json form: https://discordapp.com/developers/docs/resources/channel#embed-object


### WouldYouRather

**Aliases:** wyr

WouldYouRather



Get presented with 2 options.


### TopServers

**Aliases:**

TopServers [Skip:Whole number - Entries to skip]



Responds with the top 15 servers I'm on


### TakeRep

**Aliases:** -/tr/trep/-rep

TakeRep <User:User> [Num:Whole number]



Takes away rep from someone


### GiveRep

**Aliases:** +/gr/grep/+rep

GiveRep <User:User> [Num:Whole number]



Gives rep to someone


### SetRep

**Aliases:** SetRepID

SetRep <User:Mention/ID> <Num:Whole number>



Sets someones rep, this is an admin command and bypasses cooldowns and other restrictions.


### DelRep

**Aliases:**

DelRep <User:Mention/ID>



Deletes someone from the reputation list completely, this cannot be undone.


### RepLog

**Aliases:** replogs

RepLog <User:Mention/ID> [Page:Whole number]



Shows the rep log for the specified user.


### Rep

**Aliases:**

Rep [User:User]



Shows yours or the specified users current rep and rank


### TopRep

**Aliases:**

TopRep [Offset:Whole number]



Shows top 15 rep on the server


### sentiment

**Aliases:** sent

sentiment [text:Text]



Does sentiment analysys on a message or your last 5 messages longer than 3 words


### 8Ball

**Aliases:**

8Ball <What to ask:Text>



Wisdom


### Soundboard

**Aliases:** sb

Soundboard [Name:Text]



Play, or list soundboard sounds


### cah create

**Aliases:** c

create [packs:Text - Packs seperated by space, or * for all of them]

[-v Vote mode, players vote instead of having a cardczar:Switch]


Creates a cards against humanity game in this channel, add packs after commands, or * for all packs. (-v for vote mode without a card czar)


### cah end

**Aliases:**

end



Ends a cards against humanity game thats ongoing in this channel


### cah kick

**Aliases:**

kick <user:Mention/ID>



Kicks a player from the ongoing cards against humanity game in this channel


### cah packs

**Aliases:**

packs



Lists available packs


## Debug & Maintenance 🖥

### CurrentShard

**Aliases:** cshard

CurrentShard [serverid:Whole number]



Shows the current shard this server is on (or the one specified


### MemberFetcher

**Aliases:** memfetch

MemberFetcher



Shows the current status of the member fetcher


### Yagstatus

**Aliases:** status

Yagstatus



Shows yagpdb status, version, uptime, memory stats, and so on


### roledbg

**Aliases:**

roledbg



Debug debug debug autorole assignment


## Moderation 👮

### Ban

**Aliases:** banid

Ban <User:Mention/ID> [Reason:Text]

[-d Duration:Duration]


Bans a member, specify a duration with -d


### Kick

**Aliases:**

Kick <User:Mention/ID> [Reason:Text]



Kicks a member


### Mute

**Aliases:**

Mute <User:User Mention> <Duration:Duration> <Reason:Text>
Mute <User:User Mention> <Reason:Text> <Duration:Duration>
Mute <User:User Mention> <Duration:Duration>
Mute <User:User Mention> <Reason:Text>
Mute <User:User Mention>




Mutes a member


### Unmute

**Aliases:**

Unmute <User:User Mention> [Reason:Text]



Unmutes a member


### Report

**Aliases:**

Report <User:Mention/ID> <Reason:Text>



Reports a member to the server's staff


### Clean

**Aliases:** clear/cl

Clean <Num:Whole number>
Clean <Num:Whole number> <User:User Mention>
Clean <User:User Mention> <Num:Whole number>


[-r Regex:Text]
[-ma Max age:Duration]
[-i Regex case insensitive:Switch]


Delete the last number of messages from chat, optionally filtering by user, max age and regex.
Specify a regex with "-r regex_here" and max age with "-ma 1h10m"
Note: Will only look in the last 1k messages

### Reason

**Aliases:**

Reason <ID:Whole number> <Reason:Text>



Add/Edit a modlog reason


### Warn

**Aliases:**

Warn <User:User Mention> <Reason:Text>



Warns a user, warnings are saved using the bot. Use -warnings to view them.


### Warnings

**Aliases:** Warns

Warnings <User:Mention/ID>



Lists warning of a user.


### EditWarning

**Aliases:**

EditWarning <Id:Whole number> <NewMessage:Text>



Edit a warning, id is the first number of each warning from the warnings command


### DelWarning

**Aliases:** dw

DelWarning <Id:Whole number>



Deletes a warning, id is the first number of each warning from the warnings command


### ClearWarnings

**Aliases:** clw

ClearWarnings <User:Mention/ID>



Clears the warnings of a user


### automod toggle

**Aliases:** t

toggle <ruleset name:Text>



Toggles a ruleset on/off


## Rolemenu 🔘

### RoleMenu Create

**Aliases:** c

Create <Group:Text>

[-m Message ID:Whole number]
[-nodm Disable DM:Switch]
[-rr Remove role on reaction removed:Switch]
[-skip Number of roles to skip:Whole number]


Set up a role menu, specify a message with -m to use an existing message instead of having the bot make one


### RoleMenu Remove

**Aliases:**

Remove <Message ID:Whole number>



Removes a rolemenu from a message, the message wont be deleted but the bot will now not do anything with reactions on that message


### RoleMenu Update

**Aliases:** u

Update <Message ID:Whole number>

[-nodm Disable DM:Switch]
[-rr Remove role on reaction removed:Switch]


Updates a rolemenu, toggling the provided flags and adding missing options, aswell as updating the order.


### RoleMenu ResetReactions

**Aliases:** reset

ResetReactions <Message ID:Whole number>



Removes all reactions on this menu and re-adds them, can be used to fix the order


### RoleMenu EditOption

**Aliases:** edit

EditOption <Message ID:Whole number>



Allows you to reassign the emoji of an option, tip: use ResetReactions afterwards
