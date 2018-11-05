# Custom Commands Examples

{% hint style="warning" %}
This isn't the actual page about custom commands. A brief overview about custom commands can be found [here](https://docs.yagpdb.xyz/custom-commands).
{% endhint %}

### Controlled randomizer example

YAGPDB has a built in random response system built into it custom command system but sometimes you want to control the chances of certain responses occurring. You can control this by creating a singular response and creating a Variable with randInt. Then use a if else if statement like such to print out your desired output. 

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

Trigger Type: Command Trigger: `updates`

```go
{{$a := (exec "role" "yagpdb")}}
Oh hi there, I just ran the role command. 
/*{{$a}} Remove the /* and the * / if you want the response to be displayed*/
```

The variable $a will store the output of running the role command and you can then just print out your own response.

### Range example

This command will let teach you about how the range command works. It works really well for iterating through all your inputs. 

This particular command will let the bot repeat everything that was being said behind the command \(careful with this one as there are ways to abuse it\). 

Trigger Type: Command Trigger: `repeat`

```go
{{range $k, $v := .CmdArgs}}{{$v}}{{end}}
```

$k is the iteration number you are on starting at 0 and $v is the current word in your input that you are on. The if statement is in there so the command doesn't include the first word in the sentence or "-repeat" in the output. If your trigger is multiple words you may need to adjust accordingly 

### Dictionary example

A dictionary does not currently have a lot of piratical use as of right now as YAGPDB has a built in randomizer in its custom command now in case you ever find yourself needing to use it, here's how to set it up.

Trigger Type: Command Trigger: `dict`

```go
{{$options := (dict "0" "test" "1" "test1" "2" "test2")}}
{{$d := randInt (len $options)}}
{{index $options (toString $d)}}
```

## User submitted custom commands

### GiveRole command for specific roles

> By **GryTrean**\#8957

This command will allow you to give a role to someone, making sure that the role is added to a list with allowed roles. We use the {{giveRoleName &lt;user&gt; &lt;role&gt;}} template which allows us to give an user a role by name. We also make sure that the command has a correct number of arguments and if not, we give a response with the correct usage of the command. To add a new exception to the roles that can be given, you simply add another role in line 2. You could also make the command take away roles from someone instead of giving them by simply using the {{takeRoleName}} template instead of {{giveRoleName}}.

Trigger Type: Command Trigger: `giveRoleName` 

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

> By **GryTrean**\#8957   
> Updated by: Timcampy\#5636

This command gives you the ability to send a message in another channel, it also uses embeds for this so you can see `sdict`\(dictionary but with only string keys\), `sendMessage`, and `cembed`in action.

Trigger Type: Command Trigger: `bc`

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

This command does a good job at using a little bit of everything. Which include but is not limited to, **`conditional statement`, `assigning values to variable`, `getting command arguments`, `using template code`, `creating embeds`**. If you are able to understand everything in this command, you are at a very good place in being able to make advance custom commands. 

Trigger Type: Command Trigger: `avatar`

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

Trigger Type: Join message in server channel

```go
{{if .UsernameHasInvite}}
{{ $silent := (execAdmin "ban" .User.ID "ad blocked") }}
{{else}}
{{/* Replace this with your normal join message or leave it as it is */}}
{{end}}
```

{% hint style="info" %}
You want your custom command here? Post it in the [Support Server ](https://discord.gg/GcpyYh3)and we'll review it.
{% endhint %}

