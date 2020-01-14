# Templates

"Go is all about type... Type is life." // William Kennedy

All available data that can be used in YAGPDB's templating "engine" which is slightly modified version of Golang's stdlib text/template package; more in depth and info about actions, pipelines and global functions like `printf, index, len`etc &gt; [https://golang.org/pkg/text/template/](https://golang.org/pkg/text/template/)

{% hint style="warning" %}
**Put curly brackets around the data you want to formulate as template** like this: `{{.User.Username}}`

This `{{ ... }}` syntax of having two curly brackets aka braces around context is always necessary to form a template's control structure with methods and functions stated below.
{% endhint %}

{% hint style="warning" %}
Data passed around template pipeline can be initialized as a variable to capture it &gt; \(_in EBNF syntax\)_ $variable `:=` value. Previously declared variable can also be assigned with new data &gt; $variable `=` value, it has to have a whitespace before it or control panel will error out. Variable scope extends to the `{{end}}` action of the control structure.
{% endhint %}

{% hint style="info" %}
If you want to join different data objects \(e.g. to wrap toString in joinStr around .Guild.MemberCount\), you use round brackets aka parentheses as delimiters:  
`{{joinStr "" "Our member count is " (toString .Guild.MemberCount) "!"}}`
{% endhint %}

{% hint style="info" %}
Templating system uses standard ASCII quotation marks:  
0x22 &gt; `"` for straight double quotes, 0x27 &gt; `'`for apostrophes and 0x60 ````` for backticks;   
so make sure no "smart-quotes" are being used.
{% endhint %}

{% hint style="success" %}
Everything in Go is passed by value \(even errors\) as in C and in all languages descending from C. Values are carried by types.  
Many problems start with different kinds of type user has as value and what is needed for argument. YAGPDB usually states that in error message - what went wrong with type e.g. `CC #42:24:123 ... error calling lt: incompatible types for comparison` tells you that CC \#42 has an error on line 24 and at entry point position 123 due to different types presented for comparison action.  
  
To see of what type a variable or function's return is, use printf "%T", for example &gt; `{{printf "%T" currentTime}}` will output the type `time.Time`.
{% endhint %}

## The Dot

The dot `{{ . }}`  encompasses all active data available for templating system.   
From official docs &gt; "Execution of the template walks the structure and sets the cursor, represented by a period '.' and called "dot", to the value at the current location in the structure as execution proceeds." All following fields/methods/objects like `User/Guild/Member/Channel etc` are all part of that dot-structure and there are some more in tables below.

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
        <p><code>{{(userArg .User.ID).Mention}}</code> mentions triggering user. Explained
          more in <a href="templates.md#this-sections-snippets">this section&apos;s snippets</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>pastUsernames userID offset</code>
      </td>
      <td style="text-align:left">
        <p>Returns a slice of type <code>[ ]*logs.CCNameChange</code> having fields <code>.Name</code> and <code>.Time</code> of
          previous 15 usernames and skips <code>offset</code> number in that list.</p>
        <p><code>{{range pastUsernames .User.ID 0}} <br />{{.Name}} - {{.Time.Format &quot;Jan _2 2006&quot;}} <br />{{end}}</code> 
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>pastNicknames userID offset</code>
      </td>
      <td style="text-align:left">Same as <code>pastUsernames</code>.</td>
    </tr>
  </tbody>
</table>[User object in Discord documentation](https://discordapp.com/developers/docs/resources/user#user-object).

#### This section's snippets:

`{{(userArg .Guild.OwnerID).String}}` this template returns Guild/Server owner's username and discriminator as of type string. First, `userArg` function is given `.Guild.OwnerID` as argument \(what it does, explained below\). The parentheses surrounding them make `userArg` function's return `.User` as .User object which is handled further by `.String` method \(ref`.User.String`\), giving a result like &gt; YAGPDB\#8760.

## Guild / Server

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

[Guild object in Discord documentation](https://discordapp.com/developers/docs/resources/guild#guild-object).

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
      <td style="text-align:left"><code>editNickname &quot;newNick&quot;</code>
      </td>
      <td style="text-align:left">Edits triggering user&apos;s nickname, argument has to be of type string.
        YAGPDB must be above the roles user&apos;s having.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>getMember</code>
      </td>
      <td style="text-align:left">
        <p>Function returns Member object having above methods.</p>
        <p><code>{{(getMember .User.ID).JoinedAt}}</code> 
          <br />is the same as <code>{{.Member.JoinedAt}}</code>
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
</table>[Member object in Discord documentation](https://discordapp.com/developers/docs/resources/guild#guild-member-object).

## Channel

| Field | Description |
| :--- | :--- |
| .Channel.Name | The Name of the channel. |
| .Channel.ID | The ID of the channel. |
| .Channel.ParentID | The ID of the channel's parent \(category\), returns 0 if none. |
| .Channel.Topic | The Topic of the channel. |
| .Channel.NSFW | Outputs whether this channel is NSFW or not. |

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>editChannelName <br />channel &quot;newName&quot;</code>
      </td>
      <td style="text-align:left">Function edits channel&apos;s name. <code>channel</code> can be either ID,
        &quot;name&quot; or even <code>nil</code> if triggered in that channel name
        change is intended to happen. <code>&quot;newName&quot;</code> has to be
        of type string. For example &gt;<code>{{editChannelName nil (joinStr &quot;&quot; &quot;YAG - &quot; (randInt 1000))}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>editChannelTopic channel &quot;newTopic&quot;</code>
      </td>
      <td style="text-align:left">
        <p>Function edits channel&apos;s topic/description. <code>channel</code> can
          be either ID, &quot;name&quot; or even <code>nil</code> if triggered in that
          channel name change is intended to happen. <code>&quot;newTopic&quot;</code> has
          to be of type string. For example &gt;</p>
        <p><code>{{editChannelTopic nil &quot;YAG is cool&quot;}}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>getChannel channel</code>
      </td>
      <td style="text-align:left">Function returns full channel object of given <code>channel</code> argument
        which can be either it&apos;s ID, name or <code>nil</code> for triggering
        channel, and is of type *dstate.ChannelState. For example &gt; <code>{{(getChannel nil).Name}}</code> returns
        the name of the channel command was triggered in.</td>
    </tr>
  </tbody>
</table>[Channel object in Discord documentation](https://discordapp.com/developers/docs/resources/channel#channel-object).

## Message

| Field | Description |
| :--- | :--- |
| .Message.ID | ID of the message. |
| .Message.ChannelID | Channel ID this message is in. |
| .Message.GuildID | Guild ID in which the message is. |
| .Message.Content | Text content on this message. |
| .Message.Timestamp | Timestamp of the message in type timestamp \(use .Message.Timestamp.Parse to get type time and .Parse.String method returns type string\). |
| .Message.EditedTimestamp | The time at which the last edit of the message occurred, if it has been edited. |
| .Message.MentionRoles | The roles mentioned in the message. |
| .Message.MentionEveryone | Whether the message mentions everyone. |
| .Message.Author | Author of the message \([User](templates.md#user) object\). |
| .Message.Attachments | Attachments to this message \(slice of attachment objects\). |
| .Message.Embeds | Embeds on this message \(slice of embed objects\). |
| .Message.Mentions | Users this message mentions. |
| .Message.Reactions | Reactions on this message \(only available from getMessage\). |
| .Message.Type | The [type](https://discordapp.com/developers/docs/resources/channel#message-object-message-types) of the message. |
| .Args | List of everything that is passed to .Message.Content. .Args is a slice of type string. |
| .Cmd | .Cmd is of type string and shows all arguments that trigger custom command, part of .Args. Starting from `{{index .Args 0}}`.  |
| .CmdArgs | List of all the arguments passed after `.Cmd` \(`.Cmd` is the actual trigger\) `.CmdArgs` is a slice of type string. Examples in [misc. snippets](templates.md#miscellaneous-snippets). |
| .StrippedMsg | "Strips" or cuts off the triggering part of the message and prints out everything else after that. Bare in mind, when using regex as trigger, for example `"day"` and input message is `"Have a nice day my dear YAG!"` output will be `"my dear YAG!"`  - rest is cut off. |

[Message object in Discord documentation](https://discordapp.com/developers/docs/resources/channel#message-object).

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
        <p><code>{{range .ReactionMessage.Reactions}}<br />{{.Count}} - {{.Emoji.Name}} <br />{{end}}</code>
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
</table>[Reaction object in Discord documentation](https://discordapp.com/developers/docs/resources/channel#reaction-object).

## Time

Time in general uses Golang's time package library &gt; [https://golang.org/pkg/time/\#time](https://golang.org/pkg/time/#Time) and also this although slightly different syntax all applies here &gt; [https://gobyexample.com/time](https://gobyexample.com/time).

| Field | Description |
| :--- | :--- |
| .TimeHour | Variable of time.Duration type and returns 1 hour &gt; `1h0m0s`. |
| .TimeMinute | Variable of time.Duration type and returns 1 minute &gt; `1m0s`. |
| .TimeSecond | Variable of time.Duration type and returns 1 second &gt; `1s`. |

| Function | Description |
| :--- | :--- |
| `currentTime` | Gets the current time, value is of type time; which can be used in a custom embed. More info [here](../commands/custom-commands.md#currenttime-template). |
| `formatTime Time "arg"` | Outputs given time in RFC822 formatting, first argument `Time` shows it needs to be of type time, also with extra layout if second argument is given - e.g. `{{formatTime currentUserCreated "3:04PM"}}` would output `11:22AM` if that would have been user's creating time. |
| `humanizeDurationHours` | Returns given integer or time.Duration argument in nanoseconds in human readable format - as how long it would take to get towards given time - e.g. `{{humanizeDurationHours 9000000000000000000}}` returns `285 years 20 weeks 6 days and 16 hours`. More in [snippets](templates.md#this-sections-snippets). |
| `humanizeDurationMinutes` | Sames as `humanizeDurationHours`, this time duration is returned in minutes - e.g. `{{humanizeDurationMinutes 3500000000000}}` would return `58 minutes`. |
| `humanizeDurationSeconds` | Sames as both humanize functions above, this time duration is returned in seconds - e.g. `{{humanizeDurationSeconds 3500000000000}}` would return `58 minutes and 20 seconds`. |
| `humanizeTimeSinceDays` | Returns time has passed since given argument of type Time in human readable format - e.g. `{{humanizeTimeSinceDays currentUserCreated}}` |
| `newDate year month day hour minute second` | Returns new time object in UTC using following syntax... all arguments need to be of type int, for example &gt; `{{humanizeDurationHours ((newDate 2059 1 2 12 34 56).Sub currentTime)}}` will give you how much time till year 2059 January 2nd 12:34:56. More examples in [snippets](templates.md#this-sections-snippets).  |

#### This section's snippets:

* To demonstrate humanizeDurationHours and also how to parse a timestamp, output will be like `whois` command shows user's _join server age_. `{{humanizeDurationHours (currentTime.Sub .Member.JoinedAt.Parse)}}`
* To demonstrate newDate to get Epoch times. `{{$unixEpoch := newDate 1970 1 1 0 0 0}} in seconds > {{$unixEpoch.Unix}} {{$discordEpoch := newDate 2015 1 1 0 0 0}} in seconds > {{$discordEpoch.Unix}}`

## Functions

Functions are underappreciated. In general, not just in templates. // Rob Pike

### Type conversion

| Function | Description |
| :--- | :--- |
| `toString` | Converts something into a string. Usage: `(toString x)`. |
| `toInt` | Converts something into an integer. Usage: `(toInt x)`. |
| `toInt64` | Converts something into an int64. Usage: `(toInt64 x)`. |
| `toFloat` | Converts argument \(number or string form of a number\) to type float64.  Usage: `(toFloat x)`. |
| `toDuration` | Converts the argument, number or string to type Duration. Number represents nanoseconds. String can be with time modifier \(second, minute, hour, day etc\) `s, m, h, d, w, mo, y`,without a modifier string will be converted to minutes. Usage:`(toDuration x)`. Example in section's [Snippets](templates.md#this-sections-snippets-1).  |
| `json value` | Traverses given `value` through MarshalJSON \([more here](%20https://golang.org/pkg/encoding/json/#Marshal)\) and returns it as type string. For example `{{ json .TimeHour }}` outputs type string; before this `.TimeHour` was of type time.Duration. Basically it's good to use if multistep type conversion is needed `(toString (toInt value) )` and certain parts of `cembed` need this for example. |

#### This section's snippets:

* To demonstrate toDuration, outputs 12 hours from current time in UTC. `{{(currentTime.Add (toDuration (mult 12 .TimeHour))).Format "15:04"}}`is the same as`{{(currentTime.Add (toDuration "12h")).Format "15:04"}}` or`{{(currentTime.Add (toDuration 43200000000000)).Format "15:04"}}`

### String manipulation

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>joinStr &quot;separator&quot; &quot;str1&quot; (arg1)(arg2) &quot;str2&quot; ...</code>
      </td>
      <td style="text-align:left">Joins several strings into one, separated by the first arg<code>&quot;separator&quot;</code>,
        useful for executing commands in templates (e.g.<code>{{joinStr &quot;&quot; &quot;1&quot; &quot;2&quot; &quot;3&quot;}}</code> returns <code>123</code>).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>lower &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Converts the string to lowercase.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>upper &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Converts the string to uppercase.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>slice &quot;string&quot;|slice integer (integer2)</code>
      </td>
      <td style="text-align:left">
        <p>Function&apos;s first argument must be of type string or slice.</p>
        <p>Outputs the &quot;string&quot; after cutting/slicing off integer (numeric)
          value of symbols (actually starting the string&apos;s index from integer
          through integer2) - e.g. <code>{{slice &quot;Fox runs&quot; 2}}</code>outputs <code>x runs</code>.
          When using also integer2 - e.g. <code>{{slice &quot;Fox runs&quot; 1 7}}</code>,
          it outputs <code>ox run</code>. For slicing whole arguments, let&apos;s
          say words, see example in section&apos;s <a href="templates.md#this-sections-snippets-2">Snippets</a>.</p>
        <p></p>
        <p>This<code> slice</code> function is not the same as basic dynamically-sized
          slice data type discussed in this reference doc.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>urlescape &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Escapes the string so it can be safely placed inside a URL path segment
        - e.g. &quot;Hello, YAGPDB!&quot; becomes &quot;Hello%2C%20YAGPDB%21&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>split &quot;string&quot; &quot;sepr&quot;</code>
      </td>
      <td style="text-align:left">Splits given <code>&quot;string&quot;</code> to substrings separated by <code>&quot;sepr&quot;</code>arg
        and returns new slice of the substrings between given separator e.g. <code>{{split &quot;YAG, is cool!&quot; &quot;,&quot;}}</code> returns <code>[YAG  is cool!]</code> slice
        where <code>YAG</code> is at index 0 and <code>is cool!</code> at index 1.
        Example also in section&apos;s <a href="templates.md#this-sections-snippets-2">Snippets</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>title &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Returns string with the first letter of each word capitalized.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>reFind &quot;regex&quot; &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Compares string to regex pattern and returns first match. <code>{{reFind &quot;AG&quot; &quot;YAGPDB is cool!&quot;}}</code>returns <code>AG</code> (regex
        pattern is case sensitive).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>reFindAll &quot;regex&quot; &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Adds all regex matches from the string to a slice. Example in section&apos;s
        <a
        href="templates.md#this-sections-snippets-2">Snippets</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>reFindAllSubmatches &quot;regex&quot; &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Returns whole-pattern matches and also the sub-matches within those matches
        as slices inside a slice. <code>{{reFindAllSubmatches &quot;(?i)y([a-z]+)g&quot; &quot;youngish YAGPDB&quot;}} </code>returns<code> [[young oun] [YAG A]] </code>(regex
        pattern here is case insensitive).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>reReplace &quot;regex&quot; &quot;string1&quot; &quot;string2&quot;</code>
      </td>
      <td style="text-align:left">Replaces string1 contents with string2 at regex match point. <code>{{reReplace &quot;I am&quot; &quot;I am cool!&quot; &quot;YAGPDB is&quot;}}</code>returns <code> YAGPDB is cool!</code> (regex
        pattern here is case sensitive).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>print, printf, println</code>
      </td>
      <td style="text-align:left">These are template package&apos;s predefined functions and are aliases
        for <a href="https://golang.org/pkg/fmt/#Sprint">fmt.Sprint</a>, <a href="https://golang.org/pkg/fmt/#Sprint">fmt.Sprintf</a> and
        <a
        href="https://golang.org/pkg/fmt/#Sprintln">fmt.Sprintln</a>. Formatting is also discussed <a href="https://golang.org/pkg/fmt/#hdr-Printing">here</a>.
          <br
          /><code>printf</code> is usable for example to determine the type of the
          value &gt; <code>{{printf &quot;%T&quot; currentTime}} </code>outputs <code>currentTime </code>functions
          output value type of<code> time.Time</code>.</td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
Special information we can include in the string is _escape sequences_. Escape sequences are two \(or more\) characters, the first of which is a backslash `\`, which gives the remaining characters special meaning - let's call them metacharacters. The most common escape sequence you will encounter is `\n`, which means "newline". 
{% endhint %}

{% hint style="info" %}
With regular expression patterns - when using quotes you have to "double-escape" metacharacters starting with backslash or use backquotes/ticks to simplify this. `{{reFind "\\d+" (toString 42)}}` versus ``{{reFind `\d+` (toString 42)}}``
{% endhint %}

#### This section's snippets:

* `{{$args:= (joinStr " " (slice .CmdArgs 1))}}` Saves all the arguments except the first one to a variable `$args`. 
* To demonstrate usage of split function. &gt; `{{$x := "Hello, World, YAGPDB, here!"}} {{range $k, $v := (split $x ", ")}}Word {{$k}}: __{{$v}}__ {{end}}`
* To demonstrate usage of reFindAll. &gt;  `Before regex: {{$msg := "1 YAGPDB and over 100000 servers conqured."}} {{$re2 := reFindAll "[0-9]+" $msg}} {{$msg}}   After regex matches: {{joinStr " " "Only" (index $re2 0) "YAGPDB and already" (index $re2 1) "servers captured."}}`

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
      <td style="text-align:left">Returns x + y + z + ..., detects first number type; is it integer or float
        and based on that adds. (use <code>toFloat</code> on the first argument to
        force floating point math.)<code>{{add 5 4 3 2 -1}}</code> sums all these
        numbers and returns <code>13</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sub x y z ...</code>
      </td>
      <td style="text-align:left">Returns x - y -z - ... Works like add, just subtracts.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>mult x y z ...</code>
      </td>
      <td style="text-align:left">Multiplication, like <code>add</code> or <code>div</code>, detects first
        number type. <code>{{mult 3.14 2}}</code> returns <code>6.28</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>div x y z ...</code>
      </td>
      <td style="text-align:left">Division, like <code>add</code> or <code>mult</code>, detects number type
        first. <code>{{div 11 3}}</code> returns <code>3</code> whereas <code>{{div 11.1 3}}</code> returns <code>3.6999999999999997</code>
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
        <p>Result will be <code>start &lt;= random number &lt; stop</code>. Example
          in section&apos;s <a href="templates.md#this-sections-snippets-3">Snippets</a>.</p>
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
        up. <code>{{roundCeil 1.1}}</code> returns <code>2</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>roundFloor</code>
      </td>
      <td style="text-align:left">Returns the greatest integer value less than or equal to input or rounds
        down. <code>{{roundFloor 1.9}}</code> returns <code>1</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>roundEven </code>
      </td>
      <td style="text-align:left">Returns the nearest integer, rounding ties to even.
        <br /><code>{{roundEven 10.5}}</code> returns <code>10 {{roundEven 11.5}}</code> returns <code>12</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sqrt</code>
      </td>
      <td style="text-align:left">Returns the square root of a number as type float64.
        <br /><code>{{sqrt 49}}</code> returns <code>7, {{sqrt 12.34 | printf &quot;%.4f&quot;}} returns 3.5128</code>
      </td>
    </tr>
  </tbody>
</table>#### This section's snippets:

* `{{$d := randInt 10}}` Stores random int into variable `$d` \(a random number from 0-9\).
* To demonstrate rounding float to 2 decimal places. `{{div (round (mult 12.3456 100)) 100}}` returns 12.35 `{{div (roundFloor (mult  12.3456 100)) 100}}` returns 12.34

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
| `addReactions "👍" "👎" ...` | Adds each emoji as a reaction to the message that triggered the command \(recognizes Unicode emojis and `emojiname:emojiid`\). |
| `addResponseReactions "👍" "👎" ...` | Adds each emoji as a reaction to the response message \(recognizes Unicode emojis and `emojiname:emojiid`\). |
| `addMessageReactions channel messageID reactions` | Same as `addReactions` or `addResponseReactions`, but can be used on any messages using its ID. Channel can be either `nil`, channelID or channel's name. Example in section's [Snippets](templates.md#this-sections-snippets-4). |
| `deleteAllMessageReactions channel messageID` | Deletes all reactions pointed message has. `channel` can be ID, "name" or `nil`. |

#### This section's snippets:

* Sends message to current channel `nil` and gets messageID to variable `$x`. Also adds reactions to this message. After 5 seconds, deletes that message. &gt;

  `{{$x := sendMessageRetID nil "Hello there!"}} {{addMessageReactions nil $x "👍" "👎"}} {{deleteMessage nil $x 5}}`

* To demonstrate sleep and slightly also editMessage functions. &gt; `{{$x := sendMessageRetID nil "Hello"}} {{sleep 3}} {{editMessage nil $x "There"}} {{sleep 5}} {{sendMessage nil "We all know, that"}} {{sleep 3}} YAGPDB rules!`

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

* `<@{{.User.ID}}>` Outputs a mention to the user that called the command and is the same as `{{.User.Mention}}`
* `<@###########>` Mentions the user that has the ID \#\#\#\#\#\# \(See [How to get IDs](templates.md#how-to-get-ids) to get ID\).
* `<#&&&&&&&&&&&>` Mentions the channel that has ID &&&&&& \(See [How to get IDs](templates.md#how-to-get-ids) to get ID\).
* `<@&##########>` Mentions the role with ID \#\#\#\#\#\#\#\# \([lis~~t~~roles](../commands/all-commands.md#listroles) command gives roleIDs\). This is usable for example with `{{sendMessageNoEscape nil "Welcome to role <@&11111111...>"}}`. Mentioning that role has to be enabled server- side in Discord.
* To demonstrate usage of escapeEveryoneHere. &gt; `{{$x := "@here Hello World! @everyone"}} {{sendMessage nil $x}} {{sendMessageNoEscape nil $x}} {{sendMessageNoEscape nil (escapeEveryoneHere $x)}}`

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

* To demonstrate usage of targetHasRoleID. &gt;  `{{$x := (userArg (index .Args 1)).ID}} {{if targetHasRoleID $x ############}} Has the Role! {{else}} Does not have the role! {{end}}`

### Current User

| Function | Description |
| :--- | :--- |
| `currentUserCreated` |  Returns value of type time and shows when the current user was created. |
| `currentUserAgeHuman` |  The account age of the current user in more human readable format  \(Eg:`3 days 2 hours`\). |
| `currentUserAgeMinutes` |  The account age of the current user in minutes. |

### Miscellaneous

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>adjective</code>
      </td>
      <td style="text-align:left">Returns a random adjective.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>range slice/array</code>
      </td>
      <td style="text-align:left">Iterates (loops) over the given slice or array and sets successive elements
        as active data (the dot) to be further handled inside the range template.
        Example usage <a href="custom-command-examples.md#range-example">here</a>.
        <a
        href="templates.md#range-action">More in-depth here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>dict key1 value1 key2 value2 ...</code>
      </td>
      <td style="text-align:left">Creates an unordered collection of key-value pairs, a dictionary so to
        say. The number of parameters to form key-value pairs must be even.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sdict &quot;key1&quot; &quot;value1&quot; &quot;key2&quot; &quot;value2&quot; ...</code>
      </td>
      <td style="text-align:left">The same as <code>dict</code> but with only string keys and can be used
        in <code>cembed</code>. Has<code>.Get &quot;key&quot;</code>, <code>.Del &quot;key&quot; </code>and<code> .Set &quot;key&quot; &quot;value&quot; </code>methods
        that&apos;ll allow to capture, delete or change value&apos;s content for
        given key. Example on using those methods in <a href="templates.md#miscellaneous-snippets">Snippets</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>cslice value1 value2 ...</code>
      </td>
      <td style="text-align:left">Creates a slice (similar to array) that can be used elsewhere (<code>cembed</code> and <code>sdict</code> for
        example).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>cembed &quot;list of embed values&quot;</code>
      </td>
      <td style="text-align:left">Function to generate embed inside custom command. <a href="../others/custom-embeds.md#embeds-in-custom-commands">More in-depth here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>in list value</code>
      </td>
      <td style="text-align:left">Returns boolean true/false whether case-sensitive value is in list/slice. <code>{{ in (cslice &quot;YAGPDB&quot; &quot;is cool&quot;) &quot;yagpdb&quot; }}</code> returns <code>false</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>inFold </code>
      </td>
      <td style="text-align:left">Same as <code>in</code>, but is case-insensitive. <code>{{inFold (cslice &quot;YAGPDB&quot; &quot;is cool&quot;) &quot;yagpdb&quot;}}</code> returns <code>true</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>seq start stop</code>
      </td>
      <td style="text-align:left">Creates a new slice of type integer, beginning from start number, increasing
        in sequence and ending at stop (not included). <code>{{seq -4 2}}</code> returns
        a slice <code>[ -4 -3 -2 0 1 ]</code>. Sequence&apos;s max length is 10
        000.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>shuffle list</code>
      </td>
      <td style="text-align:left">Returns a shuffled, randomized version of a list/slice.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>exec &quot;command&quot; &quot;args&quot; &quot;args&quot; &quot;args&quot; ...</code>
      </td>
      <td style="text-align:left">
        <p>Executes a YAGPDB command (e.g. roll, kick etc) in a custom command. Exec
          can be run max 5 times per command. If real command returns an embed -
          exec will return raw data of type embed, so you can use embed fields for
          better formatting - e.g. <code>{{$resp := exec &quot;whois&quot;}} {{$resp.Title}} Joined at &gt; {{(index $resp.Fields 4).Value}}</code> will
          return the title (username#discriminator) and &quot;Joined at&quot; field&apos;s
          value from <code>whois</code> command. <b>NB!</b> This will not work for un/nn
          commands!</p>
        <p></p>
        <p>exec syntax is <code>exec &quot;command&quot; arguments</code> - this means
          you format it the same way as you would type the command regularly, just
          without the prefix, e.g. if you want to clear 2 messages and avoiding the
          pinned message &gt; <code>{{exec &quot;clear 2 -nopin&quot;}}</code>, where <code>&quot;command&quot;</code> part
          is whole <code>&quot;clear 2 -nopin&quot;</code>. If you change that number
          inside CC somewhere then you have to use <code>arguments</code> part of exec
          formatting &gt; <code>{{$x := 2}} {{exec &quot;clear&quot; $x &quot;-nopin&quot;}}</code> Here <code>&quot;clear&quot;</code> is
          the <code>&quot;command&quot;</code> and it is followed by <code>arguments</code>,
          one variable <code>$x</code> and one string <code>&quot;-nopin&quot;</code>.
          Last template is the same as <code>{{exec (joinStr &quot; &quot; &quot;clear&quot; $x &quot;-nopin&quot;)}}</code>(also
          notice the space in joinStr separator).</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>execAdmin &quot;command&quot; &quot;args&quot; &quot;args&quot; &quot;args&quot; ...</code>
      </td>
      <td style="text-align:left">Functions same way as <code>exec</code> but will override any permission
        requirement (such as the kick permission to use kick command etc.).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>parseArgs required_args error_message ...carg</code>
      </td>
      <td style="text-align:left">Checks the arguments for a specific type. Has methods <code>.Get</code> and <code>.IsSet</code>.
        <a
        href="../commands/custom-commands.md#require-arguments">More in depth here</a>and example in <a href="custom-command-examples.md#parseargs-example">Custom Command Examples.</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>carg &quot;type&quot; &quot;name&quot;</code>
      </td>
      <td style="text-align:left">Defines type of argument for parseArgs. <a href="../commands/custom-commands.md#require-arguments">More in depth</a> here
        and an example in <a href="custom-command-examples.md#parseargs-example">Custom Command Examples.</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sleep seconds</code>
      </td>
      <td style="text-align:left">Pauses execution of template inside custom command for max 60 seconds
        combined. Argument<code>seconds</code>is of type integer. Example in
        <a
        href="templates.md#miscellaneous-snippets">Snippets</a>.</td>
    </tr>
  </tbody>
</table>### ExecCC

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
        This example is important &gt; <a href="https://docs.yagpdb.xyz/reference/custom-command-examples#countdown-example-exec-cc">execCC example</a> also
        next snippet which shows you same thing run using the same custom command
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
{{ $ctr := 0 }} {{ $yourCCID := .CCID }}
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

You can have max 50 \* user\_count \(or 500 \* user\_count for premium\) values in the database, if you go above this all new write functions will fail, this value is also cached so it won't be detected immediately when you go above nor immediately when you're under again.

Patterns are basic PostgreSQL patterns, not Regexp: An underscore `(_)`  matches any single character; a percent sign `(%)` matches any sequence of zero or more characters.

Keys can be max 256 bytes long and has to be strings or numbers. Values can be anything, but if they go above 100KB they will be truncated.

You can just pass a `userID`of 0 to make it global \(or any other number, but 0 is safe\).  
  
There can be 10 database interactions per CC, out of which dbTop/BottomEntries, dbCount and dbGetPattern may be only run once \(50,10 for premium users\).  
  
[Example here](custom-command-examples.md#database-example).

| Function | Description |
| :--- | :--- |
| `dbSet userID key value` | Sets the value for the specified `key` for the specific `userID` to the specified `value`. `userID` can be any number of type int64.    Values are stored either as of type float64 \(for numbers or hex\) or as varying type in bytes \(for slices, maps, strings etc\) depending on input argument. |
| `dbSetExpire userID key value ttl` | Same as `dbSet` but with an expiration in seconds \(Note: This does not work with `dbIncr` atm\). |
| `dbIncr userID key incrBy`  | Increments the value for specified key for the specified user, if there was no value then it will be set to `incrBy .` Also returns the entry's current, increased value. |
| `dbGet userID key`  | Retrieves a value from the database for the specified user, this returns DBEntry object. |
| `dbGetPattern userID pattern amount nSkip` | Retrieves up to`amount (max 100)`entries from the database in ascending order. |
| `dbGetPatternReverse userID pattern amount nSkip` | Retrieves`amount (max 100)`entries from the database in descending order. |
| `dbDel userID key` | Deletes the specified key for the specified value from the database. |
| `dbDelByID userID ID` | Deletes database entry by it's ID. |
| `dbTopEntries pattern amount nSkip` | Returns `amount (max 100)`top entries from the database, sorted by the value in a descending order. |
| `dbBottomEntries pattern amount nSkip` | Returns `amount (max 100)`top entries from the database, sorted by the value in a ascending order. |
| `dbCount (userID|key)` | Returns the count of all database entries which are not expired. Optional arguments: if `userID` is given, counts entries for that userID or if `key`, then only those keys are counted. |

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

Branching using `if` action's pipeline and comparison operators - these operators don't need to be inside `if` branch. `if` statements always need to have an enclosing `end`.

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
        <p><code>{{if (condition)}} output {{end}}</code>
        </p>
        <p>Initialization statement can also be inside <code>if</code> statement with
          conditional statement, limiting the initialized scope to that <code>if</code> statement.
          <br
          /><code>{{$x := 24}} <br />{{if eq ($x := 42) 42}} Inside: {{$x}} {{end}} <br />Outside: {{$x}}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">else if</td>
      <td style="text-align:left">
        <p><code>{{if (condition)}} output1 {{else if (condition)}} output2 {{end}}</code>
        </p>
        <p>You can have as many<code>else if</code>statements as many different conditionals
          you have.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">else</td>
      <td style="text-align:left"><code>{{if (condition)}} output1 {{else}} output2 {{end}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">not</td>
      <td style="text-align:left"><code>{{if not (condition)}} output {{end}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">and</td>
      <td style="text-align:left"><code>{{if and (cond1) (cond2) (cond3)}} output {{end}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">or</td>
      <td style="text-align:left"><code>{{if or (cond1) (cond2) (cond3)}} output {{end}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Equal: eq</td>
      <td style="text-align:left"><code>{{if eq .Channel.ID ########}} output {{end}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Not equal: ne</td>
      <td style="text-align:left"><code>{{$x := 7}} {{$y := 8}} {{ne $x $y}}</code> returns true</td>
    </tr>
    <tr>
      <td style="text-align:left">Less than: lt</td>
      <td style="text-align:left"><code>{{if lt (len .Args) 5}} output {{end}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Less than or equal: le</td>
      <td style="text-align:left"><code>{{$x := 7}} {{$y := 8}} {{le $x $y}}</code> returns true</td>
    </tr>
    <tr>
      <td style="text-align:left">Greater than: gt</td>
      <td style="text-align:left"><code>{{if gt (len .Args) 1}} output {{end}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Greater than or equal: ge</td>
      <td style="text-align:left"><code>{{$x := 7}} {{$y := 8}} {{ge $x $y}}</code> returns false</td>
    </tr>
  </tbody>
</table>## Range action

`range`iterates over element values in variety of data structures in pipeline - slices/arrays, maps or channels. The dot `.` is set to successive elements of those data structures and output will follow execution. If the value of pipeline has zero length, nothing is output or if an `{{else}}` action is used, that section will be executed.  
  
`range` on slices/arrays provides both the index and element for each entry; range on map iterates over key/element pairs. If a range action initializes a variable, that variable is set to the successive elements of the iteration. Range can also declare two variables, separated by a comma and set by index and element or key and element pair. In case of only one variable, it is assigned the element.  
  
Like `if`, `range`is concluded with`{{end}}`action and declared variable scope inside `range` extends to that point.  


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

## With action

`with` lets you assign and carry pipeline value with its type as a dot `.` inside that control structure, it's like a shorthand. If the value of the pipeline is empty, dot is unaffected and when `{{else}}` is used, that branch is executed instead.   
  
Affected dot inside `with` is important because methods mentioned above in this documentation:`.Server.ID`, `.Message.Content` etc are all already using the dot on the pipeline and if they are not carried over to the `with` control structure, these fields do not exists and template will error out.

Like `if` and `range` actions, `with` is concluded using `{{end}}` and variable scope extends to that point.

```go
{{/* Shows the scope and how dot is affected by object's value in pipeline */}}
{{ $x := "42" }} {{ with and ($z:= seq 0 5) ($x := seq 0 10) }} 
len $x: `{{ len $x }}` 
same as len dot: `{{ len . }}` {{/* "and" function uses $x as last value for dot */}}
but len $z is `{{ len $z }}` {{ end }}
Outer-scope $x len however: {{ len $x }}
{{/* when there's no value, dot is unaffected */}}
{{ with false }} dot is unaffected {{ else }} printing here {{ .CCID }} {{ end }}
```

## Miscellaneous snippets

* `{{if hasRoleName "funrole"}} Has role funrole {{end}}`This will only respond if the member has a role with name "funrole" .
* `{{if gt (len .Args) 0}} {{index .Args 1}} {{end}}`Assuming your trigger is a command, will display your first input if input was given.
* `{{if eq .Channel.ID #######}} YAG! {{end}}`Will only show `YAG!` if ChannelID is \#\#\#\#\#.
* `{{if ne .User.ID #######}} YAG! {{end}}`Will ignore if user ID equal to \#\#\#\#\# uses command.
* `{{addReactions .CmdArgs}}` Adds the emoji following a trigger as reactions.
* `{{$a := (exec "catfact")}}` Saves the response of the `catfact` ****command to variable `$a`. 
* `{{$allArgs := (joinStr " " .CmdArgs)}}` Saves all the arguments after trigger to a variable `$allArgs`. 
* `{{/* this is a comment */}}`For commenting something inside a template, use this syntax. May contain newlines. Comments do not nest and they start and end at the the delimiters. 
* To trim spaces, for example &gt;`{{- /* this is a multi-line  comment with white space trimmed from  preceding and following text */ -}}` Using`{{- ... -}}` is also handy inside`range` actions, because white spaces and newlines are rendered there as output.
* To demonstrate usage of sdict methods .Get .Set .Del.  &gt;  `{{$x := sdict "key" "value"}} {{$x.Get "key"}} {{$x.Set "key" "eulav"}} {{$x.Get "key"}} {{$x.Del "key"}}`to add to that `sdict`, simply use `.Set` again &gt;  `{{$x.Set "YAGPDB" "is cool!"}} {{$x}}`
* To demonstrate sleep and slightly also editMessage functions. &gt; `{{$x := sendMessageRetID nil "Hello"}} {{sleep 3}} {{editMessage nil $x "There"}} {{sleep 5}} {{sendMessage nil "We all know, that"}} {{sleep 3}} YAGPDB rules!`

## How to get IDs <a id="how-to-get-ids"></a>

**User IDs:** Can be found by mentioning the user then adding a \ such as `\@jonas747#0001` . Alternatively if you have developer mode on, you can right click and select Copy ID. [How to enable developer mode in Discord](https://support.discordapp.com/hc/en-us/articles/206346498-Where-can-I-find-my-User-Server-Message-ID-).

**Channel IDs:** Can be found by mentioning the channel then adding a \ such as `\#announcements`. Alternatively if you have developer mode on, you can right click on the channel and select Copy ID.

**Role IDs**: Use the `listroles`command.

**Emote IDs:** 

If it is a **custom emote**, adding a \ in front of the emote such as `\:yag:` will display the name along with the ID such as  `<:yag:277569741932068864>`.

If it is an **animated emote**, do the same steps as a normal emote. If you do not have Discord Nitro, you can have a friend or a bot use the emote and right click on the emote to open its link. The ID will be a part of the URL.

If it is a **default emote**, look up the Unicode for the emote on Google. Note that some of the more customized default emotes such as some of the family emotes will not work in any of the YAGPDB commands. 

