# Custom Commands Examples

{% hint style="warning" %}
This isn't the actual page about custom commands. A brief overview about custom commands can be found [here](https://docs.yagpdb.xyz/custom-commands).
{% endhint %}

### Controlled randomizer example

YAGPDB has a built-in random response system for custom commands, but sometimes you may want to control the chances for certain responses to occur. You can do this by creating a singular response and creating a variable with randInt. Then use an if else if statement like this to print out your desired output. 

```go
{{$var := randInt 1 100}}

{{if lt $var 10}}
This has a 10% chance of being triggered
{{else if lt $var 35}}
This has a 25% chance of being triggered
{{else}}
This has a 65% chance of being triggered
{{end}}
```

### Silent execution of commands or storage in a variable

If you create a custom command with exec or execAdmin you might not want the response for the executed command to show. You can suppress the response of a command like the following:

Trigger type: `Command` Trigger: `updates`

```go
{{$a := (exec "role" "yagpdb")}}
Oh hi there, I just ran the role command. 
{{/*$a*/}} Remove the /* and the * / if you want the response to be displayed.
```

The variable `$a` will store the output of running the role command and you can then just print out your own response.

### Range example

This command will teach you on how the range command works. It works really well for iterating through all your inputs. 

This particular command will let the bot repeat everything that was being said behind the command \(be careful with this one as there are ways to abuse it\). 

Trigger type: `Command` Trigger: `repeat`

```go
{{range $k, $v := .CmdArgs}}{{$v}}{{end}}
```

`$k` is the iteration number you are on, starting at 0 and `$v` is the current word in your input that you are on. 

### Dictionary example

A dictionary does not currently have a lot of piratical use, since YAGPDB has a built-in randomizer for the custom commands. In case you ever find yourself needing to use it, here's how to set it up.

Trigger type: `Command` Trigger: `dict`

```go
{{$options := (dict "0" "test" "1" "test1" "2" "test2")}}
{{$d := randInt (len $options)}}
{{index $options (toString $d)}}
```

### parseArgs example

The `parseArgs` template can check if specific arguments are given. If not, it will return a custom error message. It also checks if specific args are of a specific type and simplifies the argument management. Available types for `carg` are:

* `int` \(whole number\)
* `string` \(text\)
* `user` \(user mentions as type user\)
* `userid` \(mentions or the user's ID, as integer\)
* `channel` \(channel mention or ID, as type channel\)

Trigger type: `Command` Trigger: `send` 

```go
{{$args := parseArgs 2 "Syntax is <channel> <text>"
    (carg "channel" "channel to send to")
    (carg "string" "text to send")}}

{{sendMessage ($args.Get 0).ID ($args.Get 1)}}
```

### execCC example

This example consists of two custom commands, and after copy/paste `REPLACE-WITH-...` arguments need to be replaced by actual custom command ID's in your system. This custom command is very complex, uses very many advanced functions, all it does, constructs a 10 second countdown timer command-system for given starting time.

```go
{{$args := parseArgs 2 ""
 (carg "duration" "countdown-duration")
 (carg "string" "countdown-message")}}

{{$t := currentTime.Add ($args.Get 0)}}
{{$mID := sendMessageRetID nil (joinStr  "" "countdown starting..." $t.String)}}
{{execCC REPLACE-WITH-NEXT-CC-ID nil 0 (sdict "MessageID" $mID "T" $t "Message" ($args.Get 1)) }}
```

Second part of the custom commands, here we see, how `data`-part of exeCC was made in previous custom command as `sdict`and now we are calling those keys with `.ExecData` - for example `.ExecData.MessageID` sets new variable the same as stated in previous code.

```go
{{$timeLeft := .ExecData.T.Sub currentTime}}
{{$cntDownMessageHeader := joinStr "" "Countdown Timer: " .ExecData.Message}}
{{$formattedTimeLeft := humanizeDurationSeconds $timeLeft}}

{{$t := .ExecData.T}}
{{$mID := .ExecData.MessageID}}
{{$ts := .TimeSecond}}

{{if lt $timeLeft (mult .TimeSecond 30)}}
  {{range seq 1 (toInt $timeLeft.Seconds) }}
    {{$timeLeft := $t.Sub currentTime}}
    {{$formattedTimeLeft := humanizeDurationSeconds $timeLeft}}

    {{editMessage nil $mID (joinStr "" $cntDownMessageHeader "\nTime left: " $formattedTimeLeft " seconds")}}
    {{if gt $timeLeft $ts}} {{sleep 1}} {{end}}
  {{end}}
  {{editMessage nil  .ExecData.MessageID (joinStr "" $cntDownMessageHeader "\nTime left: **ENDED**")}}
{{else}}
    {{editMessage nil .ExecData.MessageID (joinStr "" $cntDownMessageHeader "\nTime left: " $formattedTimeLeft)}}
    {{execCC REPLACE-WITH-CURRENT-CC-ID nil 10 .ExecData}}
{{end}}
```

![Jonas&apos; using YAGPDB testing bot here, same execCC custom commands.](../.gitbook/assets/unknown.png)

### Database example

This is a simple note taking system having 3 separate custom commands. Also notice that actual name of the key inserted to database begins with "notes\_".

#### Save note:

```go
{{$args := parseArgs 2 ""
  (carg "string" "key")
  (carg "string" "value")}}

{{dbSet .User.ID (joinStr "" "notes_" ($args.Get 0)) ($args.Get 1)}}
Saved `{{$args.Get 0}}` as `{{$args.Get 1}}`
```

#### Get note:

```go
{{$key := joinStr "" "notes_"  .StrippedMsg}}
{{$note := dbGet .User.ID $key}}
{{if $note}}

{{$strippedKey := slice $key 6 (len $key)}}
Note: `{{$strippedKey}}` Created {{humanizeTimeSinceDays $note.CreatedAt}} ago:
{{$note.Value}}

{{else}}Couldn't find any note like that :({{end}}
```

#### List user's notes:

```go
{{$notes := dbGetPattern .User.ID "notes_%" 100 0}}
{{range $notes}}
{{- $strippedKey := slice .Key 6 (len .Key)}}
`{{$strippedKey}}` created {{humanizeTimeSinceDays .CreatedAt}} ago
{{- else}}
You don't have any notes :(
{{end}}
```

### Custom command cooldown example

A simple way to create cooldowns for your custom commands, by user and globally. Replace the 10 with the length of the cooldown.

#### Global cooldown
```go
{{if (dbGet 0 "cooldown")}}This command is still on cooldown for {{humanizeDurationSeconds ((dbGet 0 "cooldown").ExpiresAt.Sub currentTime)}}!{{else}}{{dbSetExpire 0 "cooldown" "command cooldown" 10}}
Command body {{/* Replace with code */}}{{end}}
```

#### Per user cooldown
```go
{{if (dbGet .User.ID "cooldown")}}This command is still on cooldown for {{humanizeDurationSeconds ((dbGet .User.ID "cooldown").ExpiresAt.Sub currentTime)}}!{{else}}{{dbSetExpire .User.ID "cooldown" "command cooldown" 10}}
Command body {{/* Replace with code */}}{{end}}
```

## User submitted custom commands

### GiveRole command for specific roles

> By **GryTrean\#8957**

This command will allow you to give a role to someone, making sure that the role given is in a list of allowed roles. We use the `{{giveRoleName <user> <role>}}` template which allows us to give a user a role by name. We also make sure that the command has the correct number of arguments and if not, we give a response with the correct usage of the command. To add a new exception to the roles that can be given, you simply add another role in line 2. You could also make the command take away roles from someone instead of giving them by simply using the `{{takeRoleName}}` template instead of `{{giveRoleName}}`.

Trigger type: `Command` Trigger: `giveRoleName`

{% code-tabs %}
{% code-tabs-item title="GiveRole Custom Command" %}
```go
{{if eq (len .Args) 3}}
    {{$allowedRoles := (cslice "Patron" "Quality Patron" "Paypal Donors")}}
    {{$role := (index .CmdArgs 1)}}

    {{if in $allowedRoles $role}}
        {{giveRoleName (userArg (index .CmdArgs 0)) $role}}
        Gave {{$role}} to {{index .CmdArgs 0}}! :white_check_mark:
    {{else}}
        You can't use this command to give that role to someone! :x:
    {{end}}
{{else}}
    Correct usage of the command: -giverole <target> "<rolename>"
{{end}}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Broadcast command

> By **GryTrean\#8957**   
> Updated by: **Timcampy\#5636**

This command lets the bot send a message to another channel. It uses embeds so you can see `sdict`\(dictionary but with only string keys\), `sendMessage`, and `cembed`in action.

Trigger type: `Command` Trigger: `bc`

```go
{{if eq (len .Args) 3}}
    {{$channel := (index .CmdArgs 0)}}
    {{$msg:= (joinStr " " (slice .CmdArgs 1))}}

    {{$footer1 := (sdict "text" (joinStr "" "This broadcast was sent by " (.User.Username) ""))}}
    {{$msgEmbed := cembed "title" "Broadcast!" "description" ($msg) "color" 16763904 "footer" ($footer1)}}

    {{sendMessage $channel $msgEmbed}}

    {{$desc := (joinStr "" "User " (.User.Username) " broadcasted a message in #" ($channel) "")}}
    {{$footer := (sdict "text" (joinStr "" "The broadcast was sent on " (exec "ctime") ""))}}

    {{$embed := cembed "title" "Broadcast sent!" "description" ($desc) "color" 4325120 "footer" ($footer) "fields" (cslice (sdict "name" "Broadcasted message:" "value" ($msg)))}}

    {{sendMessage nil $embed}}

{{else}}
    Correct usage of the command: -bc "<channel-name>" "<message>"
{{end}}
```



### Avatar command

> By:  **L-z\#7749**

This command does a good job at using a little bit of everything. Which include but is not limited to, `conditional statement`, `assigning values to variable`, `getting command arguments`, `using template code`, and `creating embeds`. If you are able to understand everything in this command, you are at a very good place in being able to make advanced custom commands. 

Trigger type: `Command` Trigger: `avatar`

```go
{{$ln := (len .Args)}}
{{$sizes := (cslice "16" "32" "64" "128" "256" "512" "1024" "2048" "4096")}}
{{$err1 := "Wrong image size input format! Possible values: 16, 32, 64, 128, 256, 512, 1024, 2048, 4096."}}
{{$err2 := "Unknown user :("}}
{{$color := 1478046}}
{{if gt $ln 1}}
  {{$1 := (index .Args 1)}}
  {{if ($user := userArg $1)}}
    {{if gt $ln 2}}
      {{$2 := (index .Args 2)}}
      {{if in $sizes $2}}
        {{$out := $user.AvatarURL (toString $2)}}
        {{$emb := cembed "color" $color "image" (sdict "url" $out)}}
        {{sendMessage nil $emb}}
      {{else}}
        {{$err1}}
      {{end}}
    {{else}}
      {{$out := $user.AvatarURL "512"}}
      {{$emb := cembed "color" $color "image" (sdict "url" $out)}}
      {{sendMessage nil $emb}}
    {{end}}
  {{else if gt $ln 2}}
    {{$2 := (index .Args 2)}}
    {{if ($user := userArg $2)}}
      {{if in $sizes $1}}
        {{$out := $user.AvatarURL (toString $1)}}
        {{$emb := cembed "color" $color "image" (sdict "url" $out)}}
        {{sendMessage nil $emb}}
      {{else}}
        {{$err1}}
      {{end}}
    {{else}}
      {{$err2}}
    {{end}}
  {{else if in $sizes $1}}
    {{$out := .User.AvatarURL (toString $1)}}
    {{$emb := cembed "color" $color "image" (sdict "url" $out)}}
    {{sendMessage nil $emb}}
  {{else}}
    {{$err1}}
  {{end}}
{{else}}
  {{$out := .User.AvatarURL "512"}}
  {{$emb := cembed "color" $color "image" (sdict "url" $out)}}
  {{sendMessage nil $emb}}
{{end}}
```

### Invite / Ad blocker

> By:  **Michdi\#1602**

This command is to be placed in the welcome message. It filters out people with discord.gg names. Make sure that the checkbox **Censor server invites in usernames?** and the ban command are enabled on your server.

Trigger type: `Join message in server channel`

```go
{{if .UsernameHasInvite}}
{{ $silent := (execAdmin "ban" .User.ID "ad blocked") }}
{{else}}
{{/* Replace this with your normal join message or leave it as it is */}}
{{end}}
```

### Suggestion command

> By: **Michdi\#1602**

This command is used to replace suggestion bots. You can adapt it to your needs.

Trigger type: `Command` Trigger: `suggest`

```go
{{ $channel := 476178740133494784 /* Replace the ID with your suggestions Channel ID */}}

{{if gt (len .Args) 1}}
Suggestion submitted.
{{ $embed := cembed
"description" (joinStr " " .CmdArgs)
"color" 9021952
"author" (sdict "name" (joinStr "" .User.Username "#" .User.Discriminator) "url" "" "icon_url" (.User.AvatarURL "512"))
"timestamp"  currentTime
}}
{{ $id := (sendMessageNoEscapeRetID $channel $embed) }}
{{ addMessageReactions $channel $id "upvote:524907425531428864" "downvote:524907425032175638" }}
{{else}}
Correct usage: `-suggest <suggestion>`
{{end}}
{{deleteResponse 5}}
{{deleteTrigger 5}}
```

### Big emote command

> By: **CHamburr\#2591**

This super advanced command make use of range and indexing for strings, and will enlarge custom emotes, whether still or animated. This will also work for emotes that are from the servers YAGPDB is not in, as it gets the emote file directly from Discord's database.

Trigger type: `Command` Trigger: `bigemote`

```go
{{ if eq (len .CmdArgs) 1 }}
{{ $d := index .CmdArgs 0 }}
{{ $ext := ".png" }}
{{ if eq (index $d 1) 97 }}
{{ $ext = ".gif" }}
{{ end }}
{{ $n := add (len $d) -19 }}
{{ $d = slice $d $n }}
{{ $r := "" }}
{{ $e := 1 }}
{{ range $k, $kk := seq 0 (len $d) }}
{{ if $e }}
{{ $v := index $d $k }}
{{ $a := "" }}
{{ if eq $v 48 }}
{{ $a = "0" }}
{{ else if eq $v 49 }}
{{ $a = "1" }}
{{ else if eq $v 50 }}
{{ $a = "2" }}
{{ else if eq $v 51}}
{{ $a = "3" }}
{{ else if eq $v 52 }}
{{ $a = "4" }}
{{ else if eq $v 53 }}
{{ $a = "5" }}
{{ else if eq $v 54 }}
{{ $a = "6" }}
{{ else if eq $v 55 }}
{{ $a = "7" }}
{{ else if eq $v 56 }}
{{ $a = "8" }}
{{ else if eq $v 57 }}
{{ $a = "9" }}
{{ else }}
{{ $e = 0 }}
{{ end }}
{{ $r = joinStr "" $r $a }}
{{ end }}
{{ end }}
{{ $color := randInt 111111 16777216 }}
{{ $embed := cembed "title" "Big Emote" "image" (sdict "url" (joinStr "" "https://cdn.discordapp.com/emojis/" $r $ext)) "color" $color }}
{{ sendMessage nil $embed }}
{{ else }}
Wrong use of command. Correct usage: `-bigemote <emote>`.
{{ end }}
```

{% hint style="info" %}
You want your custom command here? Post it in the [Support Server ](https://discord.gg/GcpyYh3)and we'll review it.
{% endhint %}



