# Templates

{% hint style="warning" %}
Put curly brackets around the templates like this: `{{.User.Username}}`
{% endhint %}

{% hint style="info" %}
If you want to put a template inside a template \(e.g. to wrap toString in joinStr around .Guild.MemberCount\), you use normal braces:  
`{{joinStr "" "Our member count is " (toString .Guild.MemberCount) "!"}}`
{% endhint %}

## Available template data:

### User

| Field | Description |
| :--- | :--- |
| .User | The user's username together with discriminator. |
| .User.String | The user's username together with discriminator as string-type. |
| .User.Username | The user's username. |
| .User.ID | The user's ID. |
| .User.Discriminator | The user's discriminator \(The four digits in a person's username\). |
| .User.Avatar | The user's avatar ID. |
| .User.AvatarURL "256" | Gives the URL for user's avatar, argument "256" is the size of the picture  and can increase/decrease twofold \(e.g. 512, 1024 or 128, 64 etc.\). |
| .User.Bot | Determines whether the target user is a bot - if yes, it will return True. |
| .User.Mention | Mentions user. |
| .RealUsername | Only works with join and leave messages. This can be used to send the real username to a staff channel when invites are censored. |
| .UsernameHasInvite | Only works with join and leave messages. It will determine does the username contain an invite link. |

### Guild / Server

| Field | Description |
| :--- | :--- |
| .Guild.ID | Outputs the ID of the guild. |
| .Guild.Name | Outputs the name of the guild. |
| .Guild.Icon | Outputs the ID of the guild's icon. |
| .Guild.Region | Outputs the region of the guild. |
| .Guild.AfkChannelID | Outputs the AFK channel ID. |
| .Guild.OwnerID | Outputs the ID of the owner. |
| .Guild.JoinedAt | Outputs when YAGPDB joined the guild. |
| .Guild.AfkTimeout | Outputs the time when a user gets moved into the AFK channel while not being active. |
| .Guild.MemberCount | Outputs the number of users on a guild. |
| .Guild.VerificationLevel | Outputs the required verification level for the guild. |
| .Guild.EmbedEnabled | Outputs whether embeds are enabled or not, true / false. |

### Member

| Field | Description |
| :--- | :--- |
| .Member.Nick | The nickname for this member. |
| .Member.Roles | A list of role IDs that the member has. |

### Channel

| Field | Description |
| :--- | :--- |
| .Channel.Name | The Name of the channel. |
| .Channel.ID | The ID of the channel. |
| .Channel.Topic | The Topic of the channel. |
| .Channel.NSFW | Outputs whether this channel is NSFW or not. |

### Message

| Field | Description |
| :--- | :--- |
| .Message.ID | ID of the message |
| .Message.ChannelID | Channel id this message is in |
| .Message.Author | Author of the message \(User object\) |
| .Message.Timestamp | Timestamp of the message \(use .Message.Timestamp.Parse for a time object, otherwise string\) |
| .Message.Attachments | Attachments to this message \(slice of attachment objects\) |
| .Message.Embeds | Embeds on this message \(slice of embed objects\) |
| .Message.Mentions | Users this message mentions |
| .Message.Reactions | Reactions on this message \(only available form getMessage\) |
| .Message.Content | Text content on this message |

{% hint style="info" %}
More information about the `Message` template can be found [here](../commands/custom-commands.md#the-message-template).
{% endhint %}

### Current User

| Function | Description |
| :--- | :--- |
| currentUserCreated |  The time the current user was created. |
| currentUserAgeHuman |  The account age of the current user in more human readable format  \(`3 days 2 hours`, for example\). |
| currentUserAgeMinutes |  The account age of the current user in minutes. |

### Functions

| Function | Description |
| :--- | :--- |
| `adjective` | Returns a random adjective. |
| `dict key1 value1 key2 value2 etc` | Creates a dictionary \(not many use cases yet\). |
| `sdict "key1" "value1" "key2" "value2"` |  The same as `dict` but with only string keys and can be used in `cembed`. |
| `cslice value1 value2` | Creates a slice \(similar to array\) that can be used elsewhere \(`cembed` and `sdict` for example\). |
| `cembed "list of embed values"` | Function to generate embed inside custom command. [More in-depth here](../others/custom-embeds.md#embeds-in-custom-commands). |
| `in list value` | Returns true if value is in list. |
| `inFold`  | Same as `in`, but is case insensitive. |
| `add x y` | Returns x + y. |
| `seq start stop` | Creates a new array of integer, starting from start and ending at stop. |
| `shuffle list` | Returns a shuffled version of a list. |
| `joinStr seperator str1 str2` | Joins several strings into one, separated by the first arg \(the separator\), useful for executing commands in templates \(e.g.`{{joinStr "" "1" "2" "3"}}` = `123`\). |
| `randInt (stop, or start stop)` | Returns a random integer between 0 and stop, or start - stop if two args are provided. |
| `toString` | Converts something into a string. Usage: `(toString x)`. |
| `toInt` | Converts something into an integer. Usage: `(toInt x)`. |
| `toInt64` | Converts something into an int64. Usage: `(toInt64 x)`. |
| `sendDM "message here"` | Sends the user a direct message, only one DM can be sent per template \(accepts embed objects\). |
| `sendMessage channel message` | Sends `message (string or embed)` in `channel`, channel can be either `nil`, the channel ID or the channel's name. |
| `sendMessageNoEscape channel message` | Sends `message (string or embed)` in `channel`, channel can be either `nil`, the channel ID or the channel name. Doesn't escape mentions \(e.g. role mentions or @here/@everyone\). |
| `sendMessageRetID channel message` | Same as `sendMessage`, but also returns messageID for later use. Example in [Snippets](templates.md#snippets). |
| `sendMessageNoEscapeRetID channel message` | Same as `sendMessageNoEscape`, but also returns messageID for later use. |
| `addMessageReactions channel messageID reactions` | Same as `addReactions` or `addResponseReactions`, but can be used on any messages using its ID. Channel can be either `nil`, channelID or channel's name. Example in [Snippets](templates.md#snippets). |
| `deleteMessage channel messageID (delay)` | Deletes message with given `messageID` from `channel`. Channel can be either `nil`, channelID or channel's name. `(Delay)` is optional and defaults to 10 seconds. Example in [Snippets](templates.md#snippets). |
| `mentionEveryone` | Mentions @everyone. |
| `escapeEveryone "input"` | Escapes everyone mentions in a string. |
| `mentionHere` | Mentions @here. |
| `escapeHere "input"` | Escapes here mentions in a string. |
| `escapeEveryoneHere "input"` | Escapes everyone and here mentions in a string. Useful with sendMessageNoEscape, also applies to escapeEveryone/Here. Example in [Snippets](templates.md#snippets). |
| `mentionRoleName "rolename"` | Mentions the first role found with the provided name \(case-insensitive\). |
| `mentionRoleID roleID` | Mentions the role found with the provided ID. |
| `hasRoleName "rolename"` | Returns true if the user has the role with the specified name \(case-insensitive\). |
| `hasRoleID roleID` | Returns true if the user has the role with the specified ID \(use the listroles command for a list of roles\). |
| `targetHasRoleName userID "rolename"` | Returns true if the given user has the role with the specified name \(case-insensitive\). |
| `targetHasRoleID userID roleID` | Returns true if the given user has the role with the specified ID \(use the listroles command for a list of roles\). Example in [Snippets](templates.md#snippets). |
| `addRoleID roleID` | Adds the role with the given ID to the user that triggered the command \(use the listroles command for a list of roles\). |
| `removeRoleID roleID` | Removes the role with the given ID from the user that triggered the command \(use the listroles command for a list of roles\). |
| `giveRoleName userID "rolename"` | Gives a role by name to the target. |
| `giveRoleID userID roleID` | Gives a role by ID to the target. |
| `takeRoleName userID "rolename"` | Takes away a role by name from the target. |
| `takeRoleID userID "roleID"` | Takes away a role by ID from the target. |
| `deleteResponse time` | Deletes the response after a certain time \(1-60 seconds\). |
| `deleteTrigger time` | Deletes the trigger after a certain time \(1-60 seconds\). |
| `addReactions "👍" "👎"` | Adds each emoji as a reaction to the message that triggered the command \(recognizes Unicode emojis and `emojiname:emojiid`\). |
| `addResponseReactions "👍" "👎"` | Adds each emoji as a reaction to the response message \(recognizes Unicode emojis and `emojiname:emojiid`\). |
| `exec "command" "args" "args" "args"` | Execute a YAGPDB \(e.g. reverse, roll, kick etc\) in a custom command. Exec can be run max 5 times per command.  |
| `execAdmin "command" "args" "args" "args" etc` | Function the same as exec but will override any permission requirement \(such as the kick permission to use kick command etc.\). |
| `userArg ########` | Function that can be used to retrieve a user from a mention string or ID. |
|  `currentTime` | Gets the current time which can be used in a custom embed. |
| `.CmdArgs` | Gets all the arguments passed to the command. |
| `slice "string" integer (integer2)` | Outputs the "string" after cutting/slicing off integer \(numeric\) value of symbols \(actually starting the string's index from integer through integer2\) - e.g. `{{slice "Fox runs" 2}}`outputs `x runs`. When using also integer2 - e.g. `{{slice "Fox runs" 1 7 }}`, it outputs `ox run`. For slicing whole words, see example below in [Snippets](templates.md#how-to-get-ids).  |
| `lower "string"` | Converts the string to lowercase. |
| `upper "string"` | Converts the string to uppercase. |
| `title "string"` | Returns string with the first letter of each word capitalized. |
| `parseArgs required_args error_message ...carg` | Checks the arguments for a specific type. [More in depth here](../commands/custom-commands.md#require-arguments) and an example in [Custom Command Examples.](custom-command-examples.md#parseargs-example) |
| `carg type name` | Defines type of argument for parseArgs. [More in depth](../commands/custom-commands.md#require-arguments) here and an example in [Custom Command Examples.](custom-command-examples.md#parseargs-example) |
| `getMessage channelID messageID` | Returns a [Message ](templates.md#message)object |

### Branching

| Case | Example |
| :--- | :--- |
| Basic if |  `{{if (condition)}} {{end}}` |
| Not |  `{{if not (condition)}} {{end}}` |
| And |  `{{if and (cond1) (cond2) (cond3)}}` |
| Or |  `{{if or (cond1) (cond2) (cond3)}} {{end}}` |
| Equals |  `{{if eq .Channel.ID ########}} {{end}}` |
| Not equals |  `{{if ne .Channel.ID #######}} {{end}}` |
| Less than |  `{{if lt (len .Args) 5}} {{end}}` |
| Greater than |  `{{if gt (len .Args) 1}} {{end}}` |
| Else if |  `{{if (case statement)}} {{else if (case statement)}} {{end}}` |
| Else |  `{{if (case statement)}} {{else}} output here {{end}}` |

### Snippets

* `<@{{.User.ID}}>` Outputs a mention to the user that called the command.
* `<@###########>` Mentions the user that has the ID \#\#\#\#\#\# \(See [How to get IDs](templates.md#how-to-get-ids) to get ID\).
* `<#&&&&&&&&&&&>` Mentions the channel that has ID &&&&&& \(See [How to get IDs](templates.md#how-to-get-ids) to get ID\).
* `{{if hasRoleName "funrole"}} Has role funrole {{end}}`This will only show if the member has a role with name "funrole" .
* `{{if gt (len .Args) 0}} {{index .Args 1}} {{end}}` Assuming your trigger is a command, will display your first input if input was given.
* `{{if eq .Channel.ID #######}}` Will only show in Channel \#\#\#\#\#.
* `{{if ne .User.ID #######}}` Will ignore if user ID \#\#\#\#\# uses command.
* `{{$d := randInt 10}}` Store the random int into variable $d \(A random number from 0-9\).
* `{{addReactions .CmdArgs}}` Adds the emoji following a trigger as reactions.
* `{{$a := (exec "catfact")}}` Saves the response of the `catfact` ****command to variable `$a`. 
* `{{$allArgs := (joinStr " " .CmdArgs)}}` Saves all the argument to a variable `$allArgs`. 
* `{{$args:= (joinStr " " (slice .CmdArgs 1))}}` Saves all the arguments except the first one to a variable `$args`. 
* `{{/* this is a comment */}}`For commenting something inside a template, use this syntax.
* `{{ $x := sendMessageRetID nil "Hello there!" }} {{ addMessageReactions nil $x "👍" "👎" }} {{ deleteMessage nil $x 5 }}` Sends message to current channel `nil` and gets messageID to variable `$x`. Also adds reactions to this message. After 5 seconds, deletes that message.
* To demonstrate usage of escapeEveryoneHere &gt; `{{ $x := "@here Hello World! @everyone" }} {{ sendMessage nil $x }} {{ sendMessageNoEscape nil $x }} {{ sendMessageNoEscape nil ( escapeEveryoneHere $x ) }}`
* To demonstrate usage of targetHasRoleID &gt;  `{{ $x := ( userArg ( index .Args 1) ).ID }} {{ if targetHasRoleID $x ############ }} Has the Role! {{ else }} Does not have the role! {{ end }}`

## How to get IDs <a id="how-to-get-ids"></a>

**User IDs:** Can be found by mentioning the user then adding a \ such as `\@jonas747#0001` . Alternatively if you have developer mode on, you can right click and select Copy ID

**Channel IDs:** Can be found by mentioning the channel then adding a \ such as `\#announcements`. Alternatively if you have developer mode on, you can right click on the channel and select Copy ID.

**Role IDs**: Use the `listroles`command.

**Emote IDs:** 

If it is a **custom emote**, adding a \ in front of the emote such as `\:yag:` will display the name along with the ID such as  `<:yag:277569741932068864>`.

If it is an **animated emote**, do the same steps as a normal emote. If you do not have Discord Nitro, you can have a friend or a bot use the emote and right click on the emote to open its link. The ID will be a part of the URL.

If it is a **default emote**, look up the Unicode for the emote on Google. Note that some of the more customized default emotes such as some of the family emotes will not work in any of the YAGPDB commands. 

