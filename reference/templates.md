# Templates

All available data that can be used in YAGPDB's templating "engine" which is slightly modified version of Golang's stdlib text/template package; more in depth and info about actions, pipelines and global functions like `printf, index`etc &gt; [https://golang.org/pkg/text/template/](https://golang.org/pkg/text/template/)

{% hint style="warning" %}
**Put curly brackets around the data you want to formulate as template** like this: `{{ .User.Username }}`

This `{{ ... }}` syntax of having two curly brackets aka braces around context is always necessary to form a template with methods and functions stated below.
{% endhint %}

{% hint style="info" %}
If you want to join different data objects \(e.g. to wrap toString in joinStr around .Guild.MemberCount\), you use round brackets aka parentheses as delimiters:  
`{{ joinStr "" "Our member count is " (toString .Guild.MemberCount) "!" }}`
{% endhint %}

{% hint style="info" %}
Templating system uses standard ASCII quotation marks:  
0x22 &gt; `"` for straight double quotes, 0x27 &gt; `'`for apostrophes and 0x60 ````` for backticks;   
so make sure no "smart-quotes" are being used.
{% endhint %}

{% hint style="success" %}
"Go is all about type... Type is life." // William Kennedy   
Many problems start with different kinds of type the user has as values and what is needed for arguments. YAGPDB usually states that in error message - what went wrong with type.  
  
To see of what type a variable or function's return is, use printf "%T", for example &gt; `{{ printf "%T" currentTime }}` will output the type `time.Time`.
{% endhint %}

## The Dot

The dot `{{ . }}`  encompasses all active data available for templating system.   
From official docs &gt; "Execution of the template walks the structure and sets the cursor, represented by a period '.' and called "dot", to the value at the current location in the structure as execution proceeds." Following Methods/Objects like `User/Guild/Member/Channel etc` are all part of that dot-structure and there are some more in table below.

| Field | Description |
| :--- | :--- |
| .CCID | The ID of currently executing custom command in type of int64. |
| .IsPremium | Returns boolean true/false whether guild is premium of YAGPDB or not. |

## User

| Field | Description |
| :--- | :--- |
| .User | The user's username together with discriminator. |
| .User.String | The user's username together with discriminator as string-type. |
| .User.Username | The user's username. |
| .User.ID | The user's ID. |
| .User.Discriminator | The user's discriminator \(The four digits after a person's username\). |
| .User.Avatar | The user's avatar ID. |
| .User.AvatarURL "256" | Gives the URL for user's avatar, argument "256" is the size of the picture  and can increase/decrease twofold \(e.g. 512, 1024 or 128, 64 etc.\). |
| .User.Bot | Determines whether the target user is a bot - if yes, it will return True. |
| .User.Mention | Mentions user. |
| .RealUsername | Only works with join and leave messages \(not join dms\). This can be used to send the real username to a staff channel when invites are censored. |
| .UsernameHasInvite | Only works with join and leave messages \(not join dms\). It will determine does the username contain an invite link. |

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>userArg mention/userID</code>
      </td>
      <td style="text-align:left">
        <p>Function that can be used to retrieve .User object from a mention or userID.</p>
        <p><code>{{ (userArg .User.ID).Mention }}</code> mentions triggering user.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>pastUsernames userID offset</code>
      </td>
      <td style="text-align:left">
        <p>Returns a slice of type <code>[ ]*logs.CCNameChange</code> having fields <code>.Name</code> and <code>.Time</code> of
          previous 15 usernames and skips <code>offset</code> number in that list.</p>
        <p><code>{{ range pastUsernames .User.ID 0 }} <br />{{ .Name }} - {{ .Time.Format &quot;Jan _2 2006&quot; }} <br />{{ end }}</code> 
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>pastNicknames userID offset</code>
      </td>
      <td style="text-align:left">Same as <code>pastUsernames</code>.</td>
    </tr>
  </tbody>
</table>## Guild / Server

| Field | Description |
| :--- | :--- |
| .Guild.ID | Outputs the ID of the guild. |
| .Guild.Name | Outputs the name of the guild. |
| .Guild.Icon | Outputs the ID of the guild's icon. |
| .Guild.Region | Outputs the region of the guild. |
| .Guild.AfkChannelID | Outputs the AFK channel ID. |
| .Guild.OwnerID | Outputs the ID of the owner. |
| .Guild.JoinedAt | Outputs the timestamp when YAGPDB joined the guild. To convert it to type Time, use .Parse method &gt; `.Guild.JoinedAt.Parse` |
| .Guild.AfkTimeout | Outputs the time when a user gets moved into the AFK channel while not being active. |
| .Guild.MemberCount | Outputs the number of users on a guild. |
| .Guild.VerificationLevel | Outputs the required verification level for the guild. |
| .Guild.EmbedEnabled | Outputs whether guild is embeddable \(e.g. widget\) or not, true / false. |
| .Guild.Roles | Outputs all roles and indexing them gives more information about the role. For exampe `{{ len .Server.Roles }}` gives you how many roles are there in that guild. |

## Member

| Field | Description |
| :--- | :--- |
| .Member.JoinedAt | When member joined the guild/server of type Timestamp. .Parse method will convert this to of type Time. |
| .Member.Nick | The nickname for this member. |
| .Member.Roles | A list of role IDs that the member has. |
| .Member.User | Underlying user on which the member is based on. |

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>getMember</code>
      </td>
      <td style="text-align:left">
        <p>Function returns Member object having above methods.</p>
        <p><code>{{ (getMember .User.ID).JoinedAt }}</code> 
          <br />is the same as <code>{{ .Member.JoinedAt }}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>onlineCount</code>
      </td>
      <td style="text-align:left">Returns the count of online users/members on current server.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>onlineCountBots</code>
      </td>
      <td style="text-align:left">Returns the count of online bots.</td>
    </tr>
  </tbody>
</table>## Channel

| Field | Description |
| :--- | :--- |
| .Channel.Name | The Name of the channel. |
| .Channel.ID | The ID of the channel. |
| .Channel.ParentID | The ID of the channel's parent \(category\), returns 0 if none. |
| .Channel.Topic | The Topic of the channel. |
| .Channel.NSFW | Outputs whether this channel is NSFW or not. |

| Function | Description |
| :--- | :--- |
| `editChannelName  channel "newName"` | Function that edits channel's name. `channel` can be either ID, "name" or even `nil` if triggered in that channel name change is intended to happen. For example  &gt;`{{ editChannelName nil (joinStr "" "YAG - " (randInt 1000) ) }}` |

## Message

| Field | Description |
| :--- | :--- |
| .Message.ID | ID of the message. |
| .Message.ChannelID | Channel id this message is in. |
| .Message.Author | Author of the message \([User](templates.md#user) object\). |
| .Message.Timestamp | Timestamp of the message in type timestamp \(use .Message.Timestamp.Parse to get type time and .Parse.String method returns type string\). |
| .Message.Attachments | Attachments to this message \(slice of attachment objects\). |
| .Message.Embeds | Embeds on this message \(slice of embed objects\). |
| .Message.Mentions | Users this message mentions. |
| .Message.Reactions | Reactions on this message \(only available form getMessage\). |
| .Message.Content | Text content on this message. |
| .Args | List of everything that is passed to .Message.Content. .Args is a slice of type string. |
| .Cmd | .Cmd is of type string and shows all arguments that trigger custom command, part of .Args. Starting from `{{ index .Args 0 }}`.  |
| .CmdArgs | List of all the arguments passed after .Cmd \(.Cmd is the actual trigger\) .CmdArgs is a slice of type string. |
| .StrippedMsg | "Strips" or cuts off the triggering part of the message and prints out everything else after that. Bare in mind, when using regex as trigger, for example `"day"` and input message is `"Have a nice day my dear YAG!"` output will be `"my dear YAG!"`  - rest is cut off. |

{% hint style="info" %}
More information about the `Message` template can be found [here](../commands/custom-commands.md#the-message-template).
{% endhint %}

## Reaction

This is available and part of the dot when reaction trigger type is used.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">.Reaction</td>
      <td style="text-align:left">Returns reaction object which has following fields <code>UserID</code>, <code>MessageID</code>,
        <br
        /><code>Emoji.(ID/Name/...)</code>, <code>ChannelID</code>, <code>GuildID</code>.
        Emoji.ID is the ID of the emoji for custom emojis, and Emoji.Name will
        hold the unicode emoji if its a default one. (otherwise the name of the
        custom emoji).</td>
    </tr>
    <tr>
      <td style="text-align:left">.ReactionMessage</td>
      <td style="text-align:left">
        <p>Returns the message object reaction was added to.</p>
        <p><code>{{ range .ReactionMessage.Reactions }}<br />{{ .Count }} - {{ .Emoji.Name }} <br />{{ end }}</code>
        </p>
        <p>Returns emoji count and their name.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">.ReactionAdded</td>
      <td style="text-align:left">Returns a boolean true/false indicating whether reaction was added or
        removed.</td>
    </tr>
  </tbody>
</table>## Time

Time in general uses Golang's time package library &gt; [https://golang.org/pkg/time/\#time](https://golang.org/pkg/time/#Time) and also this although slightly different syntax all applies here &gt; [https://gobyexample.com/time](https://gobyexample.com/time).

| Field | Description |
| :--- | :--- |
| .TimeHour | Variable of time.Duration type and returns 1 hour &gt; `1h0m0s`. |
| .TimeMinute | Variable of time.Duration type and returns 1 minute &gt; `1m0s`. |
| ~~.~~TimeSecond | Variable of time.Duration type and returns 1 second &gt; `1s`. |

| Function | Description |
| :--- | :--- |
| `currentTime` | Gets the current time, value is of type time; which can be used in a custom embed. More info [here](../commands/custom-commands.md#currenttime-template). |
| `formatTime Time "arg"` | Outputs given time in RFC822 formatting, first argument `Time` shows it needs to be of type time, also with extra layout if second argument is given - e.g. `{{ formatTime currentUserCreated "3:04PM" }}` would output `11:22AM` if that would have been user's creating time. |
| `humanizeDurationHours` | Returns `nanoseconds` argument of type int64 in human readable format - as how long it would take to get towards given time - e.g. `{{ humanizeDurationHours 9000000000000000000 }}` returns `285 years 20 weeks 6 days and 16 hours`. |
| `humanizeDurationMinutes` | Sames as `humanizeDurationHours`, this time duration is given in minutes - e.g. `{{ humanizeDurationMinutes 3500000000000 }}` would return `58 minutes`. |
| `humanizeDurationSeconds` | Sames as both humanize functions above, this time duration is given in seconds - e.g. `{{ humanizeDurationSeconds 3500000000000 }}` would return `58 minutes and 20 seconds`. |
| `humanizeTimeSinceDays` | Returns time has passed since given argument of type Time in human readable format - e.g. `{{ humanizeTimeSinceDays currentUserCreated }}` |
| `newDate year month day hour minute second` | Returns new time object in UTC using following syntax... all arguments need to be of type int, for example &gt; `{{ humanizeDurationHours ( (newDate 2059 1 2 12 34 56).Sub currentTime) }}` will give you how much time till year 2059 January 2nd 12:34:56. |

#### This section's snippets:

* To demonstrate humanizeDurationHours and also how to parse a timestamp, output will be like `whois` command shows user's _join server age_. `{{ humanizeDurationHours (currentTime.Sub .Member.JoinedAt.Parse) }}`

## Functions

### Type conversion

| Function | Description |
| :--- | :--- |
| `toString` | Converts something into a string. Usage: `(toString x)`. |
| `toInt` | Converts something into an integer. Usage: `(toInt x)`. |
| `toInt64` | Converts something into an int64. Usage: `(toInt64 x)`. |
| `toFloat` | Converts argument \(number of string\) to type float64.  Usage: `(toFloat x)`. |
| `toDuration` | Converts argument \(number or string\) to type Duration, usable in time operations. Usage:`(toDuration x)`. Example in section's [Snippets](templates.md#this-sections-snippets-1).  |
| `json value` | Traverses given `value` through MarshalJSON \([more here](%20https://golang.org/pkg/encoding/json/#Marshal)\) and returns it as type string. For example `{{ json .TimeHour }}` outputs type string; before this `.TimeHour` was of type time.Duration. Basically it's good to use if multistep type conversion is needed `(toString (toInt value) )` and certain parts of `cembed` need this for example. |

#### This section's snippets:

* To demonstrate toDuration, outputs 12 hours from current time in UTC. `{{ (currentTime.Add (toDuration (mult 12 .TimeHour) ) ).Format "15:04" }}`

### String manipulation

| Function | Description |
| :--- | :--- |
| `joinStr "separator" "str1" (arg1)(arg2) "str2" ...` | Joins several strings into one, separated by the first arg`"separator"`, useful for executing commands in templates \(e.g.`{{joinStr "" "1" "2" "3"}}` returns `123`\). |
| `lower "string"` | Converts the string to lowercase. |
| `upper "string"` | Converts the string to uppercase. |
| `slice "string" integer (integer2)` | Outputs the "string" after cutting/slicing off integer \(numeric\) value of symbols \(actually starting the string's index from integer through integer2\) - e.g. `{{slice "Fox runs" 2}}`outputs `x runs`. When using also integer2 - e.g. `{{slice "Fox runs" 1 7 }}`, it outputs `ox run`. For slicing whole words, see example in section's [Snippets](templates.md#this-sections-snippets-2).  |
| `urlescape "string"` | Escapes the string so it can be safely placed inside a URL path segment - e.g. "Hello, YAGPDB!" becomes "Hello%2C%20YAGPDB%21" |
| `split "string" "sepr"` | Slices given `"string"` to sub-strings separated by `"sepr"`arg and returns new slice/array of the sub-strings. Example in section's [Snippets](templates.md#this-sections-snippets-2). |
| `title "string"` | Returns string with the first letter of each word capitalized. |
| `reFind "regex" "string"` | Compares string to regex pattern and returns first match. `{{ reFind "AG" "YAGPDB is cool!" }}`returns `AG` \(regex pattern is case sensitive\). |
| `reFindAll "regex" "string"` | Adds all regex matches from the string to a slice. Example in section's [Snippets](templates.md#this-sections-snippets-2). |
| `reFindAllSubmatches "regex" "string"` | Returns whole-pattern matches and also the sub-matches within those matches as slices inside a slice. `{{ reFindAllSubmatches "(?i)y([a-z]+)g" "youngish YAGPDB" }}` returns `[[young oun] [YAG A]]` \(regex pattern here is case insensitive\). |
| `reReplace "regex" "string1" "string2"` | Replaces string1 contents with string2 at regex match point. `{{ reReplace "I am" "I am cool!" "YAGPDB is" }}`returns  `YAGPDB is cool!` \(regex pattern here is case sensitive\). |

{% hint style="info" %}
With regular expression patterns - when using quotes you have to "double-escape" metacharacters starting with backslash or use backquotes/ticks to simplify this. `{{ reFind "\\d+" (toString 42) }}` versus ``{{ reFind `\d+` (toString 42) }}``
{% endhint %}

#### This section's snippets:

* `{{ $args:= (joinStr " " (slice .CmdArgs 1) ) }}` Saves all the arguments except the first one to a variable `$args`. 
* To demonstrate usage of split function. &gt; `{{ $x := "Hello, World, YAGPDB, here!" }} {{ range $k, $v := (split $x ", ") }}Word {{ $k }}: __{{ $v }}__ {{ end }}`
* To demonstrate usage of reFindAll. &gt;  `Before regex: {{ $msg := "1 YAGPDB and over 100000 servers conqured." }} {{ $re2 := reFindAll "[0-9]+" $msg }} {{ $msg }}   After regex matches: {{ joinStr " " "Only" (index $re2 0) "YAGPDB and already" (index $re2 1) "servers captured."}}`

### Math functions

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>add x y z ...</code>
      </td>
      <td style="text-align:left">Returns x + y + z + ...., detects first number type; is it integer or
        float and based on that adds. (use <code>toFloat</code> on the first argument
        to force floating point math.)<code>{{ add 5 4 3 2 -1 }}</code> sums all
        these numbers and returns <code>13</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>mult x y z ...</code>
      </td>
      <td style="text-align:left">Multiplication, like <code>add</code> or <code>div</code>, detects first
        number type. <code>{{ mult 3.14 2 }}</code> returns <code>6.28</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>div x y z ...</code>
      </td>
      <td style="text-align:left">Division, like <code>add</code> or <code>mult</code>, detects number type
        first. <code>{{ div 11 3 }}</code> returns <code>3</code> whereas <code>{{ div 11.1 3 }}</code> returns <code>3.6999999999999997</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>fdiv x y z ...</code>
      </td>
      <td style="text-align:left">Meant specifically for floating point numbers division.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>mod x y</code>
      </td>
      <td style="text-align:left">Mod returns the floating-point remainder of x/y. <code>mod 17 3</code> returns <code>2 </code>of
        type float64.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>randInt (stop, or start stop)</code>
      </td>
      <td style="text-align:left">
        <p>Returns a random integer between 0 and stop, or start - stop if two args
          are provided.</p>
        <p>Result will be <code>start &lt;= random numer &lt; stop</code>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>round</code>
      </td>
      <td style="text-align:left">Returns the nearest integer, rounding half away from zero. Regular rounding
        &gt; 10.4 is 10 and 10.5 is 11. All round functions return type float64,
        so use conversion functions to get integers. For more complex rounding,
        example in section&apos;s <a href="templates.md#this-sections-snippets-3">Snippets</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>roundCeil</code>
      </td>
      <td style="text-align:left">Returns the least integer value greater than or equal to input or rounds
        up. <code>{{ roundCeil 1.1 }}</code> returns <code>2</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>roundFloor</code>
      </td>
      <td style="text-align:left">Returns the greatest integer value less than or equal to input or rounds
        down. <code>{{ roundFloor 1.9 }}</code> returns <code>1</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>roundEven </code>
      </td>
      <td style="text-align:left">Returns the nearest integer, rounding ties to even.
        <br /><code>{{ roundEven 10.5 }}</code> returns <code>10 {{ roundEven 11.5 }}</code> returns <code>12</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sqrt</code>
      </td>
      <td style="text-align:left">Returns the square root of a number.
        <br /><code>{{ sqrt 49 }}</code> returns <code>7, {{ sqrt 12.34 | printf &quot;%.4f&quot; }} returns 3.5128</code>
      </td>
    </tr>
  </tbody>
</table>#### This section's snippets:

* To demonstrate rounding float to 2 decimal places. `{{ div (round (mult 12.3456 100) ) 100 }}` returns 12.35 `{{ div (roundFloor (mult  12.3456 100) ) 100 }}` returns 12.34

### Message functions

| Function | Description |
| :--- | :--- |
| `sendDM "message here"` | Sends the user a direct message, only one DM can be sent per template \(accepts embed objects\). random adjective. |
| `sendMessage channel message` | Sends `message (string or embed)` in `channel`, channel can be either `nil`, the channel ID or the channel's "name". |
| `sendMessageRetID channel message` | Same as `sendMessage`, but also returns messageID to assigned variable for later use. Example in section's [Snippets](templates.md#this-sections-snippets-4). |
| `sendMessageNoEscape channel message` | Sends `message (string or embed)` in `channel`, channel can be either `nil`, the channel ID or the channel "name". Doesn't escape mentions \(e.g. role mentions or @here/@everyone\). |
| `sendMessageNoEscapeRetID channel message` | Same as `sendMessageNoEscape`, but also returns messageID to assigned variable for later use. |
| `editMessage channel messageID newMessageContent` | Edits the message in channel, channel can be either `nil`, channel's ID or "name". Light example in section's [Snippets](templates.md#this-sections-snippets-4). |
| `editMessageNoEscape channel messageID newMessageContent` | Edits the message in channel and has same logic in escaping characters as `sendMessageNoEscape`. |
| `getMessage channelID messageID` | Returns a [Message ](templates.md#message)object. |
| `deleteResponse time` | Deletes the response after a certain time \(max 86400 seconds\). |
| `deleteTrigger time` | Deletes the trigger after a certain time \(max 86400 seconds\). |
| `deleteMessage channel messageID (delay)` | Deletes message with given `messageID` from `channel`. Channel can be either `nil`, channelID or channel's name. `(Delay)` is optional and like previous two delete functions, it defaults to 10 seconds, max being 1 day. Example in section's [Snippets](templates.md#this-sections-snippets-4). |
| `addReactions "👍" "👎"` | Adds each emoji as a reaction to the message that triggered the command \(recognizes Unicode emojis and `emojiname:emojiid`\). |
| `addResponseReactions "👍" "👎"` | Adds each emoji as a reaction to the response message \(recognizes Unicode emojis and `emojiname:emojiid`\). |
| `addMessageReactions channel messageID reactions` | Same as `addReactions` or `addResponseReactions`, but can be used on any messages using its ID. Channel can be either `nil`, channelID or channel's name. Example in section's [Snippets](templates.md#this-sections-snippets-4). |
| `deleteAllMessageReactions channel messageID` | Deletes all reactions pointed message has. `channel` can be ID, "name" or `nil`. |

#### 

#### This section's snippets:

* Sends message to current channel `nil` and gets messageID to variable `$x`. Also adds reactions to this message. After 5 seconds, deletes that message. &gt;

  `{{ $x := sendMessageRetID nil "Hello there!" }} {{ addMessageReactions nil $x "👍" "👎" }} {{ deleteMessage nil $x 5 }}`

* To demonstrate sleep and slightly also editMessage functions. &gt; `{{ $x := sendMessageRetID nil "Hello" }} {{ sleep 3 }} {{ editMessage nil $x "There" }} {{ sleep 5 }} {{ sendMessage nil "We all know, that" }} {{ sleep 3 }} YAGPDB rules!`

### Mentions

| Function | Description |
| :--- | :--- |
| `mentionEveryone` | Mentions `@everyone`. |
| `mentionHere` | Mentions `@here`. |
| `mentionRoleName "rolename"` | Mentions the first role found with the provided name \(case-insensitive\). |
| `mentionRoleID roleID` | Mentions the role found with the provided ID. |
| `escapeEveryone "input"` | Escapes everyone mentions in a string. |
| `escapeHere "input"` | Escapes here mentions in a string. |
| `escapeEveryoneHere "input"` | Escapes everyone and here mentions in a string. Useful with sendMessageNoEscape, also applies to escapeEveryone/Here. Example in section's [Snippets](templates.md#this-sections-snippets-5). |

#### This section's snippets:

* `<@{{ .User.ID }}>` Outputs a mention to the user that called the command.
* `<@###########>` Mentions the user that has the ID \#\#\#\#\#\# \(See [How to get IDs](templates.md#how-to-get-ids) to get ID\).
* `<#&&&&&&&&&&&>` Mentions the channel that has ID &&&&&& \(See [How to get IDs](templates.md#how-to-get-ids) to get ID\).
* `<@&##########>` Mentions the role with ID \#\#\#\#\#\#\#\# \([lis~~t~~roles](../commands/all-commands.md#listroles) command gives roleIDs\). This is usable for example with `{{ sendMessageNoEscape nil "Welcome to role <@&11111111...>" }}`. Mentioning that role has to be enabled server- side in Discord.
* To demonstrate usage of escapeEveryoneHere. &gt; `{{ $x := "@here Hello World! @everyone" }} {{ sendMessage nil $x }} {{ sendMessageNoEscape nil $x }} {{ sendMessageNoEscape nil (escapeEveryoneHere $x) }}`

### Role functions

| Function | Description |
| :--- | :--- |
| `hasRoleName "rolename"` | Returns true if the user has the role with the specified name \(case-insensitive\). |
| `hasRoleID roleID` | Returns true if the user has the role with the specified ID \(use the listroles command for a list of roles\). |
| `addRoleID roleID` | Adds the role with the given ID to the user that triggered the command \(use the listroles command for a list of roles\). |
| `removeRoleID roleID (delay)` | Removes the role with the given ID from the user that triggered the command \(use the listroles command for a list of roles\). `Delay` is optional argument in seconds. |
| `giveRoleID userID roleID` | Gives a role by ID to the target. |
| `giveRoleName userID "roleName"` | Gives a role by name to the target. |
| `takeRoleID userID roleID (delay)` | Takes away a role by ID from the target. `Delay` is optional argument in seconds. |
| `takeRoleName userID "roleName" (delay)` | Takes away a role by name from the target. `Delay` is optional argument in seconds. |
| `targetHasRoleID userID roleID` | Returns true if the given user has the role with the specified ID \(use the listroles command for a list of roles\). Example in section's [Snippets](templates.md#this-sections-snippets-6). |
| `targetHasRoleName userID "roleName"` | Returns true if the given user has the role with the specified name \(case-insensitive\). |

#### This section's snippets:

* To demonstrate usage of targetHasRoleID. &gt;  `{{ $x := (userArg (index .Args 1) ).ID }} {{ if targetHasRoleID $x ############ }} Has the Role! {{ else }} Does not have the role! {{ end }}`

### Current User

| Function | Description |
| :--- | :--- |
| `currentUserCreated` |  Returns value of type time and shows when the current user was created. |
| `currentUserAgeHuman` |  The account age of the current user in more human readable format  \(Eg:`3 days 2 hours`\). |
| `currentUserAgeMinutes` |  The account age of the current user in minutes. |

### Miscellaneous

| Function | Description |
| :--- | :--- |
| `adjective` | Returns a random adjective. |
| `range slice/array` | Iterates \(loops\) over the given slice or array and sets successive elements as active data \(the dot\) to be further handled inside the range template. Example usage [here](custom-command-examples.md#range-example) |
| `dict key1 value1 key2 value2 ...` | Creates an unordered collection of key-value pairs, a dictionary so to say. The number of parameters to form key-value pairs must be even. |
| `sdict "key1" "value1" "key2" "value2" ...` |  The same as `dict` but with only string keys and can be used in `cembed`. Has`.Get "key"` and `.Set "key" "value"` methods that'll allow to capture or change value content from given key.  Example on using those methods in [Snippets](templates.md#miscellaneous-snippets). |
| `cslice value1 value2 ...` | Creates a slice \(similar to array\) that can be used elsewhere \(`cembed` and `sdict` for example\). |
| `cembed "list of embed values"` | Function to generate embed inside custom command. [More in-depth here](../others/custom-embeds.md#embeds-in-custom-commands).  |
| `in list value` | Returns true if value is in list. List can be either an array or a slice. |
| `inFold`  | Same as `in`, but is case insensitive. |
| `seq start stop` | Creates a new array of integer, starting from start and ending at stop. |
| `shuffle list` | Returns a shuffled version of a list. |
| `exec "command" "args" "args" "args" ...` | Executes a YAGPDB command \(e.g. reverse, roll, kick etc\) in a custom command. Exec can be run max 5 times per command. If real command returns an embed - exec will return raw data of type embed, so you can use embed fields for better formatting - e.g. `{{ $resp := exec "whois" }} {{ $resp.Title }} Joined at > {{ (index $resp.Fields 4).Value }}` will return the title \(username\#discriminator\) and "Joined at" field's value from `whois` command. |
| `execAdmin "command" "args" "args" "args" ...` | Functions same way as `exec` but will override any permission requirement \(such as the kick permission to use kick command etc.\). |
| `parseArgs required_args error_message ...carg` | Checks the arguments for a specific type. [More in depth here](../commands/custom-commands.md#require-arguments) and an example in [Custom Command Examples.](custom-command-examples.md#parseargs-example) |
| `carg "type" "name"` | Defines type of argument for parseArgs. [More in depth](../commands/custom-commands.md#require-arguments) here and an example in [Custom Command Examples.](custom-command-examples.md#parseargs-example) |
| `sleep seconds` | Pauses execution of template inside custom command for max 60 seconds. Argument`seconds`is of type integer. Example in [Snippets](templates.md#miscellaneous-snippets). |

### ExecCC

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>execCC ccID channel delay data</code>
      </td>
      <td style="text-align:left">Function that executes another custom command specified by <code>ccID,</code>max
        recursion depth is 2 (using <code>.StackDepth</code> shows the current depth)
        and it&apos;s rate-limited strictly at max 10 delayed custom commands executed
        per channel per minute, if you go over that it will be simply thrown away.
        Argument <code>channel</code> can be <code>nil</code>, channel&apos;s ID or
        name. The<code>delay</code> argument is execution delay of another CC is
        in seconds. The <code>data</code> argument is content that you pass to the
        other executed custom command. To retrieve that <code>data </code>you use <code>.ExecData</code>.
        This example is important - <a href="custom-command-examples.md#execcc-example">execCC example</a> also
        this snippet which shows you same thing run using the same custom command
        &gt; <a href="templates.md#this-sections-snippets-7">Snippets</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>scheduleUniqueCC ccID channel delay key data</code>
      </td>
      <td style="text-align:left">
        <p>Same as <code>execCC</code>except there can only be 1 scheduled cc execution
          per server per key, if key already exists then it is overwritten with the
          new data and delay.</p>
        <p>An example would be a mute command that schedules unmute in the future,
          but if you use the mute command again on the same user you dont want to
          schedule another unmute, you wanna overwrite the next unmute event to the
          new time, which is what this does.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>cancelScheduledUniqueCC ccID key</code>
      </td>
      <td style="text-align:left">Cancels a previously scheduled custom command execution using <code>scheduleUniqueCC </code>
      </td>
    </tr>
  </tbody>
</table>#### This section's snippets:

* To demonstrates execCC  and .ExecData using the same CC.

```go
{{ $yag := "YAGPDB rules! " }}
{{ $ctr := 0 }} {{ $yourCCID := toInt .CCID }}
{{ if .ExecData }}
    {{ $ctr = add .ExecData.number 1 }}
    {{ $yag = joinStr "" $yag $ctr }} {{ .ExecData.YAGPDB }}
{{ else }} 
    So, someone rules.
    {{ $ctr = add $ctr 1 }} {{ $yag = joinStr "" $yag 1 }}
{{ end }}
{{ if lt $ctr 5 }}
    {{ execCC $yourCCID nil 10 (sdict "YAGPDB" $yag "number" $ctr) }}
{{ else }} FUN'S OVER! {{ end }}
```

## Database

You have access to a basic set of Database functions, this is almost a key value store ordered by the key and value combined.

You can have max 50\*user\_count \(or 500\*user\_count for premium\) values in the database, if you go above this all new write functions will fail, this value is also cached so it won't be detected immediately when you go above nor immediately when you're under again.

Patterns are basic PostgreSQL patterns, not Regexp: An underscore `(_)`  matches any single character; a percent sign `(%)` matches any sequence of zero or more characters.

Keys can be max 256 bytes long and has to be strings or numbers. Values can be anything, but if they go above 100KB they will be truncated.

You can just pass a `userID`of 0 to make it global \(or any other number, but 0 is safe\).  
  
[Example here](custom-command-examples.md#database-example).

| Function | Description |
| :--- | :--- |
| `dbSet userID key value` | Sets the value for the specified key for the specified user to the specified value. |
| `dbSetExpire userID key value ttl` | Same as `dbSet` but with a expiration in seconds \(Note: This does not work with `dbIncr` atm\). |
| `dbIncr userID key incrBy`  | Increments the value for specified key for the specified user, if there was no value then it will be set to `incrBy .` Also returns the entry's current, increased value. |
| `dbGet userID key`  | Retrieves a value from the database for the specified user, this returns a DBEntry object. |
| `dbGetPattern userID pattern amount nSkip` | Retrieves up to`amount (max 100)`entries from the database in ascending order. |
| `dbGetPatternReverse userID pattern amount nSkip` | Retrieves up to`amount (max 100)`entries from the database in descending order. |
| `dbDel userID key` | Deletes the specified key for the specified value from the database. |
| `dbDelByID userID ID` | Deletes database entry by it's ID. |
| `dbTopEntries pattern amount nSkip` | Returns `amount (max 100)`top entries from the database, sorted by the value in a descending order. |
| `dbBottomEntries pattern amount nSkip` | Returns `amount (max 100)`top entries from the database, sorted by the value in a ascending order. |
| `dbCount (userID)` | Returns count of all database entries which are not expired, and if userID is given, only for that userID. |

### DBEntry

| Fields | Description |
| :--- | :--- |
| `ID` | ID of the entry. |
| `GuildID` | ID of the server. |
| `UserID` | ID of the user. |
| `CreatedAt` | When this entry was created. |
| `UpdatedAt` | When this entry was last updated. |
| `ExpiresAt` | When entry will expire. |
| `Key` | The key of the entry. |
| `Value` | The value of the entry. |

## Conditional branching

Branching using `if` pipeline and comparison operators - these operators don't need to be inside `if` branch. `if` statements always need to have an enclosing `end`.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Case</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">if</td>
      <td style="text-align:left">
        <p><code>{{ if (condition) }} output {{ end }}</code>
        </p>
        <p>Initialization statement can also be inside <code>if</code> statement with
          conditional statement, limiting the initialized scope to that <code>if</code> statement. <code>{{ if eq ($x := 42) 42 }} True {{ $x }} {{ end }}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">else if</td>
      <td style="text-align:left">
        <p><code>{{ if (condition) }} output1 {{ else if (condition) }} output2 {{ end }}</code>
        </p>
        <p>You can have as many<code>else if</code>statements as many different conditionals
          you have.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">else</td>
      <td style="text-align:left"><code>{{ if (condition) }} output1 {{ else }} output2 {{ end }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">not</td>
      <td style="text-align:left"><code>{{ if not (condition) }} output {{ end }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">and</td>
      <td style="text-align:left"><code>{{ if and (cond1) (cond2) (cond3) }} output {{ end }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">or</td>
      <td style="text-align:left"><code>{{ if or (cond1) (cond2) (cond3) }} output {{ end }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Equal: eq</td>
      <td style="text-align:left"><code>{{ if eq .Channel.ID ######## }} output {{ end }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Not equal: ne</td>
      <td style="text-align:left"><code>{{ $x := 7 }} {{ $y := 8 }} {{ ne $x $y }}</code> returns true</td>
    </tr>
    <tr>
      <td style="text-align:left">Less than: lt</td>
      <td style="text-align:left"><code>{{ if lt (len .Args) 5 }} output {{ end }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Less than or equal: le</td>
      <td style="text-align:left"><code>{{ $x := 7 }} {{ $y := 8 }} {{ le $x $y }}</code> returns true</td>
    </tr>
    <tr>
      <td style="text-align:left">Greater than: gt</td>
      <td style="text-align:left"><code>{{ if gt (len .Args) 1 }} output {{ end }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Greater than or equal: ge</td>
      <td style="text-align:left"><code>{{ $x := 7 }} {{ $y := 8 }} {{ ge $x $y }}</code> returns false</td>
    </tr>
  </tbody>
</table>## Range action

`range`iterates over element values in variety of data structures in pipeline - arrays, slices, maps or channels. The dot is set to successive elements of those data structures and output will follow execution. If the value of pipeline has zero length, nothing is output or if an `{{ else }}` action is used, that section will be executed.  
  
`range` on arrays and slices provides both the index and element for each entry; range on map iterates over key/element pairs. If a range action initializes a variable, that variable is set to the successive elements of the iteration. Range can also declare two variables, separated by a comma and set by index and element or key and element pair. In case of only one variable, it is assigned the element.  
  
Like `if`, `range`is concluded with`{{ end }}`action and declared variable scope inside `range` extends to that point.  


```go
{{/* range over a slice */}}
{{ range $index, $element := cslice "YAGPDB" "IS COOL!" }}
{{ $index }} : {{ $element }} {{ end }}
{{/* range on a map */}}
{{ range $key, $value := dict "SO" "SAY" "WE" "ALL!" }}
{{ $key }} : {{ $value }} {{ end }}
{{/* range with else and variable scope */}}
{{ range seq 1 1 }} no output {{ else }} output here {{ end }}
{{ $x := 42 }} {{ range $x := seq 2 4 }} {{ $x }} {{ end }} {{ $x }}
```

## Miscellaneous snippets

* `{{ if hasRoleName "funrole" }} Has role funrole {{ end }}`This will only show if the member has a role with name "funrole" .
* `{{ if gt (len .Args) 0 }} {{ index .Args 1 }} {{ end }}`Assuming your trigger is a command, will display your first input if input was given.
* `{{ if eq .Channel.ID ####### }} YAG! {{ end }}`Will only show `YAG!` in Channel \#\#\#\#\#.
* `{{ if ne .User.ID ####### }} YAG! {{ end }}`Will ignore if user ID equal to \#\#\#\#\# uses command.
* `{{ $d := randInt 10 }}` Store the random int into variable $d \(A random number from 0-9\).
* `{{ addReactions .CmdArgs }}` Adds the emoji following a trigger as reactions.
* `{{ $a := (exec "catfact") }}` Saves the response of the `catfact` ****command to variable `$a`. 
* `{{ $allArgs := (joinStr " " .CmdArgs) }}` Saves all the arguments after trigger to a variable `$allArgs`. 
* `{{/* this is a comment */}}`For commenting something inside a template, use this syntax.
* To demonstrate usage of sdict methods .Get and .Set.  &gt;  `{{ $x := sdict "key" "value" }} {{ $x.Get "key" }} {{ $x.Set "key" "eulav" }} {{ $x.Get "key" }}` to add to that `sdict`, simply use `.Set` again &gt;  `{{ $x.Set "YAGPDB" "is cool!" }} {{ $x }}`
* To demonstrate sleep and slightly also editMessage functions. &gt; `{{ $x := sendMessageRetID nil "Hello" }} {{ sleep 3 }} {{ editMessage nil $x "There" }} {{ sleep 5 }} {{ sendMessage nil "We all know, that" }} {{ sleep 3 }} YAGPDB rules!`

## How to get IDs <a id="how-to-get-ids"></a>

**User IDs:** Can be found by mentioning the user then adding a \ such as `\@jonas747#0001` . Alternatively if you have developer mode on, you can right click and select Copy ID. [How to enable developer mode in Discord](https://support.discordapp.com/hc/en-us/articles/206346498-Where-can-I-find-my-User-Server-Message-ID-).

**Channel IDs:** Can be found by mentioning the channel then adding a \ such as `\#announcements`. Alternatively if you have developer mode on, you can right click on the channel and select Copy ID.

**Role IDs**: Use the `listroles`command.

**Emote IDs:** 

If it is a **custom emote**, adding a \ in front of the emote such as `\:yag:` will display the name along with the ID such as  `<:yag:277569741932068864>`.

If it is an **animated emote**, do the same steps as a normal emote. If you do not have Discord Nitro, you can have a friend or a bot use the emote and right click on the emote to open its link. The ID will be a part of the URL.

If it is a **default emote**, look up the Unicode for the emote on Google. Note that some of the more customized default emotes such as some of the family emotes will not work in any of the YAGPDB commands. 

