# Command Settings

## Prefix

The prefix is by default `-` The first thing you see when you open the command page is the prefix, you can replace this with your own unique prefix if you would like. Be sure to hit the save button afterwards. Only commands have a designated prefix.

{% hint style="warning" %}
**Flags and switches** are _not_ affected by prefixes. For example, if you were using the `rolemenu create` command with the prefix `+`, it would be`+rolemenu create (group name) -m (message id)`. Note that we used the `+` prefix but `-m` stayed as `-m`, not `+m`.
{% endhint %}

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

Full indexed list of all commands is also here  &gt; [All Commands](all-commands.md).

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
      <td style="text-align:left">(-channel: channelName/ID)</td>
      <td style="text-align:left">Sets a role to mentionable, mentions the role, then sets it back to not
        mentionable after 10 seconds. <code>-channel</code> flag makes it possible
        to send a mention to some other channel defined by ID or name.</td>
    </tr>
    <tr>
      <td style="text-align:left">listroles</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">-nomanaged</td>
      <td style="text-align:left">List roles and their IDs, and some other stuff on the server. <code>-nomanaged </code>is
        a switch that does not display managed/bot roles in <code>listroles</code> return.</td>
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
        &quot;-a&quot; and manage messages perm) in this channel.</td>
    </tr>
    <tr>
      <td style="text-align:left">viewperms</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(mention/userID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Shows you requested user&apos;s permissions in this channel.</td>
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
      <td style="text-align:left">(mention/userID)</td>
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
      <td style="text-align:left">resetpastnames</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Resets your past usernames &amp; nicknames.</td>
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
      <td style="text-align:left">(reminderID)</td>
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
    <tr>
      <td style="text-align:left">settimezone</td>
      <td style="text-align:left">setz, tzset</td>
      <td style="text-align:left">(timezone)</td>
      <td style="text-align:left">-d, -u</td>
      <td style="text-align:left">Sets your timezone, used for various purposes such as auto conversion. <code>timezone</code> is
        your country, use this &gt; <a href="http://kevalbhatt.github.io/timezone-picker/">Timezone Picker</a> ,
        enter the <code>Area/City</code> result. Flag -u shows users currently set
        time zone or server&apos;s local and -d deletes it if set.</td>
    </tr>
    <tr>
      <td style="text-align:left">toggletimeconversion</td>
      <td style="text-align:left">toggletconv</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(flags)</td>
      <td style="text-align:left">Toggles automatic time conversion for people with registered timezones
        (setz) in current channel, its on by default. By using <code>flags</code> argument,
        currently <code>all</code> or <code>*</code> will toggle that time conversion
        in all channels, including newly created ones.</td>
    </tr>
  </tbody>
</table>

###  Moderation

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
      <td style="text-align:left">ban</td>
      <td style="text-align:left">banid</td>
      <td style="text-align:left">(mention/userID)</td>
      <td style="text-align:left">
        <p>(reason)</p>
        <p>(-d:duration)</p>
        <p>(-ddays:number)</p>
      </td>
      <td style="text-align:left">Bans given member by name mention or ID. Duration sets how long the ban
        lasts, default is in minutes - this can be altered <b><code>-d 2w</code></b> is
        for two weeks. <code>-ddays</code> switch determines how many days of messages
        gets deleted - max 7 days.</td>
    </tr>
    <tr>
      <td style="text-align:left">kick</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(mention/userID)</td>
      <td style="text-align:left">(reason)</td>
      <td style="text-align:left">Kicks given member by name mention or ID.</td>
    </tr>
    <tr>
      <td style="text-align:left">mute</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(mention/userID)</td>
      <td style="text-align:left">(minutes) (reason)</td>
      <td style="text-align:left">Mutes given member.</td>
    </tr>
    <tr>
      <td style="text-align:left">unmute</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(mention/userID)</td>
      <td style="text-align:left">(reason)</td>
      <td style="text-align:left">Unmutes given member.</td>
    </tr>
    <tr>
      <td style="text-align:left">report</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(mention/userID)</td>
      <td style="text-align:left">(reason)</td>
      <td style="text-align:left">Reports given member.</td>
    </tr>
    <tr>
      <td style="text-align:left">clean</td>
      <td style="text-align:left">clear, cl</td>
      <td style="text-align:left">(count)</td>
      <td style="text-align:left">
        <p>(mention/userID)</p>
        <p>(-ma: max age)</p>
        <p>(-minage: min age)</p>
        <p>(-r:regex)</p>
        <p>(-i:regex case insensitive)</p>
        <p>(-nopin: Ignore pinned messages)</p>
        <p>(-to: whole number, stops deleting at that message ID)</p>
      </td>
      <td style="text-align:left">
        <p>Cleans the chat. More in depth <a href="all-commands.md#clean">here</a>.</p>
        <p>Also disclaimer by Discord <a href="https://discordapp.com/developers/docs/resources/channel#bulk-delete-messages">here</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">reason</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(messageID) (reason)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Add/Edit modlog message&apos;s reason to given ID.</td>
    </tr>
    <tr>
      <td style="text-align:left">warn</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(mention/userID) (reason)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Warns given member. Warnings are saved.</td>
    </tr>
    <tr>
      <td style="text-align:left">warnings</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(mention/userID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Lists warnings of given member with an ID.</td>
    </tr>
    <tr>
      <td style="text-align:left">editwarning</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(warningID) (reason)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Edit given warning.</td>
    </tr>
    <tr>
      <td style="text-align:left">delwarning</td>
      <td style="text-align:left">dw</td>
      <td style="text-align:left">(warningID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Deletes the warning with the given ID.</td>
    </tr>
    <tr>
      <td style="text-align:left">clearwarnings</td>
      <td style="text-align:left">clw</td>
      <td style="text-align:left">(mention/userID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Clears all warnings from given member.</td>
    </tr>
    <tr>
      <td style="text-align:left">topwarnings</td>
      <td style="text-align:left">topwarns</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">-id:switch</td>
      <td style="text-align:left">Shows ranked list of warnings on the server. -id switch switches their
        username to IDs.</td>
    </tr>
    <tr>
      <td style="text-align:left">giverole</td>
      <td style="text-align:left">grole, arole, addrole</td>
      <td style="text-align:left">(mention/userID) (rolename)</td>
      <td style="text-align:left">(-d:duration)</td>
      <td style="text-align:left">Gives a role to the specified member, with optional expiry, for example <code>-d 10h5m10s.</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">removerole</td>
      <td style="text-align:left">rrole, takerole, trole</td>
      <td style="text-align:left">(mention/userID) (rolename)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Removes the specified role from the target.</td>
    </tr>
  </tbody>
</table>

#### Automod 

Everything here starts with `automod` or `amod` such as `-automod toggle`

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
      <td style="text-align:left">Rulesets</td>
      <td style="text-align:left">r, list, l</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Lists all rulesets and their status.</td>
    </tr>
    <tr>
      <td style="text-align:left">Toggle</td>
      <td style="text-align:left">t</td>
      <td style="text-align:left">(ruleset)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Toggles a ruleset on/off.</td>
    </tr>
    <tr>
      <td style="text-align:left">Logs</td>
      <td style="text-align:left">log</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(count: number)</td>
      <td style="text-align:left">Shows triggered automod rules (optionally can show number of logged messages).</td>
    </tr>
    <tr>
      <td style="text-align:left">ListViolations</td>
      <td style="text-align:left">
        <p>Violations/</p>
        <p>ViolationLogs/
          <br />VLogs/VLog</p>
      </td>
      <td style="text-align:left">(Mention/ID)</td>
      <td style="text-align:left">
        <p>(page :numer)</p>
        <p>(-old)</p>
      </td>
      <td style="text-align:left">Lists Violations of specified user -old flag posts oldest violations in
        first page (from oldest to newest).</td>
    </tr>
    <tr>
      <td style="text-align:left">ListViolationsCount</td>
      <td style="text-align:left">
        <p>ViolationsCount/</p>
        <p>VCount</p>
      </td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">
        <p>(mention/ID)</p>
        <p>(-ma: duration)</p>
        <p>(-skip: number)</p>
      </td>
      <td style="text-align:left">Lists Violations summary in entire server or of specified user optionally
        filtered by max violation age. Specify number of violations to skip while
        fetching using -skip flag ; max entries fetched 500</td>
    </tr>
    <tr>
      <td style="text-align:left">DeleteViolation</td>
      <td style="text-align:left">
        <p>DelViolation/</p>
        <p>DelV/DV</p>
      </td>
      <td style="text-align:left">ID</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Deletes a Violation with the specified ID. ID is the first number of each
        Violation in the ListViolations command.</td>
    </tr>
    <tr>
      <td style="text-align:left">ClearViolations</td>
      <td style="text-align:left">
        <p>ClearV/</p>
        <p>ClrViolations/ClrV</p>
      </td>
      <td style="text-align:left">(Mention/ID)</td>
      <td style="text-align:left">
        <p>(Violation Name:text)</p>
        <p>(-ma, -mina: duration)
          <br />(-num, -skip: number)
          <br />(-old: switch)</p>
        <p></p>
      </td>
      <td style="text-align:left">
        <p>Clears Violations of specified user optionally filtered by Name, Min/Max
          age and other conditions. By default, more recent violations are preferentially
          cleared.</p>
        <p>-ma and -mina are max and min violation age; -num is the max number of
          violations to be cleared; -old is a switch for clearing older violations;
          -skip the amount to be skipped.</p>
      </td>
    </tr>
  </tbody>
</table>

### Fun

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
      <td style="text-align:left">define</td>
      <td style="text-align:left">df</td>
      <td style="text-align:left">(topic)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Looks for an Urban Dictionary definition.</td>
    </tr>
    <tr>
      <td style="text-align:left">weather</td>
      <td style="text-align:left">w</td>
      <td style="text-align:left">(location)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Show the weather for the given location.</td>
    </tr>
    <tr>
      <td style="text-align:left">topic</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Generates a chat topic.</td>
    </tr>
    <tr>
      <td style="text-align:left">catfact</td>
      <td style="text-align:left">cf, cat, catfacts</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Catfacts. What else?!</td>
    </tr>
    <tr>
      <td style="text-align:left">dogfact</td>
      <td style="text-align:left">dog, dogfacts</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Dogfacts. Yeah. Competitor to catfacts.</td>
    </tr>
    <tr>
      <td style="text-align:left">advice</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(for?)</td>
      <td style="text-align:left">Get some advice.</td>
    </tr>
    <tr>
      <td style="text-align:left">throw</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(username)</td>
      <td style="text-align:left">Throws random stuff at nearby people or at the given member.</td>
    </tr>
    <tr>
      <td style="text-align:left">roll</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(number of sides)</td>
      <td style="text-align:left">Roll a dice. Specify nothing for 6 siddes, or specify a number for max.
        sides.</td>
    </tr>
    <tr>
      <td style="text-align:left">customembed</td>
      <td style="text-align:left">ce</td>
      <td style="text-align:left">(json)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Creates an embed from what you give it in json form: <a href="https://discordapp.com/developers/docs/resources/channel#embed-object">Embed Object</a>.
        Requires Manage Messages permission.</td>
    </tr>
    <tr>
      <td style="text-align:left">simpleembed</td>
      <td style="text-align:left">se</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(switches)</td>
      <td style="text-align:left">A simpler version of CustomEmbed, controlled using switches. Requires
        Manage Messages permission. <a href="all-commands.md#simpleembed">More info</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">wouldyourather</td>
      <td style="text-align:left">wyr</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Presents you with 2 choices. Somewhat NSFW text wise.</td>
    </tr>
    <tr>
      <td style="text-align:left">xkcd</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">number or -l:switch for latest</td>
      <td style="text-align:left">Gives random xkcd comic if not stated by number or -l flag meaning latest.</td>
    </tr>
    <tr>
      <td style="text-align:left">topservers</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">
        <p>(skip: number - entries to skip</p>
        <p>-id: serverID)</p>
      </td>
      <td style="text-align:left">Responds with the top servers list YAGPDB is on.</td>
    </tr>
    <tr>
      <td style="text-align:left">takerep</td>
      <td style="text-align:left">-, tr, trep</td>
      <td style="text-align:left">(username)</td>
      <td style="text-align:left">(count)</td>
      <td style="text-align:left">Takes away given number of rep from given member. Default number is 1.</td>
    </tr>
    <tr>
      <td style="text-align:left">giverep</td>
      <td style="text-align:left">+, gr, grep</td>
      <td style="text-align:left">(username)</td>
      <td style="text-align:left">(count)</td>
      <td style="text-align:left">Give given number of rep to given member. Default number is 1.</td>
    </tr>
    <tr>
      <td style="text-align:left">setrep</td>
      <td style="text-align:left">setrepID</td>
      <td style="text-align:left">(mention/userID) (number)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Sets someones rep, by mention or ID. This is a rep admin command (manage
        server perms. or rep admin role) and bypasses cooldowns and other restrictions.</td>
    </tr>
    <tr>
      <td style="text-align:left">delrep</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(mention/userID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Deletes someone from the reputation list completely. This is a rep admin
        command and bypasses cooldowns and other restrictions. This action cannot
        be undone.</td>
    </tr>
    <tr>
      <td style="text-align:left">replog</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(mention/userID)</td>
      <td style="text-align:left">(page number)</td>
      <td style="text-align:left">Shows specified user&apos;s rep log. Longer logs are divided into pages.</td>
    </tr>
    <tr>
      <td style="text-align:left">rep</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(username)</td>
      <td style="text-align:left">Shows your or the given member&apos;s current rep and rank.</td>
    </tr>
    <tr>
      <td style="text-align:left">toprep</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(offset)</td>
      <td style="text-align:left">Shows top 15 rep members on the server.</td>
    </tr>
    <tr>
      <td style="text-align:left">sentiment</td>
      <td style="text-align:left">sent</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(text)</td>
      <td style="text-align:left">Does sentiment analysis on the given text or your last 5 messages longer
        than 3 words.</td>
    </tr>
    <tr>
      <td style="text-align:left">8ball</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(question)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Wisdom.</td>
    </tr>
    <tr>
      <td style="text-align:left">soundboard</td>
      <td style="text-align:left">sb</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(soundname)</td>
      <td style="text-align:left">Play or list soundboard sounds.</td>
    </tr>
    <tr>
      <td style="text-align:left">soundboardreset</td>
      <td style="text-align:left">sbclose/ sbreset</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Resets Soundboard Player</td>
    </tr>
  </tbody>
</table>

####  Cards Against Humanity

Everything here starts with `cah` such as `-cah create`

| Command | Aliases | Required Args | Optional Args | Description |
| :--- | :--- | :--- | :--- | :--- |
| create | c | N/A | \(pack name\) |  Creates a cards against humanity game in this channel. |
| end | N/A | N/A | N/A |  Ends a cards against humanity game that's ongoing in this channel. |
| kick | N/A | \(user\) | N/A |  Kicks a player from the ongoing cards against humanity game in this channel. |
| packs | N/A | N/A | N/A |  Lists available packs. |

### Rolemenu

{% hint style="warning" %}
Rolemenu commands require user to have at least manage server permission.
{% endhint %}

Everything here starts with `rolemenu`or `rmenu` such as `-rolemenu create` 

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
      <td style="text-align:left">create</td>
      <td style="text-align:left">c</td>
      <td style="text-align:left">(rolegroup&apos;s name)</td>
      <td style="text-align:left">
        <p>(-m: messageID) (-nodm)
          <br />(-rr)</p>
        <p>(-skip: number)</p>
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
      <td style="text-align:left">(-nodm)
        <br />(-rr)</td>
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
    <tr>
      <td style="text-align:left">complete</td>
      <td style="text-align:left">finish</td>
      <td style="text-align:left">(messageID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Marks the menu as done.</td>
    </tr>
  </tbody>
</table>

### Tickets

Everything here starts with `ticket(s)` such as `-tickets create`

| Command | Aliases | Required Args | Optional Args | Description |
| :--- | :--- | :--- | :--- | :--- |
| open | create, new, make | \(subject's name\) | N/A | Opens a new ticket.  |
| addUser | N/A | \(user\) | N/A | Adds a user to the ticket in this channel. |
| removeUser | N/A | \(user\) | N/A | Removes a user from the ticket. |
| rename | N/A | \(new name\) | N/A | Renames the ticket. |
| close | end, delete | N/A | \(reason\) | Closes the ticket. |
| adminsonly | adminonly, ao | N/A | N/A | Toggle admins only mode for this ticket. |

### Events

Everything here starts with `event(s)` such as `-events create`

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
      <td style="text-align:left">create</td>
      <td style="text-align:left">new, make</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Creates a new event, you will be led through an interactive setup.</td>
    </tr>
    <tr>
      <td style="text-align:left">edit</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">(eventID)</td>
      <td style="text-align:left">(-title)
        <br />(-time)
        <br />(-max: number)</td>
      <td style="text-align:left">
        <p>Edits an event. <b>List </b>will give you <code>eventID</code>.</p>
        <p><b>-title</b> Changes event&apos;s title.</p>
        <p><b>-time</b> Changes event&apos;s start time.</p>
        <p><b>-max</b> Changes max number of participants.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">list</td>
      <td style="text-align:left">ls</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Lists all events in current server.</td>
    </tr>
    <tr>
      <td style="text-align:left">delete</td>
      <td style="text-align:left">rm, del</td>
      <td style="text-align:left">(eventID)</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Deletes specified event. <b>List</b> will give you <code>eventID</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left">stopsetup</td>
      <td style="text-align:left">cancelsetup</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">Force cancels the setup session in current channel.</td>
    </tr>
  </tbody>
</table>

### Debug & Maintenance

| Command | Aliases | Optional Args | Description |
| :--- | :--- | :--- | :--- |
| topgames | N/A | \(-all\) | Shows the top games on this server. |
| stateinfo | N/A | N/A | Responds with state debug info. |
| topcommands | N/A | \(hours:number\) |  Shows command usage stats, defaults to last hour. |
| topevents | N/A | \(shard:number\) | Shows gateway event processing stats for all or one shard. |
| currentshard | cshard | N/A | Shows the current shard this server is on. |
| memberfetcher | memfetch | N/A | Shows the current status of the member fetcher. |
| yagstatus | status | N/A | Shows YAGPDB's status. |
| roledbg | N/A | N/A | Debug autorole assignment. |

### Administrative \(only for self-hosting\)

| Command | Aliases | Required Args | Optional Args | Description |
| :--- | :--- | :--- | :--- | :--- |
| allocstat | N/A | N/A | N/A | Memory statistics. |
| leaveserver | N/A | \(ID\) | N/A | Makes the bot leave a server by ID. |
| banserver | N/A | \(ID\) | N/A | Makes the bot leave and ban a server by ID. |
| unbanserver | N/A | \(ID\) | N/A | Makes the bot unban a server by ID. |
| findserver | N/A | \(name\)\(user\)  | N/A | Looks for a server by server name or the servers a user was on. |
| createinvite | N/A | \(ID\) | N/A | Maintenance command, creates a invite for the specified server. |
| generatepremiumcode | gpc | duration, numCodes, message | N/A | Generates premium codes |

