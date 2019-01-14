# Custom Commands

Custom commands allow you to create your own commands, the custom command system in YAGPDB is somewhat complex and can be used for some advanced stuff. It is still somewhat limited in what it can do and for the the more complex and advanced operations, you should really think about making a standalone bot for it.

## Custom Commands

To create your first custom command, go to the control panel and select your server. There you click on Commands and Custom Commands. 

![The Custom Command Page](../.gitbook/assets/image%20%282%29.png)

### Trigger Types

* **Command**: With this trigger, the message has to start with the prefix for your server \(`-` by default\) followed by the trigger
* **Starts with**: When a message starts with your trigger
* **Contains**: When a message contains your trigger
* **Exact match**: When the entire message equals your trigger
* **Regex**: This trigger allows you to use a regex pattern. \(Refer to the [`Regex page`](../reference/regex.md) for help\)

#### Case Sensitivity

As you might have seen there is an option called _Case sensitive_. This option makes your trigger case sensitive. The trigger heLLo with case sensitivity on will only trigger if somebody says `heLLo` but not if someone says `hello`.

### Using templates in custom commands

{% hint style="info" %}
Some basic coding knowledge may be required to use some of these features. 
{% endhint %}

If you wish to do anything more then a _"Type in a command" -&gt; "Make the bot say something._ Such as assigning people roles, getting information on the person calling the command, writing messages in other channels, and many other. It is recommended that you check out this page:

{% page-ref page="../reference/templates.md" %}

### Restrictions to roles or channels

You can restrict or block custom commands to specific roles or channels. For this you have to select the corresponding checkbox and select the roles/channels you want it to apply too.

![This custom command can be executed by people that either have Coll Dog, Guy-in-charge or both.](../.gitbook/assets/image%20%281%29.png)

{% hint style="warning" %}
If you select the**`Require at least one of the`**or**`Only run in the`** Options, make sure to always have a role/channel selected otherwise the bot won't respond to your commands.
{% endhint %}

### Restrictions and limitations

With custom commands there are some limitations:

* You can't create more than 100 custom commands \(250 with YAGPDB Premium\)
* You can't execute more than five commands from a custom command
* Direct Messages can be only sent with a side note from which server they're coming
* Custom Command responses can't be longer than 2000 characters \(this is a limitation by discord\)
* A Custom command itself can't be longer than 3000 characters
* Custom Commands are limited to 5 userArg calls, 5 exec/execAdmin functions, 10 template function calls and 3 sendMessage calls

### Require arguments

As of v1.12 there's a simple set of functions available for you to manage arguments, they are:

```text
{{$args := parseArgs num-required-args "Custom usage text when invalid args provided"
    (carg "int" "name of arg1")
    (carg "string" "name of arg2")
    (more args can be added aswell...)}}
...

{{$args.Get 0}} <- will have the first arg
{{$args.Get 1}} <- will have the second arg
```

The execution will stop at wherever you placed "**parseArgs**" if incorrect args are passed.

"**carg**" has the following syntax:

```text
{{carg "type" "name" additional-options-depending-on-type}}
```

Available types and options are:

* **int -** whole numbers, you can also optionally specify min and max after the name
* **string -** text
* **user -** user mentions, will have the type of User \(see [templates ](../reference/templates.md#user)for more info\)
* **userid -** user id's, this user may not exist at all, both mentions and plain id's are accepted, will have the type of int64
* **channel -** channel mentions, will have the type of Channel \(see [templates ](../reference/templates.md#channel)for more info\)

To access the parsed args you use the "**Get**" function on the returned object from **parseArgs**, this function takes in the argument index starting from 0.

There is also a "**IsSet**" function that will return true or false depending on whether the argument was set or not, if this was a optional argument.

Example usage of optional args:

```text
{{$args := parseArgs 1 "Custom usage text when invalid args provided"
    (carg "int" "name of arg1")
    (carg "string" "name of arg2 (optional)")
    (more args can be added aswell...)}}
...

{{$args.Get 0}} <- will have the first arg
{{or ($args.Get 1) "value if the second arg was not used"}}
{{if $args.IsSet 1}} only runs if the second argument was provided {{end}}
```

### The Message template

You can fetch a message by ID or use the [trigger message](https://docs.yagpdb.xyz/reference/templates#message) and get some information about it. Message returns the following things that you can access with it:  


#### Message

| Field | Type | Description |
| :--- | :--- | :--- |
| .Message.ID | Int | ID of the message |
| .Message.ChannelID | Int | Channnel id this message is in |
| .Message.Author | [User Object](https://docs.yagpdb.xyz/reference/templates#user) | Author of the message \(User object\) |
| .Message.Timestamp | String | Timestamp of the message \(use .Message.Timestamp.Parse for a time object, otherwise string\) |
| .Message.Attachments | Array of [Attachments](https://docs.yagpdb.xyz/commands/custom-commands#attachment) | Attachments to this message \(slice of attachment objects\) |
| .Message.Embeds | Array of [Embeds](../others/custom-embeds.md#embeds-in-custom-commands) | Embeds on this message \(slice of embed objects\) |
| .Message.Mentions | Array of [User Object](https://docs.yagpdb.xyz/reference/templates#user) | Users this message mentions |
| .Message.Reactions | Array of [Reactions](https://docs.yagpdb.xyz/commands/custom-commands#reaction) | Reactions on this message \(only available form getMessage\) |
| .Message.Content | String | Text content on this message |

#### Attachment

Either starts with  `(index .Message.Attachments 0).` or a variable with the attachment type.

| Field | Type | Description |
| :--- | :--- | :--- |
| ID | Int | The ID of the attachment |
| URL | String | cdn.discordapp.com URL |
| ProxyURL | String | media.discordapp.com URL |
| Filename | String | Filename of the attachment |
| Width | Int | Width of the attachment \(if image\) in pixels |
| Height | Int | Height of the attachment \(if image\) in pixels |
| Size | Int | Size of the attachment in bytes |

#### Reaction

Either starts with `(index .Message.Reactions 0)` or a variable with the reaction type.

| Field | Type | Description |
| :--- | :--- | :--- |
| Count | Int | Times this emoji has been used to react |
| Emoji | [Emoji](https://docs.yagpdb.xyz/commands/custom-commands#emoji) | The emoji used in the reaction |

#### Emoji

Either starts with `(index .Message.Reactions 0).Emoji` or a variable of the reaction type.

| Field | Type | Description |
| :--- | :--- | :--- |
| ID | Int | ID of the emoji |
| Name | String | Name of the emoji \(if unicode emoji this will be the emote\) |
| User | [User Object](https://docs.yagpdb.xyz/reference/templates#user) |  User that created this emoji |
| Animated | Boolean | Whether the emoji is animated or not |

There is [more fields ](https://discordapp.com/developers/docs/resources/channel#reaction-object)which can be used, but they are either obsolete or only used with Global Emotes.  
Example to fetch the name of the first reaction on a message provided through the `getMessage` template:

```go
{{$message := getMessage nil (index .Args 1)}}
{{if $message}}
{{if (index $message.Reactions 0) }}
Name of the first reaction: {{(index $message.Reactions 0).Emoji.Name}}
{{else}}No reactions on this message{{end}}
{{else}}Unknown message{{end}}
```

 

### Examples of custom commands

You can find multiple examples on the YAGPDB Community & Support Server or in this list \(with explanations\):

{% page-ref page="../reference/custom-command-examples.md" %}

