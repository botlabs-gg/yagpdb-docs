---
description: You can find all commands of the bot here.
---

# Commands

## Prefix

The prefix is by default `-` The first thing you see when you open the command page is the prefix, you can replace this with your own unique prefix if you would like. Be sure to hit the save button afterward.

## Command Override

![To create a command override look for the box that says New command override](../.gitbook/assets/commandoverride.PNG)

**Apply to the following commands:** Once you are in the box, you can select which command you want to override to apply to.  __

**Specific commands enabled in this command override:** You can then toggle whether or not to enable or disable the command with this override. \(Enable this if you have the command disabled in the global settings\)

**Auto delete trigger/response:** Toggle to enable/disable the auto delete for the trigger and response respectively and assign it a time to wait until deleting \(1-60 Seconds\).

**Require one of these roles:** Choose to require someone to have a role in order to use the commands.

**Ignore users with one of these roles:** Choose to ignore someone who has a role and prevent them from using the command.

## Channel Override

![Look to the top right on your screen for a box that says New channel override.](../.gitbook/assets/channeloverride.PNG)

**Channels this override affects:** Select which channels you want the override to apply to. 

**Include current and future channels from the following categories:** By picking a category, you apply this override to all the channels in the category which includes future channels .

**Require one of these roles:** Choose to require someone to have a role in order to use the commands.

**Ignore users with one of these roles:** Choose to ignore someone who has a role and prevent them from using it.

**All commands enabled**: Enable all the commands for this override, you can create command override for the channel overrides below if you wish to customize further.

**Auto delete trigger/response:** Toggle to enable/disable the auto delete for the trigger and response respectively and assign it a time to wait until deleting \(1-60 Seconds\).

**New command override:** Create a command override that will apply to all the channels in the channel override. For help on creating command overrides, refer to [Command override.](commands.md#command-override) 

## Command List

You may get a list of every command by typing `-help` on your server.  
You may also get more specific help by typing `-help (command)` .

### General

| Command | Aliases | Optional Args | Description |
| :--- | :--- | :--- | :--- |
| help | h, how, command\(s\) | \(command\) | Shows help for all or one specific command. |
| info | N/A | N/A | Response with bot information. |
| invite | inv, i | N/A | Response with the bot website link for invitation. |

###  Tools & Utilities

<table>
  <thead>
    <tr>
      <th style="text-align:left">Command</th>
      <th style="text-align:left">Aliases</th>
      <th style="text-align:left">Required Args</th>
      <th style="text-align:left">Optional Args</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">prefix</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(serverID)</td>
      <td style="text-align:left">Shows the command prefix on current server or specified server.</td>
    </tr>
    <tr>
      <td style="text-align:left">calc</td>
      <td style="text-align:left">c, calculate</td>
      <td style="text-align:left">(what to calculate)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Calculator. Example: <code>2+2</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">ping</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Response with pong and pingtime.</td>
    </tr>
    <tr>
      <td style="text-align:left">currenttime</td>
      <td style="text-align:left">ctime, gettime</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(timezone) (delta time in hours)</td>
      <td style="text-align:left">Shows UTC time, or the timezone you chose. List of <a href="https://pastebin.com/ZqSPUhc7">timezones</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">mentionrole</td>
      <td style="text-align:left">mrole</td>
      <td style="text-align:left">rolename</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Sets a role to mentionable, mentions the role, then sets it back to not
        mentionable after 30 seconds.</td>
    </tr>
    <tr>
      <td style="text-align:left">listroles</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">List roles and their IDs, and some other stuff on the server.</td>
    </tr>
    <tr>
      <td style="text-align:left">poll</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(description) (option 1) (option 2)</td>
      <td style="text-align:left">(option 3) etc</td>
      <td style="text-align:left">Creates a reaction poll.</td>
    </tr>
    <tr>
      <td style="text-align:left">undelete</td>
      <td style="text-align:left">ud</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">-a</td>
      <td style="text-align:left">Views your recent deleted messages, or all users deleted messages (with
        "-a" and manage messages perm) in this channel.</td>
    </tr>
    <tr>
      <td style="text-align:left">viewperms</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(mention/ID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Shows you requested user's permissions in this channel.</td>
    </tr>
    <tr>
      <td style="text-align:left">stats</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Shows server stats (only if public stats are enabled).</td>
    </tr>
    <tr>
      <td style="text-align:left">customcommands</td>
      <td style="text-align:left">cc</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">
        <p>(commandID)</p>
        <p>(trigger string)</p>
      </td>
      <td style="text-align:left">Shows a custom command specified by id or trigger or lists them all.
        <a
        href="custom-commands.md">More info</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">logs</td>
      <td style="text-align:left">log</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(count)</td>
      <td style="text-align:left">Creates a log of the channels messages (max. 100).</td>
    </tr>
    <tr>
      <td style="text-align:left">whois</td>
      <td style="text-align:left">whoami</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(username)</td>
      <td style="text-align:left">Shows information about given member.</td>
    </tr>
    <tr>
      <td style="text-align:left">nicknames</td>
      <td style="text-align:left">nn</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(username)</td>
      <td style="text-align:left">Shows past nicknames of given member.</td>
    </tr>
    <tr>
      <td style="text-align:left">usernames</td>
      <td style="text-align:left">unames, un</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(username)</td>
      <td style="text-align:left">Shows past usernames of given member.</td>
    </tr>
    <tr>
      <td style="text-align:left">remindme</td>
      <td style="text-align:left">remind</td>
      <td style="text-align:left">(time) (message)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Schedules a reminder. Example: <code>remindme 1h30min are you still alive?</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">reminders</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">List of your active reminders with an ID.</td>
    </tr>
    <tr>
      <td style="text-align:left">creminders</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Lists reminders only in the current channel with an ID. Only members with <code>manage server</code> permissions
        can use this command.</td>
    </tr>
    <tr>
      <td style="text-align:left">delreminder</td>
      <td style="text-align:left">rmreminder</td>
      <td style="text-align:left">(ID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Deletes the reminder with the given ID.</td>
    </tr>
    <tr>
      <td style="text-align:left">role</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(rolename)</td>
      <td style="text-align:left">Give yourself a role or list all available roles. Needs to be set up first
        on the control panel.</td>
    </tr>
  </tbody>
</table>###  Moderation

| Command | Aliases | Required Args | Optional Args | Description |
| :--- | :--- | :--- | :--- | :--- |
| ban | banid | \(username\) or \(userID\) | \(reason\) | Bans given member by name mention or ID. |
| kick | N/A | \(username\) or \(userID\) | \(reason\) | Kicks given member by name mention or ID. |
| mute | N/A | \(username\) | \(minutes\) \(reason\) | Mutes given member. |
| unmute | N/A | \(username\) | \(reason\) | Unmutes given member. |
| report | N/A | \(username\)  | \(reason\) | Reports given member. |
| clean | clear, cl | \(count\) | \(username\) | Cleans the chat. |
| reason | N/A | \(ID\) \(reason\) | N/A | Add/Edit modlog reason from given ID. |
| warn | N/A | \(username\) \(reason\) | N/A | Warns given member. Warnings are saved. |
| warnings | N/A | \(username\) | N/A | Lists warnings of given member with an ID. |
| editwarning | N/A | \(ID\) \(Reason\) | N/A | Edit given warning. |
| delwarning | dw | \(ID\) | N/A | Deletes the warning with the given ID. |
| clearwarnings | clw | \(username\) or \(userID\) | N/A | Clears all warnings from given member. |
| automod toggle | automod t | \(Ruleset\) | N/A |  Toggles a ruleset on/off. |

###  Fun

| Command | Aliases | Required Args | Optional Args | Description |
| :--- | :--- | :--- | :--- | :--- |
| define | df | \(topic\) | N/A | Looks for an Urban Dictionary definition. |
| reverse | r, rev | \(text\) | N/A | Reverse the text given. **NB! Command has been removed from the bot.** |
| weather | w | \(location\) | N/A | Show the weather for the given location.  |
| topic | N/A | N/A | N/A | Generates a chat topic. |
| catfact | cf, cat, catfacts | N/A | N/A | Catfacts. What else?! |
| advice | N/A | N/A | \(for?\) | Get some advice. **NB!** Currently not working. |
| throw | N/A | N/A | \(username\) | Throws random stuff at nearby people or at the given member. |
| roll | N/A | N/A | \(number of sides\) | Roll a dice. Specify nothing for 6 siddes, or specify a number for max. sides. |
| customembed | ce | \(json\) | N/A | Creates an embed from what you give it in json form: [Embed Object](https://discordapp.com/developers/docs/resources/channel#embed-object). |
| wouldyourather | wyr | N/A | N/A | Presents you with 2 choices. Somewhat NSFW text wise. |
| topservers | N/A | N/A | \(skip: number - entries to skip | Responds with the top 15 servers the bot is on. |
| takerep | -, tr, trep | \(username\) | \(count\) | Takes away given number of rep from given member. Default number is 1. |
| giverep | +, gr, grep | \(username\) | \(count\) | Give given number of rep to given member. Default number is 1. |
| setrep | setrepID | \(mention/ID\) \(number\) | N/A | Sets someones rep, by mention or ID. This is a rep admin command \(manage server perms. or rep admin role\) and bypasses cooldowns and other restrictions. |
| delrep | N/A | \(mention/ID\) | N/A | Deletes someone from the reputation list completely. This is a rep admin command and bypasses cooldowns and other restrictions. This action cannot be undone. |
| replog | N/A | \(mention/ID\) | \(page number\) | Shows specified user's rep log. Longer logs are divided into pages. |
| rep | N/A | N/A | \(username\) | Shows your or the given member's current rep and rank. |
| toprep | N/A | N/A | \(offset\) | Shows top 15 rep members on the server. |
| sentiment | sent | N/A | \(text\) | Does sentiment analysis on the given text or your last 5 messages longer than 3 words. |
| 8ball | N/A | \(question\) | N/A | Wisdom. |
| soundboard | sb | N/A | \(soundname\) | Play or list soundboard sounds. |

####  Cards Against Humanity

Everything here starts with cah such as `-cah create`

| Command | Aliases | Required Args | Optional Args | Description |
| :--- | :--- | :--- | :--- | :--- |
| create | c | N/A | \(pack name\) |  Creates a cards against humanity game in this channel. |
| end | N/A | N/A | N/A |  Ends a cards against humanity game that's ongoing in this channel. |
| kick | N/A | \(user\) | N/A |  Kicks a player from the ongoing cards against humanity game in this channel. |
| packs | N/A | N/A | N/A |  Lists available packs. |

### Rolemenu

Everything here starts with rolemenu such as `-rolemenu create`

<table>
  <thead>
    <tr>
      <th style="text-align:left">Comment</th>
      <th style="text-align:left">Aliases</th>
      <th style="text-align:left">Required Args</th>
      <th style="text-align:left">Optional Args</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">create</td>
      <td style="text-align:left">c</td>
      <td style="text-align:left">(rolegroup's name)</td>
      <td style="text-align:left">
        <p>(m:messageID)(nodm)(rr)</p>
        <p>(skip:number)</p>
      </td>
      <td style="text-align:left">
        <p>Sets up a role menu, specify a message with <b>-m</b> to use an existing
          message instead of having the bot make one.
          <br />
          <br /><b>-nodm</b>, <b>-rr</b> are switches - first one enables/disables DM response
          and second one alters reaction removed state, by default reaction removed
          is also role removed.</p>
        <p></p>
        <p><b>-skip</b> Skips certain number of roles in that rolegroup, if not needed
          in that rolemenu.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">remove</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(messageID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Removes the rolemenu from a message, the message wont be deleted but the
        bot will now not do anything with reactions on that message.</td>
    </tr>
    <tr>
      <td style="text-align:left">update</td>
      <td style="text-align:left">u</td>
      <td style="text-align:left">(messageID)</td>
      <td style="text-align:left">(nodm)(rr)</td>
      <td style="text-align:left">Updates a rolemenu, toggling the provided flags and adding missing options,
        aswell as updating the order.</td>
    </tr>
    <tr>
      <td style="text-align:left">resetreactions</td>
      <td style="text-align:left">reset</td>
      <td style="text-align:left">(messageID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Removes all reactions on this menu and re-adds them, can be used to fix
        the order.</td>
    </tr>
    <tr>
      <td style="text-align:left">editoption</td>
      <td style="text-align:left">edit</td>
      <td style="text-align:left">(messageID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Allows you to reassign the emoji of an option, tip: use ResetReactions
        afterwards.</td>
    </tr>
  </tbody>
</table>### Debug

| Command | Aliases | Optional Args | Description |
| :--- | :--- | :--- | :--- |
| yagstatus | status | N/A | Shows YAGPDB's status. |
| currentshard | cshard | N/A | Shows the current shard this server is on. |
| memberfetcher | memfetch | N/A | Shows the current status of the member fetcher. |
| roledbg | N/A | N/A | Debug autorole assignment. |
| stateinfo | N/A | N/A | Responds with state debug info. |
| topcommands | N/A | \(hours:number\) |  Shows command usage stats, defaults to last hour. |
| topevents | N/A | \(shard:number\) | Shows gateway event processing stats for all or one shard. |

### Administrative \(only for self-hosting\)

| Command | Aliases | Required Args | Optional Args | Description |
| :--- | :--- | :--- | :--- | :--- |
| allocstat | N/A | N/A | N/A | Memory statistics. |
| leaveserver | N/A | \(ID\) | N/A | Makes the bot leave a server by ID. |
| banserver | N/A | \(ID\) | N/A | Makes the bot leave and ban a server by ID. |
| unbanserver | N/A | \(ID\) | N/A | Makes the bot unban a server by ID. |
| findserver | N/A | \(name\)\(user\)  | N/A | Looks for a server by server name or the servers a user was on. |
| createinvite | N/A | \(ID\) | N/A | Maintenance command, creates a invite for the specified server. |

