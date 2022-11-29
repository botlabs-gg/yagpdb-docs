# Custom Commands

Custom commands - abbreviated as CCs, allow you to create your own commands. The CC-system in YAGPDB is quite complex and can be used for some advanced stuff, but even CCs are still limited and if your use case is very specific, consider trying or building another bot. Additional reading [here](https://learn.yagpdb.xyz/the-custom-command-interface). Custom Commands have also limits and they are covered [here](https://docs.yagpdb.xyz/reference/custom-commands-limits).

## Custom Commands

To create your first custom command, go to the control panel and select your server. There you click on Commands and Custom Commands.&#x20;

![The Custom Command Page](../.gitbook/assets/image\_custom\_commands.png)

### Trigger Types

* **Command**: With this trigger, the message has to start with the prefix for your server (`-` by default) followed by the trigger.
* **Starts with**: When a message starts with your trigger.
* **Contains**: When a message contains your trigger.
* **Regex**: This trigger allows you to use a regex pattern. (Refer to the [Regex page](../reference/regex.md) for help).
* **Exact match**: When the entire message equals your trigger.
* **Reaction:** CC is triggered by reactions.
* **Hourly interval**: This wi~~l~~l trigger after specified time given in hours. User can exclude certain hours and also weekdays. Channel must be selected for this trigger to work.
* **Minute interval**: Like hourly interval, the specified time is just in minutes starting from 5 min as minimum.

#### Case Sensitivity

As you might have seen, there is an option called _Case sensitive_. This option makes your trigger case-sensitive. The trigger heLLo with case sensitivity on will only trigger if somebody says `heLLo` but not if someone says `hello`.

### Restrictions to roles or channels

You can restrict or block custom commands to specific roles or channels. For this you have to select the corresponding checkbox and select the roles/channels you want it to apply too.

![This custom command can be executed by people that either have Coll Dog, Guy-in-charge or both.](../.gitbook/assets/image\_custom\_commands\_restrictions.png)

{% hint style="warning" %}
If you select the**`Require at least one of the`**or**`Only run in the`** Options, make sure to always have a role/channel selected otherwise the bot won't respond to your commands.
{% endhint %}

### Restrictions and limitations

With custom commands there are some limitations:

* You can't create more than 100 active custom commands (250 with YAGPDB Premium)
* You can't execute more than five commands from a custom command using `execAdmin` or `exec`
* Direct Messages can be only sent with a side note from which server they're coming
* Custom Command responses can't be longer than 2000 characters (this is a limitation by Discord).
* A Custom command itself can't be longer than 10 000 characters (this is total count of characters and sum of all subset custom command's responses of 20), also leave/join messages limit is 5000.
* Custom Commands have [limits](https://docs.yagpdb.xyz/reference/custom-commands-limits).
* No more than 3 custom commands may be executed from a single message for non-premium. The limit is 5 for premium servers.

## Advanced Custom Commands&#x20;

{% hint style="info" %}
Some basic coding knowledge may be required to use some of these features.&#x20;
{% endhint %}

### Using templates in custom commands

If you wish to do anything more than a _"Type in a command" -> "Make the bot say something._ Such as assigning people roles, getting information on the person calling the command, writing messages in other channels, and many others. It is recommended that you check out this page:

{% content-ref url="../reference/templates/" %}
[templates](../reference/templates/)
{% endcontent-ref %}

### Require arguments

As of v1.12 there's a simple set of functions available for you to manage arguments, they are:

```
{{$args := parseArgs num-required-args "Custom usage text when invalid args provided"
    (carg "int" "name of arg1")
    (carg "string" "name of arg2")
    (more args can be added aswell...)}}
...

{{$args.Get 0}} {{/* <- will have the first arg */}}
{{$args.Get 1}} {{/* <- will have the second arg */}}
```

The execution will stop at wherever you placed "**parseArgs**" if incorrect args are passed.

"**carg**" has the following syntax:

```
{{carg "type" "name" additional-options-depending-on-type}}
```

Available types and options are:

* **channel -** channel id/mention, will have the type of _\*templates.CtxChannel_ (see [templates ](../reference/templates/#channel)for more info). Threads are not supported
* **duration** - converts given integer number starting from minutes or string with modifier (s, m, h, w etc)  to type Duration - e.g. 10 is 10m0s and 123s is 2m3s (type _time.Duration_ is represented as an _int64_ nanosecond count - so 5s would be 5000000000). Has additional options after the name for min and max range of duration presented in nanoseconds.
* **float -** decimal numbers, you can also optionally specify min and max after the name similar to **int**. It is parsed as _float64_ datatype.
* **int -** whole numbers, you can also optionally specify min and max after the name. For example\
  `{{carg "int" "integer" 2 9}}` required argument has to be a number from 2 to 9.
* **member** - accepts userID/mention. Gives guild's member struct (object) to use later with .Member methods, like .JoinedAt. (see [templates ](../reference/templates/#member)for more info).
* **role** - matches an id or name of a role and returns a _\*discordgo.Role_ type [role object](https://discord.com/developers/docs/topics/permissions#role-object).
* **string -** text. If string-type is the last or only `carg` in `parseArgs` definition, it will take all arguments starting from that point.
* **user -** user mentions, will have the type of User (see [templates ](../reference/templates/#user)for more info).
* **userid -** user IDs, this user may not exist at all, both mentions and plain IDs are accepted, will have the type of _int64_.

To access the parsed args you use the "**Get**" method on the returned object from **parseArgs**, this function takes in the argument index starting from 0.

Method "**IsSet**" will return a boolean true or false depending on whether the argument was set or not, if this was an optional argument.

Example usage of optional args:

```
{{$args := parseArgs 1 "Custom usage text when invalid args provided"
    (carg "int" "name of arg1")
    (carg "string" "name of arg2 (optional)")
    (more args can be added aswell...)}}
...

{{$args.Get 0}} {{/* <- will have the first arg */}}
{{or ($args.Get 1) "value if the second arg was not used"}}
{{if $args.IsSet 1}} only runs if the second argument was provided {{end}}
```

### The Message template

You can fetch a message by ID or use the [trigger message](../reference/templates/#message) and get some information about it. Some fields message object has are as follows:\


Message

| Field                | Type                                                                                | Description                                                                                 |
| -------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| .Message.ID          | Int                                                                                 | ID of the message                                                                           |
| .Message.ChannelID   | Int                                                                                 | Channel id this message is in                                                               |
| .Message.Author      | [User Object](../reference/templates/#user)                                         | Author of the message (User object)                                                         |
| .Message.Timestamp   | String                                                                              | Timestamp of the message (use .Message.Timestamp.Parse for a time object, otherwise string) |
| .Message.Attachments | Array of [Attachments](https://docs.yagpdb.xyz/commands/custom-commands#attachment) | Attachments to this message (slice of attachment objects)                                   |
| .Message.Embeds      | Array of [Embeds](../reference/custom-embeds.md#embeds-in-custom-commands)          | Embeds on this message (slice of embed objects)                                             |
| .Message.Mentions    | Array of [User Object](../reference/templates/#user)                                | Users this message mentions                                                                 |
| .Message.Reactions   | Array of [Reactions](https://docs.yagpdb.xyz/commands/custom-commands#reaction)     | Reactions on this message (only available form getMessage)                                  |
| .Message.Content     | String                                                                              | Text content on this message                                                                |

#### Attachment

Either starts with  `(index .Message.Attachments 0).` or a variable with the attachment type.

| Field     | Type   | Description                                   |
| --------- | ------ | --------------------------------------------- |
| .ID       | Int    | The ID of the attachment                      |
| .URL      | String | cdn.discordapp.com URL                        |
| .ProxyURL | String | media.discordapp.com URL                      |
| .Filename | String | Filename of the attachment                    |
| .Width    | Int    | Width of the attachment (if image) in pixels  |
| .Height   | Int    | Height of the attachment (if image) in pixels |
| .Size     | Int    | Size of the attachment in bytes               |

#### Reaction

Either starts with `(index .Message.Reactions 0)` or a variable with the reaction type.

| Field  | Type                                                            | Description                             |
| ------ | --------------------------------------------------------------- | --------------------------------------- |
| .Count | Int                                                             | Times this emoji has been used to react |
| .Emoji | [Emoji](https://docs.yagpdb.xyz/commands/custom-commands#emoji) | The emoji used in the reaction          |

#### Emoji

Either starts with `(index .Message.Reactions 0).Emoji` or a variable of the reaction type.

| Field     | Type    | Description                                                 |
| --------- | ------- | ----------------------------------------------------------- |
| .ID       | Int     | ID of the emoji                                             |
| .Name     | String  | Name of the emoji (if Unicode emoji this will be the emote) |
| .Animated | Boolean | Whether the emoji is animated or not                        |

| **Method**       | **Description**                                                                                        |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| `.APIName`       | Returns a correctly formatted API name for use with reaction functions. Example output: `emojiname:id` |
| `.MessageFormat` | Returns a correctly formatted emoji for use in message content.                                        |

There are [more fields ](https://discordapp.com/developers/docs/resources/channel#reaction-object)which can be used, but they are either obsolete or only used with Global Emotes.\
Example to fetch the name of the first reaction on a message provided through the `getMessage` template:

```go
{{$message := getMessage nil (index .Args 1)}}
{{if $message}}
{{if $message.Reactions}}
Name of the first reaction: {{(index $message.Reactions 0).Emoji.Name}}
{{else}}No reactions on this message{{end}}
{{else}}Unknown message{{end}}
```

&#x20;

### currentTime template

The currentTime template is very extensive and can be used for displaying the current time, for different time zones, or in embeds in the "timestamp" field.\
\
even more in depth here > [https://golang.org/pkg/time/](https://golang.org/pkg/time/)

{% code title="As timestamp in an embed" %}
```go
{{ $embed := cembed "timestamp" currentTime }}
```
{% endcode %}

```go
{{/* golang time formating is POSIX form 0 1 2 3 4 5 6 > Mon 2 Jan 15:04:05 2006 (timezone calculation is omitted) */}}
{{/* currentTime.UTC.Format "15:04"  > gives current time in UTC */}}
{{/* ".Add" adds time in nanoseconds, in this example 2 hours have been added for UTC+2 */}}
{{ $marker := "void" }}

{{ if gt ( toInt ( currentTime.UTC.Format "15" ) ) 12 }}
{{ $marker = "PM" }}
{{ else }}
{{ $marker = "AM" }}
{{ end }}

{{/* current time in UTC+2 and in 12H format */}}
{{ ( joinStr " " ( ( currentTime.Add 7200000000000 ).Format "3:04"  ) $marker ) }}

It's the {{currentTime.Day}}. of {{currentTime.Month}} in the year {{currentTime.Year}}!
{{/*Protip: you can put PM in the format string as "3:04PM"
the variable $marker is there just to show if comparison as well.
More > https://golang.org/pkg/time/#pkg-constants*/}}
```

### Examples of custom commands

You can find multiple examples on the YAGPDB Community & Support Server or in this list (with explanations):

{% content-ref url="../reference/custom-command-examples.md" %}
[custom-command-examples.md](../reference/custom-command-examples.md)
{% endcontent-ref %}
