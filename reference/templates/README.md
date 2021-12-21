---
description: '"Go is all about type... Type is life." // William Kennedy'
---

# Templates

## Preface

All available data that can be used in YAGPDB's templating "engine" which is slightly modified version of Golang's stdlib text/template package; more in depth and info about actions, pipelines and global functions like `printf, index, len,`etc > [https://golang.org/pkg/text/template/](https://golang.org/pkg/text/template/) . This section is meant to be a concise and to the point reference document for all available templates/functions. For detailed explanations and syntax guide refer to the [learning resource](https://learn.yagpdb.xyz).

**Legend**: at current state this is still prone to formatting errors, but everything in a `code block` should refer to a function, parts of a template's action-structure or output returned by YAGPDB; single word/literal-structure in _italics_ refers to type. Methods and fields (e.g. .Append, .User) are usually kept in standard formatting. If argument for a function is optional, it's enclosed in parenthesis `( )`. If there are many optional arguments possible, it's usually denoted by 3-dot `...`ellipsis. \
If functions or methods are denoted with an accent, tilde \~, they are not yet deployed in actual YAGPDB bot but are already in master code branch.

{% hint style="warning" %}
**Always put curly brackets around the data and "actions you perform" you want to formulate as a template** like this:`{{.User.Username}}`

This `{{ ... }}` syntax of having two curly brackets aka braces around context is necessary to form a template's control structure also known as an action with methods and functions stated below.
{% endhint %}

{% hint style="info" %}
Templating system uses standard ASCII quotation marks:\
0x22 > `"` for straight double quotes, 0x27 > `'`for apostrophes and 0x60 `` ` `` for backticks; \
so make sure no "smart-quotes" are being used.
{% endhint %}

## The Dot and Variables

The dot (also known as cursor) `{{ . }}`  encompasses all active data available for use in the templating system, in other words it always refers to current context. \
\
From official docs > "Execution of the template walks the structure and sets the cursor, represented by a period `.` and called "dot", to the value at the current location in the structure as execution proceeds." All following fields/methods/objects like User/Guild/Member/Channel etc are all part of that dot-structure and there are some more in tables below.\
\
`$` has a special significance in templates, it is set to the [starting value of a dot](https://golang.org/pkg/text/template/#hdr-Variables). This means you have access to the global context from anywhere - e.g., inside `range`/`with` actions. `$` for global context would cease to work if you redefine it inside template, to recover it `{{ $ := .  }}`.\
\
`$` also denotes the beginning of a variable, which maybe be initialized inside a template action. So data passed around template pipeline can be initialized using syntax > `$variable := value`. Previously declared variable can also be assigned with new data > `$variable = value`, it has to have a white-space before it or control panel will error out. Variable scope extends to the `end` action of the control structure (`if`, `with`, or `range`) in which it is declared, or to the end of custom command if there are no control structures - call it global scope.&#x20;

| **Field**   | **Description**                                                                                                              |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------- |
| .CCID       | The ID of currently executing custom command in type of _int64_.                                                             |
| .CCRunCount | Shows run count of triggered custom command, although this is not going to be 100% accurate as it's cached up to 30 minutes. |
| .IsPremium  | Returns boolean true/false whether guild is premium of YAGPDB or not.                                                        |

## Pipes

A powerful component of templates is the ability to stack actions - like function calls, together - chaining one after another. This is done by using pipes `|`. Borrowed from Unix pipes, the concept is simple: each pipeline’s output becomes the input of the following pipe. One limitation of the pipes is that they can only work with a single value and that value becomes the last parameter of the next pipeline. \
\
**Example**: `{{randInt 41 | add 2}}` would pipeline`randInt` function's return to addition `add` as second parameter and it would be added to 2; this more simplified would be like `{{40 | add 2}}` with return 42. If written normally, it would be `{{ add 2 (randInt 41) }}`. Same pipeline but using a variable is also useful one -`{{$x:=40 | add 2}}` would not return anything as printout, 40 still goes through pipeline to addition and 42 is stored to variable `$x` whereas `{{($x:=40) | add 2}}` would return 42 and store 40 to `$x`.

{% hint style="warning" %}
Pipes are useful in select cases to shorten code and in some cases improve readability, but they **should not be overused**. In most cases, pipes are unnecessary and cause a dip in readability that helps nobody.
{% endhint %}

## Guild / Server

| **Field**                          | **Description**                                                                                                                                                                                                                                                            |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| .Guild.AfkChannelID                | Outputs the AFK channel ID.                                                                                                                                                                                                                                                |
| .Guild.AfkTimeout                  | Outputs the time when a user gets moved into the AFK channel while not being active.                                                                                                                                                                                       |
| .Guild.Channels                    | Outputs a slice of channels in the guild with type _\[]dstate.ChannelState._                                                                                                                                                                                               |
| .Guild.DefaultMessageNotifications | Outputs the default message [notification setting](https://discordapp.com/developers/docs/resources/guild#guild-object-default-message-notification-level) for the guild.                                                                                                  |
| .Guild.EmbedEnabled                | Outputs whether guild is embeddable (e.g. widget) or not, true / false. **DEPRECATED.**                                                                                                                                                                                    |
| .Guild.Emojis                      | Outputs a list of emojis in the guild with type _discordgo.Emoji._                                                                                                                                                                                                         |
| .Guild.ExplicitContentFilter       | Outputs the explicit content [filter level](https://discordapp.com/developers/docs/resources/guild#guild-object-explicit-content-filter-level) for the guild.                                                                                                              |
| .Guild.Features                    | The list of enabled guild features of type _\[]string_.                                                                                                                                                                                                                    |
| .Guild.Icon                        | Outputs the [icon hash](https://discordapp.com/developers/docs/reference#image-formatting) ID of the guild's icon. Setting full icon URL is explained [here](https://discord.com/developers/docs/reference#image-formatting).                                              |
| .Guild.ID                          | Outputs the ID of the guild.                                                                                                                                                                                                                                               |
| .Guild.MemberCount                 | Outputs the number of users on a guild.                                                                                                                                                                                                                                    |
| .Guild.MfaLevel                    | required [MFA level](https://discordapp.com/developers/docs/resources/guild#guild-object-mfa-level) for the guild. If enabled, members with moderation powers will be required to have 2-factor authentication enabled in order to exercise moderation powers.             |
| .Guild.Name                        | Outputs the name of the guild.                                                                                                                                                                                                                                             |
| .Guild.OwnerID                     | Outputs the ID of the owner.                                                                                                                                                                                                                                               |
| .Guild.Region                      | Outputs the region of the guild.                                                                                                                                                                                                                                           |
| .Guild.Roles                       | Outputs all roles and indexing them gives more information about the role. For example `{{len .Guild.Roles}}` gives you how many roles are there in that guild. Role struct has [following fields](https://discordapp.com/developers/docs/topics/permissions#role-object). |
| .Guild.Splash                      | Outputs the [splash hash](https://discordapp.com/developers/docs/reference#image-formatting) ID of the guild's splash.                                                                                                                                                     |
| .Guild.SystemChannelID             | The id of the channel where guild notices such as welcome messages and boost events are posted.                                                                                                                                                                            |
| .Guild.VerificationLevel           | Outputs the required verification level for the guild.                                                                                                                                                                                                                     |
| .Guild.VoiceStates                 | Outputs a slice of voice states (users connected to VCs) with type _\[]discordgo.VoiceState._                                                                                                                                                                              |
| .Guild.WidgetChannelID             | Outputs the channel ID for the server widget.                                                                                                                                                                                                                              |
| .Guild.WidgetEnabled               | Outputs whether or not the Server Widget is enabled or not.                                                                                                                                                                                                                |

| **Method**                                                   | **Description**                                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `.Guild.GetChannel id`                                       | Gets the channel with the ID provided, returning a _\*dstate.ChannelState_.                                                                                                                                                                                                                 |
| `.Guild.GetEmoji id`                                         | Gets the guild emoji with the ID provided, returning a _\*discordgo.Emoji._                                                                                                                                                                                                                 |
| `.Guild.GetMemberPermissions channelID memberID memberRoles` | Computes the permissions that the member has in the channel provided, taking into account the roles of the member. Example: `{{.Guild.GetMemberPermissions .Channel.ID .Member.User.ID .Member.Roles}}` would retrieve the permission bit the triggering member has in the context channel. |
| `.Guild.GetRole id`                                          | Gets the role with the ID provided, returning a _\*discordgo.Role._                                                                                                                                                                                                                         |
| `.Guild.GetVoiceState userID`                                | Gets the voice state of the user ID provided, returning a _\*discordgo.VoiceState_. Example code to show if user is in VC or not: `{{if .Guild.GetVoiceState .User.ID}} user is in voice channel {{else}} user is not in voice channel {{end}}`                                             |

[Guild object in Discord documentation](https://discordapp.com/developers/docs/resources/guild#guild-object).

## Member

| **Field**        | **Description**                                                                                                            |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------- |
| .Member.JoinedAt | When member joined the guild/server of type _discordgo.Timestamp_. Method .Parse will convert this to of type _time.Time_. |
| .Member.Nick     | The nickname for this member.                                                                                              |
| .Member.Roles    | A _slice_ of role IDs that the member has.                                                                                 |
| .Member.User     | Underlying user on which the member is based on.                                                                           |

[Member object in Discord documentation](https://discordapp.com/developers/docs/resources/guild#guild-member-object).

User functions are covered [here](https://docs.yagpdb.xyz/reference/templates/functions#member).

## User

| **Field**             | **Description**                                                                                                                                           |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| .User                 | The user's username together with discriminator.                                                                                                          |
| .User.Avatar          | The user's avatar ID.                                                                                                                                     |
| .User.AvatarURL "256" | <p>Gives the URL for user's avatar, argument "256" is the size of the picture <br>and can increase/decrease twofold (e.g. 512, 1024 or 128, 64 etc.).</p> |
| .User.Bot             | Determines whether the target user is a bot - if yes, it will return `true`.                                                                              |
| .User.Discriminator   | The user's discriminator (The four digits after a person's username).                                                                                     |
| .User.ID              | The user's ID.                                                                                                                                            |
| .User.Mention         | Mentions user.                                                                                                                                            |
| .User.String          | The user's username together with discriminator as _string_ type.                                                                                         |
| .User.Username        | The user's username.                                                                                                                                      |
| .UsernameHasInvite    | Only works with join and leave messages (not join dms). It will determine does the username contain an invite link.                                       |
| .RealUsername         | Only works with join and leave messages (not join DMs). This can be used to send the real username to a staff channel when invites are censored.          |

[User object in Discord documentation](https://discordapp.com/developers/docs/resources/user#user-object).

User functions are covered [here](https://docs.yagpdb.xyz/reference/templates/functions#user).

## Channel

| **Field**          | **Description**                                                                                                                |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| .Channel.Bitrate   | Bitrate used; only set on voice channels.                                                                                      |
| .Channel.GuildID   | Guild ID of the channel.                                                                                                       |
| .Channel.ID        | The ID of the channel.                                                                                                         |
| .Channel.IsPrivate | Whether the channel is private.                                                                                                |
| .Channel.IsThread  | Whether the channel is a thread.                                                                                               |
| .Channel.Mention   | Mentions the channel object.                                                                                                   |
| .Channel.Name      | The name of the channel.                                                                                                       |
| .Channel.NSFW      | Outputs whether this channel is NSFW or not.                                                                                   |
| .Channel.ParentID  | The ID of the channel's parent (category), returns 0 if none.                                                                  |
| .Channel.Position  | Channel position from top-down.                                                                                                |
| .Channel.Topic     | The topic of the channel.                                                                                                      |
| .Channel.Type      | The type of the channel. [Explained here.](https://discord.com/developers/docs/resources/channel#channel-object-channel-types) |

[Channel object in Discord documentation](https://discordapp.com/developers/docs/resources/channel#channel-object).

Channel functions are covered [here](https://docs.yagpdb.xyz/reference/templates/functions#channel).

## Message

| **Field**                  | **Description**                                                                                                                                                                                                                                                             |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| .Message.Attachments       | Attachments of this message (_slice_ of attachment objects).                                                                                                                                                                                                                |
| .Message.Author            | Author of the message ([User](./#user) object).                                                                                                                                                                                                                             |
| .Message.ChannelID         | Channel ID this message is in.                                                                                                                                                                                                                                              |
| .Message.Content           | Text content on this message.                                                                                                                                                                                                                                               |
| .Message.EditedTimestamp   | The time at which the last edit of the message occurred, if it has been edited. As with .Message.Timestamp, it is of type _discordgo.Timestamp._                                                                                                                            |
| .Message.Embeds            | Embeds of this message (_slice_ of embed objects).                                                                                                                                                                                                                          |
| .Message.GuildID           | Guild ID in which the message is.                                                                                                                                                                                                                                           |
| .Message.ID                | ID of the message.                                                                                                                                                                                                                                                          |
| .Message.Link              | Discord link to the message. \*                                                                                                                                                                                                                                             |
| .Message.Member            | [Member object](./#member). \*                                                                                                                                                                                                                                              |
| .Message.MentionEveryone   | Whether the message mentions everyone.                                                                                                                                                                                                                                      |
| .Message.MentionRoles      | The roles mentioned in the message, returned as a slice of type _discordgo.IDSlice._                                                                                                                                                                                        |
| .Message.Mentions          | Users this message mentions, returned as a slice of type _\[]\*discordgo.User._                                                                                                                                                                                             |
| .Message.Pinned            | Whether this message is pinned.                                                                                                                                                                                                                                             |
| .Message.Reactions         | Reactions on this message (only available from getMessage).                                                                                                                                                                                                                 |
| .Message.ReferencedMessage | Message object associated by message\_reference, like a message that was replied to.                                                                                                                                                                                        |
| .Message.Timestamp         | Timestamp of the message in type _discordgo.Timestamp_ (use .Message.Timestamp.Parse to get type _time.Time_ and .Parse.String method returns type _string_).                                                                                                               |
| .Message.Tts               | Whether the message is text-to-speech. \*                                                                                                                                                                                                                                   |
| .Message.Type              | The [type](https://discordapp.com/developers/docs/resources/channel#message-object-message-types) of the message.                                                                                                                                                           |
| .Message.WebhookID         | If the message is generated by a webhook, this is the webhook's id                                                                                                                                                                                                          |
| .Args                      | List of everything that is passed to .Message.Content. .Args is a _slice_ of type _string_.                                                                                                                                                                                 |
| .Cmd                       | .Cmd is of type _string_ and shows all arguments that trigger custom command, part of .Args. Starting from `{{index .Args 0}}`.                                                                                                                                             |
| .CmdArgs                   | List of all the arguments passed after `.Cmd` (`.Cmd` is the actual trigger) `.CmdArgs` is a _slice_ of type _string_. Examples in [misc. snippets](./#miscellaneous-snippets).                                                                                             |
| .StrippedMsg               | "Strips" or cuts off the triggering part of the message and prints out everything else after that. Bear in mind, when using regex as trigger, for example `"day"` and input message is `"Have a nice day my dear YAG!"` output will be `"my dear YAG!"`  - rest is cut off. |

\* denotes field that will not have proper return when using `getMessage` function.

[Message object in Discord documentation](https://discordapp.com/developers/docs/resources/channel#message-object).

Message functions are covered [here](https://docs.yagpdb.xyz/reference/templates/functions#message).

{% hint style="info" %}
More information about the `Message` object can be found [here](../../commands/custom-commands.md#the-message-template).
{% endhint %}

## Reaction

This is available and part of the dot when reaction trigger type is used.

| **Field**                     | **Description**                                                                                                                                                                                                                                                                                                                                           |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| .Reaction                     | <p> Returns reaction object which has following fields <code>UserID</code>, <code>MessageID</code>, <br><code>Emoji.(ID/Name/...)</code>, <code>ChannelID</code>, <code>GuildID</code>. Emoji.ID is the ID of the emoji for custom emojis, and Emoji.Name will hold the unicode emoji if its a default one. (otherwise the name of the custom emoji).</p> |
| .Reaction.Emoji.APIName       | Returns type _string_, an correctly formatted API name for use in the MessageReactions endpoints. For custom emojis it is `emojiname:ID`.                                                                                                                                                                                                                 |
| .Reaction.Emoji.MessageFormat | Returns a correctly formatted emoji for use in Message content and embeds. It's equal to `<:.Reaction.Emoji.APIName>` and `<a:.Reaction.Emoji.APIName>` for animated emojis.                                                                                                                                                                              |
| .ReactionAdded                | Returns a boolean type _bool_ true/false indicating whether reaction was added or removed.                                                                                                                                                                                                                                                                |
| .ReactionMessage              | <p>Returns the message object reaction was added to. </p><p><code>{{range .ReactionMessage.Reactions}}</code><br><code>{{.Count}} - {{.Emoji.Name}}</code> <br><code>{{end}}</code></p><p>Returns emoji count and their name.</p><p>Has an alias .Message and it works the same way.</p>                                                                  |

[Reaction object in Discord documentation](https://discordapp.com/developers/docs/resources/channel#reaction-object).\
[Emoji object in Discord documentation.](https://discord.com/developers/docs/resources/emoji)

## Conditional branching

Branching using `if` action's pipeline and comparison operators - these operators don't need to be inside `if` branch. `if` statements always need to have an enclosing `end`.\
Learning resources covers conditional branching [more in depth](https://learn.yagpdb.xyz/beginner/control\_flow\_1).\


{% hint style="success" %}
`eq` , though often used with 2 arguments (`eq x y`) can actually be used with more than 2. If there are more than 2 arguments, it checks whether the first argument is equal to any one of the following arguments. This behaviour is unique to `eq`.
{% endhint %}

{% hint style="info" %}
Comparison operators always require the same type: i.e comparing `1.23` and `1` would throw **`incompatible types for comparison` ** error as they are not the same type (one is float, the other int). To fix this, you should convert both to the same type -> for example, `toFloat 1`.
{% endhint %}

| **Case**                  | **Example**                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| if                        | <p><code>{{if (condition)}} output {{end}}</code></p><p>Initialization statement can also be inside <code>if</code> statement with conditional statement, limiting the initialized scope to that <code>if</code> statement. <br><code>{{$x := 24}}</code> <br><code>{{if eq ($x := 42) 42}} Inside: {{$x}} {{end}}</code> <br><code>Outside: {{$x}}</code></p> |
| else if                   | <p><code>{{if (condition)}} output1 {{else if (condition)}} output2 {{end}}</code></p><p>You can have as many<code>else if</code>statements as many different conditionals you have.</p>                                                                                                                                                                       |
| else                      | `{{if (condition)}} output1 {{else}} output2 {{end}}`                                                                                                                                                                                                                                                                                                          |
| not                       | `{{if not (condition)}} output {{end}}`                                                                                                                                                                                                                                                                                                                        |
| and                       | `{{if and (cond1) (cond2) (cond3)}} output {{end}}`                                                                                                                                                                                                                                                                                                            |
| or                        | `{{if or (cond1) (cond2) (cond3)}} output {{end}}`                                                                                                                                                                                                                                                                                                             |
| Equal: eq                 | `{{if eq .Channel.ID ########}} output {{end}}`                                                                                                                                                                                                                                                                                                                |
| Not equal: ne             | `{{$x := 7}} {{$y := 8}} {{ne $x $y}}` returns `true`                                                                                                                                                                                                                                                                                                          |
| Less than: lt             | `{{if lt (len .Args) 5}} output {{end}}`                                                                                                                                                                                                                                                                                                                       |
| Less than or equal: le    | `{{$x := 7}} {{$y := 8}} {{le $x $y}}` returns `true`                                                                                                                                                                                                                                                                                                          |
| Greater than: gt          | `{{if gt (len .Args) 1}} output {{end}}`                                                                                                                                                                                                                                                                                                                       |
| Greater than or equal: ge | `{{$x := 7}} {{$y := 8}} {{ge $x $y}}` returns `false`                                                                                                                                                                                                                                                                                                         |

## Custom Types

Golang has built-in primitive data types (_int_, _string_, _bool_, _float64_, ...) and built-in composite data types (_array_, _slice_, _map_, ...) which also are used in custom commands. \
\
YAGPDB's templating "engine" has currently two user-defined, custom data types - _templates.Slice_ and _templates.SDict_. There are other custom data types used like _discordgo.Timestamp_, __ but these are outside  of the main code of YAGPDB, so not explained here further. Type _time.Time_ is covered in its own [section](./#time).\
\
Custom Types section discusses functions that initialize values carrying those _templates.Slice_ (abridged to _cslice_), _templates.SDict_ (abridged to _sdict_) types and their methods. Both types handle type _interface{}_ element. It's called an empty interface which allows a value to be of any type. So any argument of any type given is handled. (In "custom commands"-wise mainly primitive data types, but _slices_ as well.)

{% hint style="warning" %}
**Reference type-like behaviour:** Slices and dictionaries in CC exhibit reference-type like behavior, which may be undesirable in certain situations. That is, if you have a variable `$x` that holds a slice/dictionary, writing `$y := $x` and then mutating `$y` via `Append`/`Set`/`Del`/etc. will modify `$x` as well. For example:

```
{{ $x := sdict "k" "v" }}
{{ $y := $x }}
{{ $y.Set "k" "v2" }} {{/* modify $y */}}
{{ $x }}
{{/* k has value v2 on $x as well - 
that is, modifying $y changed $x too. */}}
```

If this behaviour is undesirable, copy the slice/dictionary via `cslice.AppendSlice` or a `range` + `Set` call .

```
{{ $x := sdict "k" "v" }}
{{ $y := sdict }}
{{ range $k, $v := $x }} {{- $y.Set $k $v -}} {{ end }}
{{ $y.Set "k" "v2" }}
{{ $x }} {{/* $x is unmodified - k still has value v */}}
```

Note that this performs a shallow copy, not a deep copy - if you want the latter you will need to perform the aforementioned operation recursively.
{% endhint %}

### templates.Slice

`templates.Slice` - This is a custom composite data type defined using an underlying data type _\[]interface{}_ . It is of kind _slice_ (similar to _array_) having _interface{}_ type as its value and can be initialized using `cslice` function. Retrieving specific element inside _templates.Slice_ is by indexing its position number.

| **Function**               | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `cslice value1 value2 ...` | <p>Function creates a slice of type <em>templates.Slice</em> that can be used elsewhere (as an argument for <code>cembed</code> and <code>sdict</code> for example).<br></p><p>Example: <code>cslice 1 "2" (dict "three" 3) 4.5</code> returns <code>[1 2 map[three:3] 4.5]</code>, having length of 4 and index positions from 0 to 3. Notice that thanks to type <em>interface{}</em> value, <em>templates.Slice</em> elements' inherent type does not change.</p> |

| Method                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| .Append arg              | Creates a new _cslice_ having given argument appended fully by its type to current value. Has max size of 10 000 length.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| .AppendSlice arg         | Creates a new _cslice_ from argument of type _slice_ appended/joined with current value. Has max size of 10 000 length.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| .Set int value           | Changes/sets given _int_ argument as index position of current _cslice_ to new value. Note that .Set can only set indexes which already exist in the slice.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| .StringSlice strict-flag | <p>Compares <em>slice</em> contents - are they of type <em>string,</em> based on the strict-flag which is <em>boolean</em> and is by default <em>false.</em> Under these circumstances if the element is a <em>string</em> then those elements will be included as a part of the <em>[]string</em> slice and rest simply ignored. Also <em>time.Time</em> elements - their default <em>string</em> notation will be included. If none are <em>string</em> an empty <em>[]string</em> slice is returned.</p><p>If strict-flag is set to <em>true</em> it will return a <em>[]string</em> only if <strong>all</strong> elements are pure <em>string</em>, else <code>&#x3C;no value></code> is returned.</p><p>Example in this section's <a href="./#this-sections-snippets-2">Snippets</a>.</p> |

#### This section's snippets:

* To demonstrate .StringSlice `{{(cslice currentTime.Month 42 "YAPGDB").StringSlice}}` will return a slice `[February YAGPDB]`. If the flag would have been set to true - {{...).StringSlice true}}, all elements in that slice were not strings and `<no value>` is returned.

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

`templates.SDict` - This is a custom composite data type defined on an underlying data type _map\[string]interface{}._ This is of kind _map_ having _string_ type as its key and _interface{}_ type as that key's value and can be  initialized **** using `sdict` function. A map is key-value store. This means you store value and you access that value by a key. Map is an unordered list and the number of parameters to form key-value pairs must be even, difference to regular _map_ is that `templates.SDict` is ordered by its key. Retrieving specific element inside _templates.Sdict_ is by indexing its key.

| **Function**                            | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sdict "key1" value1 "key2" value2 ...` | <p>Like dict function, creating a <em>templates.SDict</em> type map, key must be of type <em>string</em>. Can be used for example in <code>cembed</code>. If only one argument is passed to <code>sdict</code> function having type <em>map[string]interface{};</em> for example .ExecData and data retrieved from database can be of such type if <code>sdict</code> was used, it is converted to a new <em>sdict</em>.</p><p></p><p>Example: <code>sdict "one" 1 "two" 2 "three" (cslice 3 4) "five" 5.5</code> returns unordered <code>map[five:5.5 one:1 three:[3 4] two:2]</code>, having length of four and index positions are its keys. Notice that thanks to type <em>interface{}</em> value, <em>templates.SmDict</em> elements' inherent type does not change.</p> |

| **Method**       | **Description**                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------- |
| .Del "key"       | Deletes given key from _sdict_.                                                             |
| .Get "key"       | Retrieves given key from _sdict_.                                                           |
| .Set "key" value | Changes/sets given key to a new value or creates new one, if no such key exists in _sdict_. |

```go
Creating sdict: {{ $x := sdict "color1" "green" "color2" "red" }} **{{ $x }}**
Retrieving key "color2": **{{ $x.Get "color2" }}**
Changing "color2" to "yellow": {{ $x.Set "color2" "yellow" }} **{{ $x }}**
Adding "color3" as "blue": {{ $x.Set "color3" "blue" }} **{{ $x }}**
Deleting key "color1" {{ $x.Del "color1" }} and whole sdict: **{{ $x }}**
```

{% hint style="success" %}
**Tip:** Previously, when saving cslices, sdicts, and dicts into database, they were serialized into their underlying native types - slices and maps. This meant that if you wanted to get the custom type back, you needed to convert manually, e.g. `{{cslice.AppendSlice $dbSlice}}` or `{{sdict $dbDict}}`. Recent changes to YAG have changed this: values with custom types are now serialized properly, making manual conversion unnecessary.
{% endhint %}

## Database

You have access to a basic set of Database functions having return of type _\*customcommands.LightDBEntry_ called here [DBEntry](./#dbentry). \
This is almost a key value store ordered by the key and value combined.

You can have max 50 \* user\_count (or 500 \* user\_count for premium) values in the database, if you go above this all new write functions will fail, this value is also cached so it won't be detected immediately when you go above nor immediately when you're under again.

Patterns are basic PostgreSQL patterns, not Regexp: An underscore `(_)`  matches any single character; a percent sign `(%)` matches any sequence of zero or more characters.

Keys can be max 256 bytes long and has to be strings or numbers. Values can be anything, but if their serialized representation exceeds 100kB an error will be raised.

You can just pass a `userID`of 0 to make it global (or any other number, but 0 is safe).\
\
There can be 10 database interactions per CC, out of which dbTop/BottomEntries, dbCount, dbGetPattern, and dbDelMultiple may only be run twice. (50,10 for premium users).

Learning resources covers database [more in-depth](https://learn.yagpdb.xyz/intermediate/custom-command-database).

**Database functions** are covered [here](https://docs.yagpdb.xyz/reference/templates/functions#database).

[Example here](../custom-command-examples.md#database-example).

### DBEntry

| **Fields** | **Description**                                                                                                         |
| ---------- | ----------------------------------------------------------------------------------------------------------------------- |
| .ID        | ID of the entry.                                                                                                        |
| .GuildID   | ID of the server.                                                                                                       |
| .UserID    | Value of `userID` argument or ID of the user if for example `.User.ID` was used for `dbSet`.                            |
| .User      | User object of type _discordgo.User_ having only `.ID` field, .Mention is still usable with correct userID field entry. |
| .CreatedAt | When this entry was created.                                                                                            |
| .UpdatedAt | When this entry was last updated.                                                                                       |
| .ExpiresAt | When entry will expire.                                                                                                 |
| .Key       | The key of the entry.                                                                                                   |
| .Value     | The value of the entry.                                                                                                 |

## Range action

`range`iterates over element values in variety of data structures in pipeline - slices/arrays, maps or channels. The dot `.` is set to successive elements of those data structures and output will follow execution. If the value of pipeline has zero length, nothing is output or if an `{{else}}` action is used, that section will be executed.

Affected dot inside `range` is important because methods mentioned above in this documentation:`.Server.ID`, `.Message.Content` etc are all already using the dot on the pipeline and if they are not carried over to the `range` control structure directly, these fields do not exists and template will error out. Getting those values inside `range` and also `with` action would need `$.User.ID` for example.\
\
`range` on slices/arrays provides both the index and element for each entry; range on map iterates over key/element pairs. If a range action initializes a variable, that variable is set to the successive elements of the iteration. Range can also declare two variables, separated by a comma and set by index and element or key and element pair. In case of only one variable, it is assigned the element.\
\
Like `if`, `range`is concluded with`{{end}}`action and declared variable scope inside `range` extends to that point.\


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

{% hint style="danger" %}
**Custom command response was longer than 2k (contact an admin on the server...)**\
****This is quite common error users will get whilst using range. Simple example to reproduce it:\
_{{ range seq 0 1000 }}_\
_{{ $x := . }}_\
_{{ end }}_\
_HELLO!_\
__This will happen because of whitespaces and newlines, so make sure you one-line the range or trim spaces, in this context _{{- $x := . -}}_
{% endhint %}

## Tickets

{% hint style="warning" %}
Ticket functions are limited to 1 call per custom command for both normal and premium guilds.
{% endhint %}

| **Function**                | **Description**                                                                                                                                                                                                                                                                           |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `createTicket author topic` | Creates a new ticket with the author and topic provided. Author can be `nil` (to use the triggering member); user ID in form of a string or an integer; a user struct; or a member struct. The topic must be a string. Returns a [template ticket](./#template-ticket) struct on success. |

#### Template Ticket

| **Field**              | **Description**                                                                                               |
| ---------------------- | ------------------------------------------------------------------------------------------------------------- |
| .AuthorID              | Author ID of the ticket.                                                                                      |
| .AuthorUsernameDiscrim | The Discord tag of the author of the ticket, formatted like `username#discrim`.                               |
| .ChannelID             | Channel ID of the ticket.                                                                                     |
| .ClosedAt              | Time that the ticket was closed, of type _null.Time._ This is, for the most part, useless in custom commands. |
| .CreatedAt             | Time that the ticket was created.                                                                             |
| .GuildID               | Guild ID of the ticket.                                                                                       |
| .LocalID               | The ticket ID.                                                                                                |
| .LogsID                | Log ID of the ticket.                                                                                         |
| .Title                 | Title of the ticket.                                                                                          |

## Time

Time in general uses Golang's time package library > [https://golang.org/pkg/time/#time](https://golang.org/pkg/time/#Time) and also this although slightly different syntax all applies here > [https://gobyexample.com/time](https://gobyexample.com/time).

| **Field**     | **Description**                                                                                             |
| ------------- | ----------------------------------------------------------------------------------------------------------- |
| .DiscordEpoch | Gives you Discord Epoch time in _time.Time._ `{{.DiscordEpoch.Unix}}` would return in seconds > 1420070400. |
| .UnixEpoch    | Gives you Unix Epoch time in _time.Time._                                                                   |
| .TimeHour     | Variable of _time.Duration_ type and returns 1 hour > `1h0m0s`.                                             |
| .TimeMinute   | Variable of _time.Duration_ type and returns 1 minute > `1m0s`.                                             |
| .TimeSecond   | Variable of _time.Duration_ type and returns 1 second > `1s`.                                               |

Time functions are covered [here](https://docs.yagpdb.xyz/reference/templates/functions#time).

## With action

`with` lets you assign and carry pipeline value with its type as a dot `.` inside that control structure, it's like a shorthand. If the value of the pipeline is empty, dot is unaffected and when `{{else}}` is used, that branch is executed instead. \
\
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
* `{{if eq .Channel.ID #######}} YAG! {{end}}`Will only show `YAG!` if ChannelID is #####.
* `{{if ne .User.ID #######}} YAG! {{end}}`Will ignore if user ID equal to ##### uses command.
* `{{addReactions .CmdArgs}}` Adds the emoji following a trigger as reactions.
* `{{$a := (exec "catfact")}}` Saves the response of the `catfact` **** command to variable `$a`.&#x20;
* `{{$allArgs := (joinStr " " .CmdArgs)}}` Saves all the arguments after trigger to a variable `$allArgs`.&#x20;
* `{{/* this is a comment */}}`For commenting something inside a template, use this syntax. May contain newlines. Comments do not nest and they start and end at the delimiters.&#x20;
* To trim spaces, for example >`{{- /* this is a multi-line` \
  `comment with whitespace trimmed from  preceding and following text */ -}}` \
  Using`{{- ... -}}` is also handy inside`range` actions, because whitespaces and newlines are rendered there as output.
* To demonstrate sleep and slightly also editMessage functions. >\
  `{{$x := sendMessageRetID nil "Hello"}} {{sleep 3}} {{editMessage nil $x "There"}} {{sleep 5}} {{sendMessage nil "We all know, that"}} {{sleep 3}} YAGPDB rules!`
