# Templates

Available data which can be used in YAGPDB's templating "engine" which is slightly modified version of Golang's stdlib text/template package; more in depth here &gt; [https://golang.org/pkg/text/template/](https://golang.org/pkg/text/template/)

{% hint style="warning" %}
Put curly brackets around the templates like this: `{{.User.Username}}`
{% endhint %}

{% hint style="info" %}
If you want to put a template inside a template \(e.g. to wrap toString in joinStr around .Guild.MemberCount\), you use normal braces:  
`{{joinStr "" "Our member count is " (toString .Guild.MemberCount) "!"}}`
{% endhint %}

{% hint style="success" %}
"Go is all about type." Many problems start with different kinds of type the user has as values and what is needed for arguments. YAGPDB usually states that in error message - what went wrong with type.
{% endhint %}

## User

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

## Guild / Server

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

## Member

| Field | Description |
| :--- | :--- |
| .Member.JoinedAt | When member joined the guild/server. |
| .Member.Nick | The nickname for this member. |
| .Member.Roles | A list of role IDs that the member has. |

## Channel

| Field | Description |
| :--- | :--- |
| .Channel.Name | The Name of the channel. |
| .Channel.ID | The ID of the channel. |
| .Channel.Topic | The Topic of the channel. |
| .Channel.NSFW | Outputs whether this channel is NSFW or not. |

## Message

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
| .Args | List of everything that is passed to .Message.Content. |
| .Cmd | Agument that triggers custom command. |
| .CmdArgs | List of all the arguments passed after .Cmd. |

{% hint style="info" %}
More information about the `Message` template can be found [here](../commands/custom-commands.md#the-message-template).
{% endhint %}

## Current User

| Function | Description |
| :--- | :--- |
| currentUserCreated |  Returns value of type time and shows when the current user was created. |
| currentUserAgeHuman |  The account age of the current user in more human readable format  \(`3 days 2 hours`, for example\). |
| currentUserAgeMinutes |  The account age of the current user in minutes. |

## Time

Time in general uses Golang's time package library &gt; [https://golang.org/pkg/time/\#time](https://golang.org/pkg/time/#Time) and also this although slightly different syntax all applies here &gt; [https://gobyexample.com/time](https://gobyexample.com/time).

| Function | Description |
| :--- | :--- |
| `currentTime` | Gets the current time, value is of type time; which can be used in a custom embed. More info [here](../commands/custom-commands.md#currenttime-template). |
| `formatTime Time "arg"` | Outputs given time in RFC822 formatting, first argument `Time` shows it needs to be of type time, also with extra layout if second argument is given - e.g. `{{ formatTime currentUserCreated "3:04PM" }}` would output `11:22AM` if that would have been user's creating time. |
| `humanizeDurationHours` | Returns `nanoseconds` argument of type int64 in human readable format - as how long it would take to get towards given time - e.g. `{{ humanizeDurationHours 9000000000000000000 }}` returns `285 years 20 weeks 6 days and 16 hours`. |
| `humanizeDurationMinutes` | Sames as `humanizeDurationHours`, this time duration is given in minutes - e.g. `{{ humanizeDurationMinutes 3500000000000 }}` would return `58 minutes`. |
| `humanizeDurationSeconds` | Sames as both humanize functions above, this time duration is given in seconds - e.g. `{{ humanizeDurationSeconds 3500000000000 }}` would return `58 minutes and 20 seconds`. |
| `humanizeTimeSinceDays` | Returns time has passed since given argument of type Time in human readable format - e.g. `{{ humanizeTimeSinceDays currentUserCreated }}` |
| `.TimeHour` | Variable of time.Duration type and returns 1 hour &gt; `1h0m0s`. |
| `.TimeMinute` | Variable of time.Duration type and returns 1 minute &gt; `1m0s`. |
| `.TimeSecond` | Variable of time.Duration type and returns 1 second &gt; `1s`. |

## Functions

### Type conversion

| Function | Description |
| :--- | :--- |
| `toString` | Converts something into a string. Usage: `(toString x)`. |
| `toInt` | Converts something into an integer. Usage: `(toInt x)`. |
| `toInt64` | Converts something into an int64. Usage: `(toInt64 x)`. |
| `toFloat` | Converts argument \(numbers of strings\) to type float64. |
| `json value` | Traverses given `value` through MarshalJSON \([more here](%20https://golang.org/pkg/encoding/json/#Marshal)\) and returns it as type string. For example `{{ json .TimeHour }}` outputs type string; before this `.TimeHour` was of type time.Duration. Basically it's good to use if multistep type conversion is needed `( toString ( toInt value ) )` and certain parts of `cembed` need this for example. |

### String manipulation

| Function | Description |
| :--- | :--- |
| `joinStr "separator" "str1" (arg1)(arg2) "str2" ...` | Joins several strings into one, separated by the first arg`"separator"`, useful for executing commands in templates \(e.g.`{{joinStr "" "1" "2" "3"}}` returns `123`\). |
| `lower "string"` | Converts the string to lowercase. |
| `upper "string"` | Converts the string to uppercase. |
| `slice "string" integer (integer2)` | Outputs the "string" after cutting/slicing off integer \(numeric\) value of symbols \(actually starting the string's index from integer through integer2\) - e.g. `{{slice "Fox runs" 2}}`outputs `x runs`. When using also integer2 - e.g. `{{slice "Fox runs" 1 7 }}`, it outputs `ox run`. For slicing whole words, see example below in [Snippets](templates.md#how-to-get-ids).  |
| `urlescape "string"` | Escapes the string so it can be safely placed inside a URL path segment - e.g. "Hello, YAGPDB!" becomes "Hello%2C%20YAGPDB%21" |
| `split "string" "sepr"` | Slices given `"string"` to substrings separated by `"sepr"`arg and returns new slice/array of the substrings. Example below in [Snippets](templates.md#snippets). |
| `title "string"` | Returns string with the first letter of each word capitalized. |
| `reFind "regex" "string"` | Compares string to regex pattern and returns first match. `{{ reFind "AG" "YAGPDB is cool!" }}`returns `AG` \(regex pattern is case sensitive\). |
| `reFindAll "regex" "string"` | Adds all regex matches from the string to a slice. Example in [Snippets](templates.md#snippets). |
| `reReplace "regex" "string1" "string2"` | Replaces string1 contents with string2 at regex match point. `{{ reReplace "I am" "I am cool!" "YAGPDB is" }}`returns  `YAGPDB is cool!` \(regex pattern is case sensitive\). |

### Math functions

| Function | Description |
| :--- | :--- |
| `add x y z ...` | Returns x + y + z + ....,  detects first number type; is it integer or float and based on that adds. \(use `toFloat` on the first argument to force floating point math.\)`{{ add 5 4 3 2 -1 }}` sums all these numbers and returns `13`. |
| `mult x y z ...` | Multiplication, like `add` or `div`, detects first number type. `{{ mult 3.14 2 }}` returns `6.28` |
| `div x y z ...` | Division, like `add` or `mult`, detects number type first. `{{ div 11 3 }}` returns `3` whereas `{{ div 11.1 3 }}` returns  `3.6999999999999997` |
| `fdiv x y z ...` | Meant specifically for floating point numbers division.  |
| `randInt (stop, or start stop)` | Returns a random integer between 0 and stop, or start - stop if two args are provided. |

### Message functions

| Function | Description |
| :--- | :--- |
| `sendDM "message here"` | Sends the user a direct message, only one DM can be sent per template \(accepts embed objects\). random adjective. |
| `sendMessage channel message` | Sends `message (string or embed)` in `channel`, channel can be either `nil`, the channel ID or the channel's "name". |
| `sendMessageRetID channel message` | Same as `sendMessage`, but also returns messageID to assigned variable for later use. Example in [Snippets](templates.md#snippets). |
| `sendMessageNoEscape channel message` | Sends `message (string or embed)` in `channel`, channel can be either `nil`, the channel ID or the channel "name". Doesn't escape mentions \(e.g. role mentions or @here/@everyone\). |
| `sendMessageNoEscapeRetID channel message` | Same as `sendMessageNoEscape`, but also returns messageID to assigned variable for later use. |
| `editMessage channel messageID newMessageContent` | Edits the message in channel, channel can be either `nil`, channel's ID or "name". Light example in [Snippets](templates.md#snippets). |
| `editMessageNoEscape channel messageID newMessageContent` | Edits the message in channel and has same logic in escaping characters as `sendMessageNoEscape`. |
| `getMessage channelID messageID` | Returns a [Message ](templates.md#message)object |
| `deleteResponse time` | Deletes the response after a certain time \(1-60 seconds\). |
| `deleteTrigger time` | Deletes the trigger after a certain time \(1-60 seconds\). |
| `deleteMessage channel messageID (delay)` | Deletes message with given `messageID` from `channel`. Channel can be either `nil`, channelID or channel's name. `(Delay)` is optional and defaults to 10 seconds. Example in [Snippets](templates.md#snippets). |
| `addReactions "👍" "👎"` | Adds each emoji as a reaction to the message that triggered the command \(recognizes Unicode emojis and `emojiname:emojiid`\). |
| `addResponseReactions "👍" "👎"` | Adds each emoji as a reaction to the response message \(recognizes Unicode emojis and `emojiname:emojiid`\). |
| `addMessageReactions channel messageID reactions` | Same as `addReactions` or `addResponseReactions`, but can be used on any messages using its ID. Channel can be either `nil`, channelID or channel's name. Example in [Snippets](templates.md#snippets). |

### Mentions

| Function | Description |
| :--- | :--- |
| `mentionEveryone` | Mentions `@everyone`. |
| `mentionHere` | Mentions `@here`. |
| `mentionRoleName "rolename"` | Mentions the first role found with the provided name \(case-insensitive\). |
| `mentionRoleID roleID` | Mentions the role found with the provided ID. |
| `escapeEveryone "input"` | Escapes everyone mentions in a string. |
| `escapeHere "input"` | Escapes here mentions in a string. |
| `escapeEveryoneHere "input"` | Escapes everyone and here mentions in a string. Useful with sendMessageNoEscape, also applies to escapeEveryone/Here. Example in [Snippets](templates.md#snippets). |

### Role functions

| Function | Description |
| :--- | :--- |
| `hasRoleName "rolename"` | Returns true if the user has the role with the specified name \(case-insensitive\). |
| `hasRoleID roleID` | Returns true if the user has the role with the specified ID \(use the listroles command for a list of roles\). |
| `addRoleID roleID` | Adds the role with the given ID to the user that triggered the command \(use the listroles command for a list of roles\). |
| `removeRoleID roleID (delay)` | Removes the role with the given ID from the user that triggered the command \(use the listroles command for a list of roles\). `Delay` is otional argument in seconds. |
| `giveRoleID userID roleID` | Gives a role by ID to the target. |
| `giveRoleName userID "roleName"` | Gives a role by name to the target. |
| `takeRoleID userID roleID (delay)` | Takes away a role by ID from the target. `Delay` is otional argument in seconds. |
| `takeRoleName userID roleName (delay)` | Takes away a role by name from the target. `Delay` is otional argument in seconds. |
| `targetHasRoleID userID roleID` | Returns true if the given user has the role with the specified ID \(use the listroles command for a list of roles\). Example in [Snippets](templates.md#snippets). |
| `targetHasRoleName userID "roleName"` | Returns true if the given user has the role with the specified name \(case-insensitive\). |

### Miscellaneous

| Function | Description |
| :--- | :--- |
| `adjective` | Returns a random adjective. |
| `dict key1 value1 key2 value2 ...` | Creates a dictionary \(not many use cases yet\). |
| `sdict "key1" "value1" "key2" "value2" ...` |  The same as `dict` but with only string keys and can be used in `cembed`. Has `.Get "key"` and `.Set "key"` methods, they allow to capture or change value content from given key.  Example on using those methods in [Snippets](templates.md#snippets). |
| `cslice value1 value2 ...` | Creates a slice \(similar to array\) that can be used elsewhere \(`cembed` and `sdict` for example\). |
| `cembed "list of embed values"` | Function to generate embed inside custom command. [More in-depth here](../others/custom-embeds.md#embeds-in-custom-commands).  |
| `in list value` | Returns true if value is in list. List can be either an array or a slice. |
| `inFold`  | Same as `in`, but is case insensitive. |
| `seq start stop` | Creates a new array of integer, starting from start and ending at stop. |
| `shuffle list` | Returns a shuffled version of a list. |
| `exec "command" "args" "args" "args" ...` | Execute a YAGPDB \(e.g. reverse, roll, kick etc\) in a custom command. Exec can be run max 5 times per command.  |
| `execAdmin "command" "args" "args" "args" ...` | Function the same as exec but will override any permission requirement \(such as the kick permission to use kick command etc.\). |
| `userArg ########` | Function that can be used to retrieve .User method/object from a mention string or ID. |
| `parseArgs required_args error_message ...carg` | Checks the arguments for a specific type. [More in depth here](../commands/custom-commands.md#require-arguments) and an example in [Custom Command Examples.](custom-command-examples.md#parseargs-example) |
| `carg type name` | Defines type of argument for parseArgs. [More in depth](../commands/custom-commands.md#require-arguments) here and an example in [Custom Command Examples.](custom-command-examples.md#parseargs-example) |
| `sleep seconds` | Pauses execution of template inside custom command for max 60 seconds. Argument`seconds`is of type integer. Example in [Snippets](templates.md#snippets). |
| `execCC ccID channel delay data` | Function that executes another custom command specified by `ccID,`max recursion depth is 2 and it's rate-limited strictly at max 10 delayed custom commands executed per channel per minute, if you go over that it will be simply thrown away. Argument `channel` can be `nil`, channel's ID or name. The`delay` argument is execution delay of another CC is in seconds. The `data` argument is content that you pass to the other executed custom command. To retrieve that `data` you use `.ExecData`. This example is important &gt; [execCC example](custom-command-examples.md#execcc-example) also this snippet that shows you same thing run using the same custom command &gt; [Snippets](templates.md#snippets). |

## Branching

Branching using if pipeline and comparison operators.

| Case | Example |
| :--- | :--- |
| Basic if |  `{{if (condition)}} {{end}}` |
| Not |  `{{if not (condition)}} {{end}}` |
| And |  `{{if and (cond1) (cond2) (cond3)}}` |
| Or |  `{{if or (cond1) (cond2) (cond3)}} {{end}}` |
| Equal |  `{{if eq .Channel.ID ########}} {{end}}` |
| Not equal |  `{{if ne .Channel.ID #######}} {{end}}` |
| Less than |  `{{if lt (len .Args) 5}} {{end}}` |
| Less than or equal | `{{if le (len .Args) 5}} {{end}}` |
| Greater than |  `{{if gt (len .Args) 1}} {{end}}` |
| Greater than or equal | `{{if ge (len .Args) 1}} {{end}}` |
| Else if |  `{{if (case statement)}} {{else if (case statement)}} {{end}}` |
| Else |  `{{if (case statement)}} {{else}} output here {{end}}` |

## Snippets

* `<@{{.User.ID}}>` Outputs a mention to the user that called the command.
* `<@###########>` Mentions the user that has the ID \#\#\#\#\#\# \(See [How to get IDs](templates.md#how-to-get-ids) to get ID\).
* `<#&&&&&&&&&&&>` Mentions the channel that has ID &&&&&& \(See [How to get IDs](templates.md#how-to-get-ids) to get ID\).
* `<@&##########>` Mentions the role with ID \#\#\#\#\#\#\#\# \( [lis~~t~~roles](../commands/all-commands.md#listroles) command gives roleIDs \). This is usable for example with `{{ sendMessageNoEscape nil "Welcome to role <@&11111111...>" }}`. Mentioning that role has to be enabled server- side in Discord.
* `{{if hasRoleName "funrole"}} Has role funrole {{end}}`This will only show if the member has a role with name "funrole" .
* `{{if gt (len .Args) 0}} {{index .Args 1}} {{end}}`Assuming your trigger is a command, will display your first input if input was given.
* `{{if eq .Channel.ID #######}} YAG! {{end}}`Will only show `YAG!` in Channel \#\#\#\#\#.
* `{{if ne .User.ID #######}} YAG! {{end}}`Will ignore if user ID equal to \#\#\#\#\# uses command.
* `{{$d := randInt 10}}` Store the random int into variable $d \(A random number from 0-9\).
* `{{addReactions .CmdArgs}}` Adds the emoji following a trigger as reactions.
* `{{$a := (exec "catfact")}}` Saves the response of the `catfact` ****command to variable `$a`. 
* `{{$allArgs := (joinStr " " .CmdArgs)}}` Saves all the arguments after trigger to a variable `$allArgs`. 
* `{{$args:= (joinStr " " (slice .CmdArgs 1))}}` Saves all the arguments except the first one to a variable `$args`. 
* `{{/* this is a comment */}}`For commenting something inside a template, use this syntax.
* Sends message to current channel `nil` and gets messageID to variable `$x`. Also adds reactions to this message. After 5 seconds, deletes that message. &gt;

  `{{ $x := sendMessageRetID nil "Hello there!" }} {{ addMessageReactions nil $x "👍" "👎" }} {{ deleteMessage nil $x 5 }}` 

* To demonstrate usage of escapeEveryoneHere. &gt; `{{ $x := "@here Hello World! @everyone" }} {{ sendMessage nil $x }} {{ sendMessageNoEscape nil $x }} {{ sendMessageNoEscape nil ( escapeEveryoneHere $x ) }}`
* To demonstrate usage of targetHasRoleID. &gt;  `{{ $x := ( userArg ( index .Args 1) ).ID }} {{ if targetHasRoleID $x ############ }} Has the Role! {{ else }} Does not have the role! {{ end }}`
* To demonstrate usage of reFindAll. &gt;  `Before regex: {{ $msg := "1 YAGPDB and over 100000 servers conqured." }} {{ $re2 := reFindAll "[0-9]+" $msg }} {{ $msg }}   After regex matches: {{ joinStr " " "Only" ( index $re2 0 ) "YAGPDB and already" ( index $re2 1 ) "servers captured."}}`
* To demonstrate usage of sdict methods .Get and .Set.  &gt;  `{{ $x := sdict "key" "value" }} {{ $x.Get "key" }} {{ $x.Set "key" "eulav" }} {{ $x.Get "key" }}` to add to that `sdict`, simply use `.Set` again &gt;  `{{ $x.Set "YAGPDB" "is cool!" }} {{ $x }}`
* To demonstrate sleep and slightly also editMessage functions. &gt; `{{ $x := sendMessageRetID nil "Hello" }} {{ sleep 3 }} {{ editMessage nil $x "There" }} {{ sleep 5 }} {{ sendMessage nil "We all know, that" }} {{ sleep 3 }} YAGPDB rules!`
* To demonstrate usage of split function. &gt; `{{ $x := "Hello, World, YAGPDB, here!" }} {{ range $k, $v := ( split $x ", " ) }}Word {{ $k }}: __{{ $v }}__ {{ end }}`
* To demonstrates execCC  and .ExecData on using same CC. `{{ $yag := "YAGPDB rules! " }} {{ $ctr := 0 }} {{ $yourCCID := YOURNUMBER-HERE }} {{ if .ExecData }} {{ $ctr = add .ExecData.number 1 }} {{ $yag = joinStr "" $yag $ctr }} {{ .ExecData.YAGPDB }} {{ else }} So, someone rules. {{ $ctr = add $ctr 1 }} {{ $yag = joinStr "" $yag 1 }} {{ end }} {{ if lt $ctr 5 }} {{ execCC $yourCCID nil 10 ( sdict "YAGPDB" $yag "number" $ctr ) }} {{ else }} FUN'S OVER! {{ end }}`

## How to get IDs <a id="how-to-get-ids"></a>

**User IDs:** Can be found by mentioning the user then adding a \ such as `\@jonas747#0001` . Alternatively if you have developer mode on, you can right click and select Copy ID

**Channel IDs:** Can be found by mentioning the channel then adding a \ such as `\#announcements`. Alternatively if you have developer mode on, you can right click on the channel and select Copy ID.

**Role IDs**: Use the `listroles`command.

**Emote IDs:** 

If it is a **custom emote**, adding a \ in front of the emote such as `\:yag:` will display the name along with the ID such as  `<:yag:277569741932068864>`.

If it is an **animated emote**, do the same steps as a normal emote. If you do not have Discord Nitro, you can have a friend or a bot use the emote and right click on the emote to open its link. The ID will be a part of the URL.

If it is a **default emote**, look up the Unicode for the emote on Google. Note that some of the more customized default emotes such as some of the family emotes will not work in any of the YAGPDB commands. 

