---
description: '"Go is all about type... Type is life." // William Kennedy'
---

# Templates

## Preface

All available data that can be used in YAGPDB's templating "engine" which is slightly modified version of Golang's stdlib text/template package; more in depth and info about actions, pipelines and global functions like `printf, index, len,`etc &gt; [https://golang.org/pkg/text/template/](https://golang.org/pkg/text/template/) . This section is meant to be a concise and to the point reference document for all available templates/functions. For detailed explanations and syntax guide refer to the [learning resource](https://learn.yagpdb.xyz/).

**Legend**: at current state this is still prone to formatting errors, but everything in a `code block` should refer to a function, parts of a template's action-structure or output returned by YAGPDB; single word/literal-structure in _italics_ refers to type. Methods and fields \(e.g. .Append, .User\) are usually kept in standard formatting. If argument for a function is optional, it's enclosed in parenthesis `( )`. If there are many optional arguments possible, it's usually denoted by 3-dot `...`ellipsis.   
If functions or methods are denoted with an accent, tilde ~, they are not yet deployed in actual YAGPDB bot but are already in master code branch.

{% hint style="warning" %}
**Always put curly brackets around the data and "actions you perform" you want to formulate as a template's action-structure** like this: `{{.User.Username}}`

This `{{ ... }}` syntax of having two curly brackets aka braces around context is always necessary to form a template's control structure aka an action with methods and functions stated below.
{% endhint %}

{% hint style="info" %}
Templating system uses standard ASCII quotation marks:  
0x22 &gt; `"` for straight double quotes, 0x27 &gt; `'`for apostrophes and 0x60 ````` for backticks;   
so make sure no "smart-quotes" are being used.
{% endhint %}

## The Dot and Variables

The dot \(also known as cursor\) `{{ . }}`  encompasses all active data available for use in the templating system, in other words it always refers to current context.   
  
From official docs &gt; "Execution of the template walks the structure and sets the cursor, represented by a period `.` and called "dot", to the value at the current location in the structure as execution proceeds." All following fields/methods/objects like User/Guild/Member/Channel etc are all part of that dot-structure and there are some more in tables below.  
  
`$` has a special significance in templates, it is set to the [starting value of a dot](https://golang.org/pkg/text/template/#hdr-Variables). This means you have access to the global context from anywhere - e.g., inside `range`/`with` actions. `$` for global context would cease to work if you redefine it inside template, to recover it `{{ $ := .  }}`.  
  
`$` also denotes the beginning of a variable, which maybe be initialized inside a template action. So data passed around template pipeline can be initialized using syntax &gt; `$variable := value`. Previously declared variable can also be assigned with new data &gt; `$variable = value`, it has to have a white-space before it or control panel will error out. Variable scope extends to the `end` action of the control structure \(`if`, `with`, or `range`\) in which it is declared, or to the end of custom command if there are no control structures - call it global scope. 

| Field | Description |
| :--- | :--- |
| .CCID | The ID of currently executing custom command in type of _int64_. |
| .IsPremium | Returns boolean true/false whether guild is premium of YAGPDB or not. |
| .CCRunCount | Shows run count of triggered custom command, although this is not going to be 100% accurate as it's cached up to 30 minutes. |

## Pipes

A powerful component of templates is the ability to stack actions - like function calls, together - chaining one after another. This is done by using pipes `|`. Borrowed from Unix pipes, the concept is simple: each pipeline’s output becomes the input of the following pipe. One limitation of the pipes is that they can only work with a single value and that value becomes the last parameter of the next pipeline.   
  
**Example**: `{{randInt 41 | add 2}}` would pipeline`randInt` function's return to addition `add` as second parameter and it would be added to 2; this more simplified would be like `{{40 | add 2}}` with return 42. If written normally, it would be `{{ add 2 (randInt 41) }}`. Same pipeline but using a variable is also useful one -`{{$x:=40 | add 2}}` would not return anything as printout, 40 still goes through pipeline to addition and 42 is stored to variable `$x`.

{% hint style="warning" %}
Pipes are useful in select cases to shorten code and in some cases improve readability, but they **should not be overused**. In most cases, pipes are unnecessary and cause a dip in readability that helps nobody.
{% endhint %}

## User

| Field | Description |
| :--- | :--- |
| .User | The user's username together with discriminator. |
| .User.String | The user's username together with discriminator as _string_ type. |
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
        <p>Returns a <em>slice </em>of type <em>[ ]*logs.CCNameChange</em> having fields
          .Name and .Time of previous 15 usernames and skips <code>offset</code> number
          in that list.</p>
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
</table>

[User object in Discord documentation](https://discordapp.com/developers/docs/resources/user#user-object).

#### This section's snippets:

`{{(userArg .Guild.OwnerID).String}}` this template's action-structure returns Guild/Server owner's username and discriminator as of type _string_. First, `userArg` function is given `.Guild.OwnerID` as argument \(what it does, explained below\). The parentheses surrounding them make `userArg` function return `.User` as .User object which is handled further by `.String` method \(ref.`.User.String`\), giving a result like &gt; `YAGPDB#8760`.

## Guild / Server

| Field | Description |
| :--- | :--- |
| .Guild.ID | Outputs the ID of the guild. |
| .Guild.Name | Outputs the name of the guild. |
| .Guild.Icon | Outputs the [icon hash](https://discordapp.com/developers/docs/reference#image-formatting) ID of the guild's icon. |
| .Guild.Splash | Outputs the [splash hash](https://discordapp.com/developers/docs/reference#image-formatting) ID of the guild's splash. |
| .Guild.Region | Outputs the region of the guild. |
| .Guild.AfkChannelID | Outputs the AFK channel ID. |
| .Guild.OwnerID | Outputs the ID of the owner. |
| .Guild.JoinedAt | Outputs the timestamp when YAGPDB joined the guild. To convert it to type _time.Time_, use .Parse method &gt; `.Guild.JoinedAt.Parse` |
| .Guild.AfkTimeout | Outputs the time when a user gets moved into the AFK channel while not being active. |
| .Guild.MemberCount | Outputs the number of users on a guild. |
| .Guild.VerificationLevel | Outputs the required verification level for the guild. |
| .Guild.ExplicitContentFilter | Outputs the explicit content [filter level](https://discordapp.com/developers/docs/resources/guild#guild-object-explicit-content-filter-level) for the guild. |
| .Guild.DefaultMessageNotifications | Outputs the default message [notification setting](https://discordapp.com/developers/docs/resources/guild#guild-object-default-message-notification-level) for the guild. |
| .Guild.VoiceStates | Outputs a list of voice states \(users connected to VCs\) with type _\*discordgo.VoiceState._ |
| .Guild.EmbedEnabled | Outputs whether guild is embeddable \(e.g. widget\) or not, true / false. |
| .Guild.SystemChannelID | The id of the channel where guild notices such as welcome messages and boost events are posted. |
| .Guild.MfaLevel | required [MFA level](https://discordapp.com/developers/docs/resources/guild#guild-object-mfa-level) for the guild. If enabled, members with moderation powers will be required to have 2-factor authentication enabled in order to exercise moderation powers. |
| .Guild.Roles | Outputs all roles and indexing them gives more information about the role. For example `{{len .Guild.Roles}}` gives you how many roles are there in that guild. Role struct has [following fields](https://discordapp.com/developers/docs/topics/permissions#role-object). |
| .Guild.WidgetEnabled | Outputs whether or not the Server Widget is enabled or not. |
| .Guild.WidgetChannelID | Outputs the channel id for the server widget. |

[Guild object in Discord documentation](https://discordapp.com/developers/docs/resources/guild#guild-object).

## Member

| Field | Description |
| :--- | :--- |
| .Member.JoinedAt | When member joined the guild/server of type _discordgo.Timestamp_. Method .Parse will convert this to of type _time.Time_. |
| .Member.Nick | The nickname for this member. |
| .Member.Roles | A _slice_ of role IDs that the member has. |
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
      <td style="text-align:left">Edits triggering user&apos;s nickname, argument has to be of type <em>string</em>.
        YAGPDB&apos;s highest role has to be above the highest role of the member.</td>
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
</table>

[Member object in Discord documentation](https://discordapp.com/developers/docs/resources/guild#guild-member-object).

## Channel

| Field | Description |
| :--- | :--- |
| .Channel.Name | The name of the channel. |
| .Channel.ID | The ID of the channel. |
| .Channel.ParentID | The ID of the channel's parent \(category\), returns 0 if none. |
| .Channel.Topic | The topic of the channel. |
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
        of type <em>string</em>. For example &gt;<code>{{editChannelName nil (joinStr &quot;&quot; &quot;YAG - &quot; (randInt 1000))}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>editChannelTopic channel &quot;newTopic&quot;</code>
      </td>
      <td style="text-align:left">
        <p>Function edits channel&apos;s topic/description. <code>channel</code> can
          be either ID, &quot;name&quot; or even <code>nil</code> if triggered in that
          channel name change is intended to happen. <code>&quot;newTopic&quot;</code> has
          to be of type <em>string</em>. For example &gt;</p>
        <p><code>{{editChannelTopic nil &quot;YAG is cool&quot;}}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>getChannel channel</code>
      </td>
      <td style="text-align:left">Function returns full channel object of given <code>channel</code> argument
        which can be either it&apos;s ID, name or <code>nil</code> for triggering
        channel, and is of type <em>*dstate.ChannelState</em>. For example &gt; <code>{{(getChannel nil).Name}}</code> returns
        the name of the channel command was triggered in.</td>
    </tr>
  </tbody>
</table>

[Channel object in Discord documentation](https://discordapp.com/developers/docs/resources/channel#channel-object).

## Message

| Field | Description |
| :--- | :--- |
| .Message.ID | ID of the message. |
| .Message.ChannelID | Channel ID this message is in. |
| .Message.GuildID | Guild ID in which the message is. |
| .Message.Content | Text content on this message. |
| .Message.Timestamp | Timestamp of the message in type _discordgo.Timestamp_ \(use .Message.Timestamp.Parse to get type _time.Time_ and .Parse.String method returns type _string_\). |
| .Message.EditedTimestamp | The time at which the last edit of the message occurred, if it has been edited. As with .Message.Timestamp, it is of type _discordgo.Timestamp._  |
| .Message.MentionRoles | The roles mentioned in the message. |
| .Message.MentionEveryone | Whether the message mentions everyone. |
| .Message.Author | Author of the message \([User](templates.md#user) object\). |
| .Message.Attachments | Attachments to this message \(_slice_ of attachment objects\). |
| .Message.Embeds | Embeds on this message \(_slice_ of embed objects\). |
| .Message.Mentions | Users this message mentions. |
| .Message.Reactions | Reactions on this message \(only available from getMessage\). |
| .Message.Type | The [type](https://discordapp.com/developers/docs/resources/channel#message-object-message-types) of the message. |
| .Message.Pinned | Whether this message is pinned. |
| .Args | List of everything that is passed to .Message.Content. .Args is a _slice_ of type _string_. |
| .Cmd | .Cmd is of type _string_ and shows all arguments that trigger custom command, part of .Args. Starting from `{{index .Args 0}}`.  |
| .CmdArgs | List of all the arguments passed after `.Cmd` \(`.Cmd` is the actual trigger\) `.CmdArgs` is a _slice_ of type _string_. Examples in [misc. snippets](templates.md#miscellaneous-snippets). |
| .StrippedMsg | "Strips" or cuts off the triggering part of the message and prints out everything else after that. Bear in mind, when using regex as trigger, for example `"day"` and input message is `"Have a nice day my dear YAG!"` output will be `"my dear YAG!"`  - rest is cut off. |

[Message object in Discord documentation](https://discordapp.com/developers/docs/resources/channel#message-object).

{% hint style="info" %}
More information about the `Message` object can be found [here](../commands/custom-commands.md#the-message-template).
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
        <p>Has an alias .Message and works it works the same way.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">.ReactionAdded</td>
      <td style="text-align:left">Returns a boolean type <em>bool </em>true/false indicating whether reaction
        was added or removed.</td>
    </tr>
  </tbody>
</table>

[Reaction object in Discord documentation](https://discordapp.com/developers/docs/resources/channel#reaction-object).

## Time

Time in general uses Golang's time package library &gt; [https://golang.org/pkg/time/\#time](https://golang.org/pkg/time/#Time) and also this although slightly different syntax all applies here &gt; [https://gobyexample.com/time](https://gobyexample.com/time).

| Field | Description |
| :--- | :--- |
| .DiscordEpoch | Gives you Discord Epoch time in _time.Time._ `{{.DiscordEpoch.Unix}}` would return in seconds &gt; 1420070400. |
| .UnixEpoch | Gives you Unix Epoch time in _time.Time._ |
| .TimeHour | Variable of _time.Duration_ type and returns 1 hour &gt; `1h0m0s`. |
| .TimeMinute | Variable of _time.Duration_ type and returns 1 minute &gt; `1m0s`. |
| .TimeSecond | Variable of _time.Duration_ type and returns 1 second &gt; `1s`. |

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>currentTime</code>
      </td>
      <td style="text-align:left">Gets the current time, value is of type <em>time.Time</em> which can be
        used in a custom embed. More info <a href="../commands/custom-commands.md#currenttime-template">here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>formatTime Time &quot;arg&quot;</code>
      </td>
      <td style="text-align:left">Outputs given time in RFC822 formatting, first argument <code>Time</code> shows
        it needs to be of type <em>time.Time</em>, also with extra layout if second
        argument is given - e.g. <code>{{formatTime currentUserCreated &quot;3:04PM&quot;}}</code> would
        output <code>11:22AM</code> if that would have been user&apos;s creating
        time.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>humanizeDurationHours</code>
      </td>
      <td style="text-align:left">Returns given integer (whole number) or <em>time.Duration</em> argument
        in nanoseconds in human readable format - as how long it would take to
        get towards given time - e.g. <code>{{humanizeDurationHours 9000000000000000000}}</code> returns <code>285 years 20 weeks 6 days and 16 hours</code>.
        More in <a href="templates.md#this-sections-snippets-1">Snippets</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>humanizeDurationMinutes</code>
      </td>
      <td style="text-align:left">Sames as <code>humanizeDurationHours</code>, this time duration is returned
        in minutes - e.g. <code>{{humanizeDurationMinutes 3500000000000}}</code> would
        return <code>58 minutes</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>humanizeDurationSeconds</code>
      </td>
      <td style="text-align:left">Sames as both humanize functions above, this time duration is returned
        in seconds - e.g. <code>{{humanizeDurationSeconds 3500000000000}}</code> would
        return <code>58 minutes and 20 seconds</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>humanizeTimeSinceDays</code>
      </td>
      <td style="text-align:left">Returns time passed since given argument of type <em>time.Time</em> in human
        readable format - e.g. <code>{{humanizeTimeSinceDays currentUserCreated}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>newDate year month day hour minute second [timezone]</code>
      </td>
      <td style="text-align:left">
        <p>Returns new type <em>time.Time</em> object in UTC using given syntax (all
          arguments need to be of type <em>int</em>), for example &gt; <code>{{humanizeDurationHours ((newDate 2059 1 2 12 34 56).Sub currentTime)}}</code> will
          give you how much time till year 2059 January 2nd 12:34:56. More examples
          in <a href="templates.md#this-sections-snippets-1">Snippets</a>.</p>
        <p><code>timezone </code>is an optional string argument which uses golang&apos;s
          <a
          href="https://golang.org/pkg/time/#LoadLocation">LoadLocation</a>function and <a href="https://en.wikipedia.org/wiki/List_of_tz_database_time_zones">ZONEINFO syntax.</a> For
            example: <code>{{newDate 2020 4 20 12 34 56 &quot;Atlantic/Reykjavik&quot;}}</code> would
            return that time in GMT+0.</p>
      </td>
    </tr>
  </tbody>
</table>

#### This section's snippets:

* To demonstrate `humanizeDurationHours` and also how to parse a timestamp, output will be like `whois` command shows user's _join server age_. `{{humanizeDurationHours (currentTime.Sub .Member.JoinedAt.Parse)}}`
* To demonstrate `newDate` to get Epoch times. `{{$unixEpoch := newDate 1970 1 1 0 0 0}} in seconds > {{$unixEpoch.Unix}} {{$discordEpoch := newDate 2015 1 1 0 0 0}} in seconds > {{$discordEpoch.Unix}}`

## Custom Types

Golang has built-in primitive data types \(_int_, _string_, _bool_, _float64_, ...\) and built-in composite data types \(_array_, _slice_, _map_, ...\) which also are used in custom commands.   
  
YAGPDB's templating "engine" has currently two user-defined, custom data types - _templates.Slice_ and _templates.SDict_. There are other custom data types used like _discordgo.Timestamp_, __but these are outside  of the main code of YAGPDB, so not explained here further. Type _time.Time_ is covered in it's own [section](templates.md#time).  
  
Custom Types section discusses functions that initialize values carrying those _templates.Slice_ \(abridged to _cslice_\), _templates.SDict_ \(abridged to _sdict_\) types and their methods. Both types handle type _interface{}_ element. It's called an empty interface which allows a value to be of any type. So any argument of any type given is handled. \(In "custom commands"-wise mainly primitive data types, but _slices_ as well.\)

### templates.Slice

`templates.Slice` - This is a custom composite data type defined using an underlying data type _\[\]interface{}_ . It is of kind _slice_ \(similar to _array_\) having _interface{}_ type as its value and can be initialized using `cslice` function. Retrieving specific element inside _templates.Slice_ is by indexing its position number.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>cslice value1 value2 ...</code>
      </td>
      <td style="text-align:left">
        <p>Function creates a slice of type <em>templates.Slice</em> that can be used
          elsewhere (as an argument for <code>cembed</code> and <code>sdict</code> for
          example).
          <br />
        </p>
        <p>Example: <code>cslice 1 &quot;2&quot; (dict &quot;three&quot; 3) 4.5</code> returns <code>[1 2 map[three:3] 4.5]</code>,
          having length of 4 and index positions from 0 to 3. Notice that thanks
          to type <em>interface{}</em> value, <em>templates.Slice</em> elements&apos;
          inherent type does not change.</p>
      </td>
    </tr>
  </tbody>
</table>

<table>
  <thead>
    <tr>
      <th style="text-align:left">Method</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">.Append arg</td>
      <td style="text-align:left">Creates a new <em>cslice</em> having given argument appended fully by its
        type to current value. Has max size of 10 000 length.</td>
    </tr>
    <tr>
      <td style="text-align:left">.AppendSlice arg</td>
      <td style="text-align:left">Creates a new <em>cslice </em>from argument of type <em>slice </em>appended/joined
        with current value. Has max size of 10 000 length.</td>
    </tr>
    <tr>
      <td style="text-align:left">.Set int value</td>
      <td style="text-align:left">Changes/sets given <em>int </em>argument as index position of current <em>cslice </em>to
        new value. Note that .Set can only set indexes which already exist in the
        slice.</td>
    </tr>
    <tr>
      <td style="text-align:left">.StringSlice strict-flag</td>
      <td style="text-align:left">
        <p>Compares <em>slice</em> contents - are they of type <em>string, </em>based
          on the strict-flag which is <em>boolean </em>and is by default <em>false. </em>Under
          these circumstances if the element is a <em>string</em> then those elements
          will be included as a part of the <em>[]string</em> slice and rest simply
          ignored. Also <em>time.Time</em> elements - their default <em>string</em> notation
          will be included. If none are <em>string</em> an empty <em>[]string</em> slice
          is returned.</p>
        <p>If strict-flag is set to <em>true </em>it will return a <em>[]string</em> only
          if <b>all</b> elements are pure <em>string</em>, else <code>&lt;no value&gt;</code> is
          returned.</p>
        <p>Example in this section&apos;s <a href="templates.md#this-sections-snippets-2">Snippets</a>.</p>
      </td>
    </tr>
  </tbody>
</table>

#### This section's snippets:

* To demonstrate .StringSlice `{{(cslice currentTime.Month 42 "YAPGDB").StringSlice}}` will return a slice `[February YAGPDB]`. If the flag would have been set to true - {{...\).StringSlice true}}, all elements in that slice were not strings and `<no value>` is returned.

General example:

```go
Creating a new cslice: {{ $x := (cslice "red" "red") }} **{{ $x }}**
Appending to current cslice data 
and assigning newly created cslice to same variable:
{{ $x = $x.Append "green" }} **{{ $x }}**
Setting current cslice value in position 1:
{{ $x.Set 1 "blue" }} **{{ $x }}**
Appending a slice to current cslice data 
but not assigning newly created cslice to same variable:
**{{ $x.AppendSlice (cslice "yellow" "magenta") }}**
Variable is still: **{{ $x }}**
Type of variable: **{{ printf "%T" $x }}**
```

### templates.SDict

`templates.SDict` - This is a custom composite data type defined on an underlying data type _map\[string\]interface{}._ This is of kind _map_ having _string_ type as its key and _interface{}_ type as that key's value and can be  initialized ****using `sdict` function. A map is key-value store. This means you store value and you access that value by a key. Map is an unordered list and the number of parameters to form key-value pairs must be even. Retrieving specific element inside _templates.Sdict_ is by indexing its key.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>sdict &quot;key1&quot; value1 &quot;key2&quot; value2 ...</code>
      </td>
      <td style="text-align:left">
        <p>Like dict function, creating a <em>templates.SDict</em> type map, key must
          be of type <em>string</em>. Can be used for example in <code>cembed</code>.
          If only one argument is passed to <code>sdict </code>function having type <em>map[string]interface{}; </em>for
          example .ExecData and data retrieved from database can be of such type
          if <code>sdict</code> was used, it is converted to a new <em>sdict</em>.</p>
        <p></p>
        <p>Example: <code>sdict &quot;one&quot; 1 &quot;two&quot; 2 &quot;three&quot; (cslice 3 4) &quot;five&quot; 5.5</code> returns
          unordered <code>map[five:5.5 one:1 three:[3 4] two:2]</code>, having length
          of four and index positions are its keys. Notice that thanks to type <em>interface{}</em> value, <em>templates.SDict</em> elements&apos;
          inherent type does not change.</p>
      </td>
    </tr>
  </tbody>
</table>

| Method | Description |
| :--- | :--- |
| .Del "key" | Deletes given key from _sdict_. |
| .Get "key" | Retrieves given key from _sdict_. |
| .Set "key" value | Changes/sets given key to a new value or creates new one, if no such key exists in _sdict_. |

```go
Creating sdict: {{ $x := sdict "color1" "green" "color2" "red" }} **{{ $x }}**
Retrieving key "color2": **{{$x.Get "color2"}}**
Changing "color2" to "yellow": {{ $x.Set "color2" "yellow" }} **{{ $x }}**
Adding "color3" as "blue": {{ $x.Set "color3" "blue" }} **{{ $x }}**
Deleteing key "color1" {{$x.Del "color1"}} and whole sdict: **{{$x}}**
```

{% hint style="danger" %}
Since both _templates.SDict_ \(_sdict_\) and _templates.Slice_ \(_cslice_\) are custom composite data types, this type information is lost while saving to a database or passing as data to scheduled `execCC` or `scheduleUniqueCC`\(which internally involves saving to database\). Thus, they are converted to their underlying data types _map\[string\]interface{}_ and _\[\]interface{}_ respectively.   
  
They can be converted back to _templates.SDict_ and _templates.Slice_ as follows :  
  
For _sdict_ -  
`{{$sdict := sdict "a" 1 "b" "two"}}    
{{dbSet 0 "example" $sdict}}  
{{$map := (dbGet 0 "example").Value}}  
{{$sdict_converted := sdict $map}}`  
  
For _cslice_ -  
`{{$cslice := cslice 1 "two" 3.0}}    
{{dbSet 0 "example" $cslice}}  
{{$slice := (dbGet 0 "example").Value}}  
{{$cslice_converted := (cslice).AppendSlice $slice}}`

The above examples use some database specific functions which are explained [here](templates.md#database).
{% endhint %}

## Functions

Functions are underappreciated. In general, not just in templates. // Rob Pike

### Type conversion

| Function | Description |
| :--- | :--- |
| `json value` | Traverses given `value` through MarshalJSON \([more here](%20https://golang.org/pkg/encoding/json/#Marshal)\) and returns it as type _string_. For example `{{json .TimeHour}}` outputs type _string_; before this `.TimeHour` was of type _time.Duration_. Basically it's good to use if multistep type conversion is needed `(toString (toInt value) )` and certain parts of `cembed` need this for example. |
| `structToSdict struct` | Function converts exported field-value pairs of a _struct_ to an _sdict_. For example it is useful for editing embeds, rather than having to reconstruct the embed field by field manually. Exampe: `{{$x := cembed "title" "Something rules!" "color" 0x89aa00}} {{$x.Title}} {{$x = structToSdict $x}} {{- x.Set "Title" "No, YAGPDB rules!!!" -}} {{$x.Title}} {{$x}}` will return No, YAGPDB rules!!! and whole sdict-mapped _cembed_. |
| `toByte "arg"` | Function converts input to a slice of bytes - meaning _\[\]uint8_. `{{toByte "YAG€"}}` would output `[89 65 71 226 130 172]`. `toString` is capable of converting that slice back to _string_. |
| `toDuration` | Converts the argument, number or string to type _time.Duration_. Number represents nanoseconds. String can be with time modifier \(second, minute, hour, day etc\) `s, m, h, d, w, mo, y`,without a modifier string will be converted to minutes. Usage:`(toDuration x)`. Example in section's [Snippets](templates.md#this-sections-snippets-3).  |
| `toFloat` | Converts argument \(_int_ or _string_ type of a number\) to type _float64_.  Usage: `(toFloat x)`. Function will return 0, if type can't be converted to _float64_. |
| `toInt` | Converts something into an integer of type _int_. Usage: `(toInt x)`. Function will return 0, if type can't be converted to _int._ |
| `toInt64` | Converts something into an _int64_. Usage: `(toInt64 x)`.  Function will return 0, if type can't be converted to _int64._ |
| `toRune "arg"` | Function converts input to a slice of runes - meaning _\[\]int32_. `{{toRune "YAG€"}}`would output `[89 65 71 8364]`. These two functions - the one above, are good for further analysis of Unicode strings. `toString` is capable of converting that slice back to _string_. |
| `toString` | Has alias `str`. Converts some other types into a _string_. Usage: `(toString x)`. |

#### This section's snippets:

* To demonstrate `toDuration`, outputs 12 hours from current time in UTC. `{{(currentTime.Add (toDuration (mult 12 .TimeHour))).Format "15:04"}}`is the same as`{{(currentTime.Add (toDuration "12h")).Format "15:04"}}` or`{{(currentTime.Add (toDuration 43200000000000)).Format "15:04"}}`

{% hint style="success" %}
**Tip:** You can convert a Unicode code point back to its string equivalent using `printf "%c"`.  For example, `printf "%c" 99` would result in the string `c` as `99` is the Unicode code point for `c`.`printf` is briefly covered later on in the next section, further documentation can be found [here.](https://golang.org/pkg/fmt/)
{% endhint %}

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
      <td style="text-align:left">Joins several strings into one, separated by the first argument<code>&quot;separator&quot;</code>,
        example:<code>{{joinStr &quot;&quot; &quot;1&quot; &quot;2&quot; &quot;3&quot;}}</code> returns <code>123</code>.
        Also if functions have <em>string</em> or easily convertible return, they
        can be used inside <code>joinStr</code> e.g. <code>{{joinStr &quot;&quot; &quot;Let&apos;s calculate &quot; (add (mult 13 3) 1 2) &quot;, was returned at &quot; (currentTime.Format &quot;15:04&quot;) &quot;.&quot;}}</code>
      </td>
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
        <p>Function&apos;s first argument must be of type <em>string </em>or <em>slice</em>.</p>
        <p>Outputs the &quot;string&quot; after cutting/slicing off integer (numeric)
          value of symbols (actually starting the string&apos;s index from integer
          through integer2) - e.g. <code>{{slice &quot;Fox runs&quot; 2}}</code>outputs <code>x runs</code>.
          When using also integer2 - e.g. <code>{{slice &quot;Fox runs&quot; 1 7}}</code>,
          it outputs <code>ox run</code>. For slicing whole arguments, let&apos;s
          say words, see example in section&apos;s <a href="templates.md#this-sections-snippets-4">Snippets</a>.</p>
        <p></p>
        <p>This<code> slice</code> function is not the same as basic dynamically-sized <em>slice</em> data
          type discussed in this reference doc. Also it&apos;s custom, not having
          3-indices as the default one from <a href="https://golang.org/pkg/text/template/#hdr-Functions">text/template</a> package.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>urlescape &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Escapes the <em>string</em> so it can be safely placed inside a URL path
        segment - e.g. &quot;Hello, YAGPDB!&quot; becomes &quot;Hello%2C%20YAGPDB%21&quot;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>split &quot;string&quot; &quot;sepr&quot;</code>
      </td>
      <td style="text-align:left">Splits given <code>&quot;string&quot;</code> to substrings separated by <code>&quot;sepr&quot;</code>arg
        and returns new <em>slice </em>of the substrings between given separator
        e.g. <code>{{split &quot;YAG, is cool!&quot; &quot;,&quot;}}</code> returns <code>[YAG  is cool!]</code>  <em>slice</em> where <code>YAG</code> is
        at <code>index</code> position 0 and <code>is cool!</code> at <code>index</code> position
        1. Example also in section&apos;s <a href="templates.md#this-sections-snippets-4">Snippets</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>title &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Returns string with the first letter of each word capitalized.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>reFind &quot;regex&quot; &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Compares &quot;string&quot; to regex pattern and returns first match. <code>{{reFind &quot;AG&quot; &quot;YAGPDB is cool!&quot;}}</code>returns <code>AG</code> (regex
        pattern is case sensitive).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>reFindAll &quot;regex&quot; &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Adds all regex matches from the &quot;string&quot; to a <em>slice</em>.
        Example in section&apos;s <a href="templates.md#this-sections-snippets-4">Snippets</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>reFindAllSubmatches &quot;regex&quot; &quot;string&quot;</code>
      </td>
      <td style="text-align:left">Returns whole-pattern matches and also the sub-matches within those matches
        as <em>slices</em> inside a <em>slice</em>. <code>{{reFindAllSubmatches &quot;(?i)y([a-z]+)g&quot; &quot;youngish YAGPDB&quot;}} </code>returns<code> [[young oun] [YAG A]] </code>(regex
        pattern here is case insensitive).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>reReplace &quot;regex&quot; &quot;string1&quot; &quot;string2&quot;</code>
      </td>
      <td style="text-align:left">Replaces &quot;string1&quot; contents with &quot;string2&quot; at regex
        match point. <code>{{reReplace &quot;I am&quot; &quot;I am cool!&quot; &quot;YAGPDB is&quot;}}</code>returns <code> YAGPDB is cool!</code> (regex
        pattern here is case sensitive).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>print, printf, println</code>
      </td>
      <td style="text-align:left">These are GO template package&apos;s predefined functions and are aliases
        for <a href="https://golang.org/pkg/fmt/#Sprint">fmt.Sprint</a>, <a href="https://golang.org/pkg/fmt/#Sprint">fmt.Sprintf</a> and
        <a
        href="https://golang.org/pkg/fmt/#Sprintln">fmt.Sprintln</a>. Formatting is also discussed <a href="https://golang.org/pkg/fmt/#hdr-Printing">here</a>.
          <br
          />
          <br /><code>printf</code> is usable for example to determine the type of the
          value &gt; <code>{{printf &quot;%T&quot; currentTime}} </code>outputs <code>currentTime </code>functions
          output value type of<code> time.Time</code>. In many cases, <code>printf</code> is
          a great alternative to <code>joinStr</code> for concatenate strings.</td>
    </tr>
  </tbody>
</table>

{% hint style="info" %}
Special information we can include in the string is _escape sequences_. Escape sequences are two \(or more\) characters, the first of which is a backslash `\`, which gives the remaining characters special meaning - let's call them metacharacters. The most common escape sequence you will encounter is `\n`, which means "newline". 
{% endhint %}

{% hint style="info" %}
With regular expression patterns - when using quotes you have to "double-escape" metacharacters starting with backslash. You can use backquotes/ticks to simplify this:`{{reFind "\\d+" (toString 42)}}` versus ``{{reFind `\d+` (toString 42)}}``
{% endhint %}

#### This section's snippets:

* `{{$args:= (joinStr " " (slice .CmdArgs 1))}}` Saves all the arguments except the first one to a variable `$args`. 
* To demonstrate usage of `split` function. &gt; `{{$x := "Hello, World, YAGPDB, here!"}} {{range $k, $v := (split $x ", ")}}Word {{$k}}: __{{$v}}__ {{end}}`
* To demonstrate usage of `reFindAll`. &gt;  `Before regex: {{$msg := "1 YAGPDB and over 100000 servers conquered."}} {{$re2 := reFindAll "[0-9]+" $msg}} {{$msg}}   After regex matches: {{joinStr " " "Only" (index $re2 0) "YAGPDB and already" (index $re2 1) "servers captured."}}`

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
      <td style="text-align:left">Returns x + y + z + ..., detects first number&apos;s type - is it <em>int</em> or <em>float</em> and
        based on that adds. (use <code>toFloat</code> on the first argument to force
        floating point math.)<code>{{add 5 4 3 2 -1}}</code> sums all these numbers
        and returns <code>13</code>.</td>
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
        number&apos;s type. <code>{{mult 3.14 2}}</code> returns <code>6.28</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>div x y z ...</code>
      </td>
      <td style="text-align:left">Division, like <code>add</code> or <code>mult</code>, detects number&apos;s
        type first. <code>{{div 11 3}}</code> returns <code>3</code> whereas <code>{{div 11.1 3}}</code> returns <code>3.6999999999999997</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>fdiv x y z ...</code>
      </td>
      <td style="text-align:left">Meant specifically for floating point numbers division.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>log x base</code>
      </td>
      <td style="text-align:left">Log is a logarithm function using (log base of x). Arguments can be any
        type of numbers, as long as they follow logarithm logic. Return value is
        of type <em>float64</em>. If base argument is not given It is using natural
        logarithm (base e - The Euler&apos;s constant) as default, also is the
        default to change the base.<code>{{ log &quot;123&quot; 2 }}</code> will
        return <code>6.94251450533924</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>mod x y</code>
      </td>
      <td style="text-align:left">Mod returns the floating-point remainder of x/y. <code>mod 17 3</code> returns <code>2 </code>of
        type <em>float64</em>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>pow x y</code>
      </td>
      <td style="text-align:left">Pow returns x**y, the base-x exponential of y which have to be both numbers.
        Type is returned as <em>float64</em>. <code>{{ pow 2 3 }}</code> returns <code>8</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>randInt (stop, or start stop)</code>
      </td>
      <td style="text-align:left">
        <p>Returns a random integer between 0 and stop, or start - stop if two args
          are provided.</p>
        <p>Result will be <code>start &lt;= random number &lt; stop</code>. Example
          in section&apos;s <a href="templates.md#this-sections-snippets-5">Snippets</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>round</code>
      </td>
      <td style="text-align:left">Returns the nearest integer, rounding half away from zero. Regular rounding
        &gt; 10.4 is <code>10</code> and 10.5 is <code>11</code>. All round functions
        return type <em>float64</em>, so use conversion functions to get integers.
        For more complex rounding, example in section&apos;s <a href="templates.md#this-sections-snippets-5">Snippets</a>.</td>
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
      <td style="text-align:left">Returns the square root of a number as type <em>float64</em>.
        <br /><code>{{sqrt 49}}</code> returns <code>7, {{sqrt 12.34 | printf &quot;%.4f&quot;}} returns 3.5128</code>
      </td>
    </tr>
  </tbody>
</table>

#### This section's snippets:

* `{{$d := randInt 10}}` Stores random _int_ into variable `$d` \(a random number from 0-9\).
* To demonstrate rounding float to 2 decimal places. `{{div (round (mult 12.3456 100)) 100}}` returns 12.35 `{{div (roundFloor (mult  12.3456 100)) 100}}` returns 12.34

### Message functions

| Function | Description |
| :--- | :--- |
| `addMessageReactions channel messageID reactions` | Same as `addReactions` or `addResponseReactions`, but can be used on any messages using its ID. `channel` can be either `nil`, channel's ID or its name. Example in section's [Snippets](templates.md#this-sections-snippets-6). |
| `addReactions "👍" "👎" ...` | Adds each emoji as a reaction to the message that triggered the command \(recognizes Unicode emojis and `emojiName:emojiID`\). |
| `addResponseReactions "👍" "👎" ...` | Adds each emoji as a reaction to the response message \(recognizes Unicode emojis and `emojiName:emojiID`\). |
| `complexMessage "content" args "embed" args "file" args`  | `complexMessage` creates a _so-called_ bundle of different message fields for `sendMessage...` functions to send them out all together. Its arguments need to be preceded by predefined keys `"content"` for regular text, `"embed"` for embed arguments created by `cembed` or `sdict`, `"file"` for printing out content as a file \(max 100 000 characters ca100kB\). Example in this section's [Snippets](templates.md#this-sections-snippets-6). |
| `complexMessageEdit "content" args "embed" args` | Special case for `editMessage` function - either if `complexMessage` is involved or works even with regular message. Has two parameters `"content"` and `"embed"` to edit regular text part or embed part. If `"embed"` is set to `nil`, it deletes whole embed. Example in this section's [Snippets](templates.md#this-sections-snippets-6). |
| `deleteAllMessageReactions channel messageID` | Deletes all reactions pointed message has. `channel` can be ID, "name" or `nil`. |
| `deleteMessageReaction channel messageID userID emojis` | Deletes reaction\(s\) from a message. `channel` can be ID, "name" or `nil`.  `emojis` argument can be up to 10 emojis, syntax is `emojiName` for Unicode/Discord's default emojis and `emojiName:emojiID` for custom emotes.   Example: `{{deleteMessageReaction nil (index .Args 1) .User.ID "👍" "👎"}}` will delete current user's reactions with thumbsUp/Down emotes from current running channel's message which ID is given to command as first argument `(index .Args 1)`. Also usable with [Reaction trigger](templates.md#reaction). |
| `deleteMessage channel messageID (delay)` | Deletes message with given `messageID` from `channel`. Channel can be either `nil`, channel's ID or its name. `(delay)` is optional and like following two delete functions, it defaults to 10 seconds, max being 1 day or 86400 seconds. Example in section's [Snippets](templates.md#this-sections-snippets-6). |
| `deleteResponse (delay)` | Deletes the response after a certain time from optional `delay` argument \(max 86400 seconds = 1 day\). Defaults to 10 seconds. |
| `deleteTrigger (delay)` | Deletes the trigger after a certain time from optional `delay` argument  \(max 86400 seconds = 1 day\). Defaults to 10 seconds. |
| `editMessage channel messageID newMessageContent` | Edits the message in channel, channel can be either `nil`, channel's ID or "name". Light example in section's [Snippets](templates.md#this-sections-snippets-6). |
| `editMessageNoEscape channel messageID newMessageContent` | Edits the message in channel and has same logic in escaping characters as `sendMessageNoEscape`. |
| `getMessage channelID messageID` | Returns a [Message ](templates.md#message)object. |
| `sendDM "message here"` | Sends the user a direct message, only one DM can be sent per custom command \(accepts embed objects\). YAG will only DM triggering user. |
| `sendMessage channel message` | Sends `message (string or embed)` in `channel`, channel can be either `nil`, the channel ID or the channel's "name". |
| `sendMessageNoEscape channel message` | Sends `message (string or embed)` in `channel`, channel can be either `nil`, the channel ID or the channel "name". Doesn't escape mentions \(e.g. role mentions or @here/@everyone\). |
| `sendMessageRetID channel message` | Same as `sendMessage`, but also returns messageID to assigned variable for later use. Example in section's [Snippets](templates.md#this-sections-snippets-6). |
| `sendMessageNoEscapeRetID channel message` | Same as `sendMessageNoEscape`, but also returns messageID to assigned variable for later use. |

#### This section's snippets:

* Sends message to current channel `nil` and gets messageID to variable `$x`. Also adds reactions to this message. After 5 seconds, deletes that message. &gt;

  `{{$x := sendMessageRetID nil "Hello there!"}} {{addMessageReactions nil $x "👍" "👎"}} {{deleteMessage nil $x 5}}`

* To demonstrate `sleep` and slightly also `editMessage` functions. &gt; `{{$x := sendMessageRetID nil "Hello"}} {{sleep 3}} {{editMessage nil $x "There"}} {{sleep 3}} {{sendMessage nil "We all know, that"}} {{sleep 3}} YAGPDB rules!`
* To demonstrate usage of `complexMessage` with `sendMessage`. `{{sendMessage nil (complexMessage "content" "Who rules?" "embed" (cembed "description" "YAGPDB of course!" "color" 0x89aa00) "file" "Here we print something nice - you all are doing awesome!")}}`
* To demonstrate usage of `complexMessageEdit` with `editMessage`. `{{$mID := sendMessageRetID nil (complexMessage "content" "You know what is..." "embed" (cembed "title" "FUN!?" "color" 0xaa8900))}} {{sleep 3}} {{editMessage nil $mID (complexMessageEdit "embed" (cembed "title" "YAGPDB!" "color" 0x89aa00) "content" "Yes, it's always working with...")}}{{sleep 3}}{{editMessage nil $mID (complexMessageEdit "embed" nil "content" "Embed deleted, goodbye YAG!")}}{{deleteMessage nil $mID 3}}`

### Mentions

| Function | Description |
| :--- | :--- |
| `mentionEveryone` | Mentions `@everyone`. |
| `mentionHere` | Mentions `@here`. |
| `mentionRoleName "rolename"` | Mentions the first role found with the provided name \(case-insensitive\). |
| `mentionRoleID roleID` | Mentions the role found with the provided ID. |

#### This section's snippets:

* `<@{{.User.ID}}>` Outputs a mention to the user that called the command and is the same as `{{.User.Mention}}`
* `<@###########>` Mentions the user that has the ID \#\#\#\#\#\# \(See [How to get IDs](templates.md#how-to-get-ids) to get ID\).
* `<#&&&&&&&&&&&>` Mentions the channel that has ID &&&&&& \(See [How to get IDs](templates.md#how-to-get-ids) to get ID\).
* `<@&##########>` Mentions the role with ID \#\#\#\#\#\#\#\# \([lis~~t~~roles](../commands/all-commands.md#listroles) command gives roleIDs\). This is usable for example with `{{sendMessageNoEscape nil "Welcome to role <@&11111111...>"}}`. Mentioning that role has to be enabled server- side in Discord.

### Role functions

| Function | Description |
| :--- | :--- |
| `addRoleID roleID` | Adds the role with the given ID to the user that triggered the command \(use the `listroles` command for a list of roles\). |
| `addRoleName roleName` | Adds the role with given name to the user that triggered the command \(use the `listroles` command for a list of roles\). |
| `giveRoleID userID roleID` | Gives a role by ID to the target. |
| `giveRoleName userID "roleName"` | Gives a role by name to the target. |
| `hasRoleID roleID` | Returns true if the user has the role with the specified ID \(use the listroles command for a list of roles\). |
| `hasRoleName "rolename"` | Returns true if the user has the role with the specified name \(case-insensitive\). |
| `removeRoleID roleID (delay)` | Removes the role with the given ID from the user that triggered the command \(use the listroles command for a list of roles\). `Delay` is optional argument in seconds. |
| `removeRoleName roleName (delay)` | Removes the role with given name from the user that triggered the command \(use the listroles command for a list of roles\). `Delay` is optional argument in seconds. |
| `takeRoleID userID roleID (delay)` | Takes away a role by ID from the target. `Delay` is optional argument in seconds. |
| `takeRoleName userID "roleName" (delay)` | Takes away a role by name from the target. `Delay` is optional argument in seconds. |
| `targetHasRoleID userID roleID` | Returns true if the given user has the role with the specified ID \(use the listroles command for a list of roles\). Example in section's [Snippets](templates.md#this-sections-snippets-8). |
| `targetHasRoleName userID "roleName"` | Returns true if the given user has the role with the specified name \(case-insensitive\). |

#### This section's snippets:

* To demonstrate usage of `targetHasRoleID`. &gt;  `{{$x := (userArg (index .Args 1)).ID}} {{if targetHasRoleID $x ############}} Has the Role! {{else}} Does not have the role! {{end}}`

### Current User

| Function | Description |
| :--- | :--- |
| `currentUserCreated` |  Returns value of type _time.Time_ and shows when the current user was created. |
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
      <td style="text-align:left"><code>cembed &quot;list of embed values&quot;</code>
      </td>
      <td style="text-align:left">Function to generate embed inside custom command. <a href="../others/custom-embeds.md#embeds-in-custom-commands">More in-depth here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>cslice, sdict</code>
      </td>
      <td style="text-align:left">These functions are covered in their own section <a href="templates.md#custom-types">here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>dict key1 value1 key2 value2 ...</code>
      </td>
      <td style="text-align:left">Creates an unordered collection of key-value pairs, a dictionary so to
        say. The number of parameters to form key-value pairs must be even. Example
        <a
        href="https://docs.yagpdb.xyz/reference/custom-command-examples#dictionary-example">here</a>. Keys and values can be of any type. Key is not restricted to <em>string </em>only
          as in case with <code>sdict</code>. <code>dict </code>also has helper methods
          .Del, .Get and .Set and they function the same way as <code>sdict</code> ones
          discussed <a href="templates.md#templates-sdict">here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>exec &quot;command&quot; &quot;args&quot; &quot;args&quot; &quot;args&quot; ...</code>
      </td>
      <td style="text-align:left">
        <p>Executes a YAGPDB command (e.g. roll, kick etc) in a custom command. Exec
          can be run max 5 times per command. If real command returns an embed - <code>exec</code> will
          return raw data of type embed, so you can use embed fields for better formatting
          - e.g. <code>{{$resp := exec &quot;whois&quot;}} {{$resp.Title}} Joined at &gt; {{(index $resp.Fields 4).Value}}</code> will
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
          Last example is the same as <code>{{exec (joinStr &quot; &quot; &quot;clear&quot; $x &quot;-nopin&quot;)}}</code>(also
          notice the space in <code>joinStr</code> separator).</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>execAdmin &quot;command&quot; &quot;args&quot; &quot;args&quot; &quot;args&quot; ...</code>
      </td>
      <td style="text-align:left">Functions same way as <code>exec</code> but will override any permission
        requirement (such as the kick permission to use kick command etc.).</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>humanizeThousands arg</code>
      </td>
      <td style="text-align:left">This function places comma to separate groups of thousands of a number. <code>arg </code>can
        be <em>int</em> or <em>string</em>, has to be a whole number, e.g. <code>{{humanizeThousands &quot;1234567890&quot;}}</code> will
        return <code>1,234,567,890</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>in list value</code>
      </td>
      <td style="text-align:left">Returns <em>bool</em> true/false whether case-sensitive value is in list/<em>slice</em>. <code>{{ in (cslice &quot;YAGPDB&quot; &quot;is cool&quot;) &quot;yagpdb&quot; }}</code> returns <code>false</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>index arg ...keys</code>
      </td>
      <td style="text-align:left">
        <p>Returns the result of indexing its first argument by the following arguments.
          Each indexed item must be a <em>map</em>, <em>slice </em>or <em>array</em>.</p>
        <p></p>
        <p>Example: <code>{{index .Args 1}}</code> returns first argument after trigger
          which is always at position 0.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>inFold </code>
      </td>
      <td style="text-align:left">Same as <code>in</code>, but is case-insensitive. <code>{{inFold (cslice &quot;YAGPDB&quot; &quot;is cool&quot;) &quot;yagpdb&quot;}}</code> returns <code>true</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>kindOf value (flag)</code>
      </td>
      <td style="text-align:left">This function helps to determine what kind of data type we are dealing
        with. <code>flag</code> part is a <em>bool </em> and if set as <b>true </b>(<b>false </b>is
        optional)<b> </b>returns the value where given <code>value</code> points
        to. Example: <code>{{kindOf cembed false}} {{kindOf cembed true}} </code>will
        return <code>ptr </code>and <code>struct</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>noun</code>
      </td>
      <td style="text-align:left">Returns a random noun.</td>
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
      <td style="text-align:left">Required by <code>parseArgs</code> and it defines the type of argument for <code>parseArgs</code>.
        <a
        href="../commands/custom-commands.md#require-arguments">More in depth</a>here and an example in <a href="custom-command-examples.md#parseargs-example">Custom Command Examples.</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>range slice/array</code>
      </td>
      <td style="text-align:left">Iterates (loops) over the given <em>slice </em>or <em>array </em>and sets
        successive elements as active data (the dot) to be further handled inside
        the <code>range</code> action. Example usage <a href="custom-command-examples.md#range-example">here</a>.
        <a
        href="templates.md#range-action">More in-depth here</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sendTemplate channel templateName data</code>
      </td>
      <td style="text-align:left">
        <p>Function sends a formulated template to another channel.
          <br />Channel is like always either name, number or nil. Also returns messageID.</p>
        <p>Example: <code>{{define &quot;logsTemplate&quot;}}This text will output on different channel, you can also use functions like {{currentTime}}. {{.TemplateArgs}} would be additional data sent out. {{end}}</code>
        </p>
        <p>Now we call that &quot;logs&quot; in the same custom command.<code>{{sendTemplate &quot;logs&quot; &quot;logsTemplate&quot; &quot;YAG rules!&quot;}}</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sendTemplateDM temlateName data</code>
      </td>
      <td style="text-align:left">Works the same way as function above. Only channel&apos;s name is not
        in the arguments. YAGPDB <b>will only </b>DM the triggering user.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>seq start stop</code>
      </td>
      <td style="text-align:left">Creates a new <em>slice</em> of type <em>int</em>, beginning from start number,
        increasing in sequence and ending at stop (not included). <code>{{seq -4 2}}</code> returns
        a <em>slice</em>  <code>[ -4 -3 -2 -1 0 1 ]</code>. Sequence&apos;s max length
        is 10 000.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>shuffle list</code>
      </td>
      <td style="text-align:left">Returns a shuffled, randomized version of a list/<em>slice</em>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sleep seconds</code>
      </td>
      <td style="text-align:left">Pauses execution of template&apos;s action-structure inside custom command
        for max 60 seconds combined. Argument<code>seconds</code>is an integer
        (whole number). Example in <a href="templates.md#miscellaneous-snippets">Snippets</a>.</td>
    </tr>
  </tbody>
</table>

### ExecCC

{% hint style="warning" %}
`execCC` calls are limited to 1 / CC for non-premium users and 10 / CC for premium users.
{% endhint %}

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
        &gt; <a href="templates.md#this-sections-snippets-9">Snippets</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>scheduleUniqueCC ccID channel delay key data</code>
      </td>
      <td style="text-align:left">
        <p>Same as <code>execCC</code>except there can only be 1 scheduled cc execution
          per server per key, if key already exists then it is overwritten with the
          new data and delay (as above, in seconds).</p>
        <p>An example would be a mute command that schedules the unmute action sometime
          in the future. However, let&apos;s say you use the unmute command again
          on the same user, you would want to override the last scheduled unmute
          to the new one. This can be used for that.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>cancelScheduledUniqueCC ccID key</code>
      </td>
      <td style="text-align:left">Cancels a previously scheduled custom command execution using <code>scheduleUniqueCC </code>
      </td>
    </tr>
  </tbody>
</table>

#### This section's snippets:

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
  
There can be 10 database interactions per CC, out of which dbTop/BottomEntries, dbCount and dbGetPattern may be only run twice. \(50,10 for premium users\).  
  
[Example here](custom-command-examples.md#database-example).

| Function | Description |
| :--- | :--- |
| `dbSet userID key value` | Sets the value for the specified `key` for the specific `userID` to the specified `value`. `userID` can be any number of type _int64_.    Values are stored either as of type _float64_ \(for numbers, oct or hex\) or as varying type in bytes \(for _slices_, _maps_, _strings_ etc\) depending on input argument. |
| `dbSetExpire userID key value ttl` | Same as `dbSet` but with an expiration in seconds. |
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
| .ID | ID of the entry. |
| .GuildID | ID of the server. |
| .UserID | ID of the user. |
| .User | [user object](templates.md#user). |
| .CreatedAt | When this entry was created. |
| .UpdatedAt | When this entry was last updated. |
| .ExpiresAt | When entry will expire. |
| .Key | The key of the entry. |
| .Value | The value of the entry. |

## Conditional branching

Branching using `if` action's pipeline and comparison operators - these operators don't need to be inside `if` branch. `if` statements always need to have an enclosing `end`.  


{% hint style="success" %}
`eq` , though often used with 2 arguments \(`eq x y`\) can actually be used with more than 2. If there are more than 2 arguments, it checks whether the first argument is equal to any one of the following arguments. This behaviour is unique to `eq`.
{% endhint %}

{% hint style="info" %}
Comparison operators always require the same type: i.e comparing `1.23` and `1` would throw **`incompatible types for comparison`** error as they are not the same type \(one is float, the other int\). To fix this, you should convert both to the same type -&gt; for example, `toFloat 1`.
{% endhint %}

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
      <td style="text-align:left"><code>{{$x := 7}} {{$y := 8}} {{ne $x $y}}</code> returns <code>true</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Less than: lt</td>
      <td style="text-align:left"><code>{{if lt (len .Args) 5}} output {{end}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Less than or equal: le</td>
      <td style="text-align:left"><code>{{$x := 7}} {{$y := 8}} {{le $x $y}}</code> returns <code>true</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Greater than: gt</td>
      <td style="text-align:left"><code>{{if gt (len .Args) 1}} output {{end}}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Greater than or equal: ge</td>
      <td style="text-align:left"><code>{{$x := 7}} {{$y := 8}} {{ge $x $y}}</code> returns <code>false</code>
      </td>
    </tr>
  </tbody>
</table>

## Range action

`range`iterates over element values in variety of data structures in pipeline - slices/arrays, maps or channels. The dot `.` is set to successive elements of those data structures and output will follow execution. If the value of pipeline has zero length, nothing is output or if an `{{else}}` action is used, that section will be executed.

Affected dot inside `range` is important because methods mentioned above in this documentation:`.Server.ID`, `.Message.Content` etc are all already using the dot on the pipeline and if they are not carried over to the `range` control structure directly, these fields do not exists and template will error out. Getting those values inside `range` and also `with` action would need `$.User.ID` for example.  
  
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
  
Affected dot inside `with` is important because methods mentioned above in this documentation:`.Server.ID`, `.Message.Content` etc are all already using the dot on the pipeline and if they are not carried over to the `with` control structure directly, these fields do not exists and template will error out. Getting those values inside `with` and also `range` action would need `$.User.ID` for example.

Like `if` and `range` actions, `with` is concluded using `{{end}}` and variable scope extends to that point.

```go
{{/* Shows the scope and how dot is affected by object's value in pipeline */}}
{{ $x := "42" }} {{ with and ($z:= seq 0 5) ($x := seq 0 10) }} 
len $x: `{{ len $x }}` 
{{/* "and" function uses $x as last value for dot */}}
same as len dot: `{{ len . }}` 
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
* `{{/* this is a comment */}}`For commenting something inside a template, use this syntax. May contain newlines. Comments do not nest and they start and end at the delimiters. 
* To trim spaces, for example &gt;`{{- /* this is a multi-line  comment with whitespace trimmed from  preceding and following text */ -}}`  Using`{{- ... -}}` is also handy inside`range` actions, because whitespaces and newlines are rendered there as output.
* To demonstrate sleep and slightly also editMessage functions. &gt; `{{$x := sendMessageRetID nil "Hello"}} {{sleep 3}} {{editMessage nil $x "There"}} {{sleep 5}} {{sendMessage nil "We all know, that"}} {{sleep 3}} YAGPDB rules!`

