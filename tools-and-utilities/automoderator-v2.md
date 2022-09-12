# Automoderator V2

{% hint style="info" %}
#### Tips

Generally speaking most people want to have "ignore bots" as a ruleset condition, that way bots won't trigger any rules.

A simple way to have it is to keep all the basic stuff (invites, spam mentions, safebrowsing etc) in a single rule, then have a single violation counter and a rule for each tier of punishment (warn, kick, mute, ban)
{% endhint %}

## Introduction

![](../.gitbook/assets/AutoMod2.0\_2.PNG)

Automod V2 is a completely new auto-moderator system made from the ground up. When starting out you will need to create a new ruleset.

#### Rulesets

Rulesets are how you will group your auto moderation rules, you will need one to start out. A ruleset can be toggled on or off in the control panel with the `-automod toggle <ruleset name>` command.

#### List

List is where you will enter a list of words or websites for the auto-moderation system to use such as a list of banned websites/banned words/banned names etc.

#### Logs

Every time a rule is triggered, a log will be posted with the Date, User, Rule, and Trigger that caused it. This is helpful to find out what exactly happened.

## Ruleset Settings

In each rule sets you have several options

* **Name:** You can edit the name of your rule
* **Enable rule set:** You can toggle the rule set on and off&#x20;
* **Ruleset scoped condition:** Assigned conditions that will apply to every rule\` in the rule set.&#x20;
* **Create a new rule:** Create a new rule in the ruleset

## Rule Setting&#x20;

![Each rule will have a combination of Trigger, Condition, and Effects. ](../.gitbook/assets/AutoMod2.0.PNG)

**Triggers:** A variety of different parameters that can configured to trigger the rule. Multiple parameters can be set but only one needs to activate to trigger the rule. \
**Conditions**: Restrictions or parameters set to limit who can trigger the rule. Multiple conditions can be set and all must be valid in order to allow the trigger.\
**Effects**: The effect that the rule will cause. Multiple effects can be added and all of them will be activated whenever the trigger is activated

## Violations&#x20;

When you create a violation, you will need to assign it a name. Each violation name will act like a key which has its own separate count.&#x20;

**Example:** If you have two violation names`links` and `badName`, `+violation` with the name `links` will increment the `links` violation counter for that user while `badName` will remains the same.

Then you can set up a rule with the  `x violations in y minutes` trigger so that when someone increments the counter `x times within y minutes`, the rule will trigger. Using this you can set up tiered punishments where repeated violations causes stricter punishments.

## Rule Options

### Trigger Types

#### **All caps**

* Triggers when a message contains more than x% of just capitalized letters.
  * **Min number of all caps:** Min number of caps needed to trigger
  * **Percentage of all caps:** Percent of the message needed to be made up of caps.&#x20;
* Both condition needs to be met to cause the trigger.&#x20;

#### **Message mentions**

* Triggers when a message includes more than x unique mentions&#x20;
  * **Threshold:** The number of unique mentions needed to trigger the rule.

#### **Any links**

* Triggers when a message contains any valid link

#### **X violation in Y minutes**

* Triggers when a user has more than x violations within y minutes.
  * **Violation name:** The violation key that we need to check&#x20;
  * **Number of violation:** The "x" number of violation needed to trigger the rule
  * **Within (minutes):** The "y" number of minutes that the violation needs to occur within.&#x20;
  * **Ignore if a higher violation trigger of this name was activated:**  Will be ignore if another violation trigger was activated that was higher up in punishment. Such as a ban violation if this was a kick violation.&#x20;

#### Word blacklist

* Triggers on messages containing words in the specified list
  * **List:** The list you want the rule to check against

#### Word whitelist

* Triggers on messages containing words not in the specified list
  * **List:** The list you want the rule to check against

#### **Website blacklist**

* Triggers on messages containing links to websites in the specified list
  * **List:** The list you want the rule to check against

#### **Website whitelist**

* Triggers on messages containing links to websites not in the specified list
  * **List:** The list you want the rule to check against

#### Server invites

* Triggers on messages containing invites to other servers, also includes some 3rd party server lists

#### Google flagged bad link

* Triggers on messages containing links that are flagged by Google Safe browsing as unsafe

#### **X channel message in Y seconds**

* Triggers when a channel has more than x messages in y seconds.
  * **Messages:** Number of "X" messages needed to trigger the rule
  * **Within (seconds):** The "Y" number of seconds that the word needs to occur within.

#### X user **message** in Y seconds

* Triggers when a user has more than x messages in y seconds in a single channel.
  * **Messages:** Number of "X" messages needed to trigger the rule
  * **Within (seconds):** The "Y" number of seconds that the word needs to occur within

#### User: X mentions within Y seconds

* Triggers when a user has sent more than x unique mentions in y seconds in a single channel
  * **Mentions:** Number of "X" mentions needed to trigger the rule
  * **Within (seconds):** The "Y" number of seconds that the word needs to occur within
  * &#x20;**Count multiple mentions of the same user**: Will count a mention to a user even if I it was previously mention before within the Y seconds.

#### Channel: X mentions within Y seconds

* Triggers when a channel has more than x unique mentions in y seconds
  * **Mentions:** Number of "X" mentions needed to trigger the rule
  * **Within (seconds):** The "Y" number of seconds that the word needs to occur within

#### Message matches Regex

* Triggers when a message matches the provided regex
  * **Regex:** The regex to trigger the rule

#### Message not matching regex

* Triggers when a message does not match the provided regex
  * **Regex:** The regex to trigger the rule

#### X consecutive identical messages

* Triggers when a user sends x identical messages after each other
  * **Threshold**: The number of x identical messages to trigger the rule

#### Nickname matches regex

* Triggers when a member's nickname matches the provided regex
  * **Regex:** The regex to trigger the rule

#### Nickname not matching regex

* Triggers when a member's nickname does not match the provided regex
  * **Regex:** The regex to trigger the rule

#### Nickname word blacklist

* Triggers when a member has a nickname containing words in the specified list (This is currently very easy to circumvent at the moment, and will likely be improved in the future)
  * **List:** The list you want the rule to check against

#### **Nickname word whitelist**

* Triggers when a member has a nickname not containing words in the specified list (This is currently very easy to circumvent at the moment, and will likely be improved in the future)
  * **List:** The list you want the rule to check against

#### x user attachments in y seconds

* Triggers when a user has more than x attachments within y seconds in a single channel
  * **Messages:** Number of "X" attachments needed to trigger the rule
  * **Within (seconds):** The "Y" number of seconds that the attachment needs to occur within

#### x channel attachments in y seconds

* Triggers when a channel has more than x attachments within y seconds
  * **Messages:** Number of "x" attachments needed to trigger the rule
  * **Within (seconds):** The "y" number of seconds that the attachment needs to occur within

#### Join username matches regex

* Triggers when a member's username matches the provided regex
  * **Regex:** The regex to trigger the rule

#### Join username not matching regex

* Triggers when a member's nickname does not match the provided regex
  * **Regex:** The regex to trigger the rule

#### Join username word blacklist

* Triggers when a member has a username containing words in the specified list (This is currently very easy to circumvent at the moment, and will likely be improved in the future)
  * **List:** The list you want the rule to check against

#### Join username word whitelist

* Triggers when a member has a nickname not containing words in the specified list (This is currently very easy to circumvent at the moment, and will likely be improved in the future)
  * **List:** The list you want the rule to check against

#### Join username invite

* Triggers when a member joins with a username that contains a server invite

#### New member

* Triggers when a new member joins

#### Message without attachments

* Triggers when a message does not contain an attachment

#### Message with attachments

* Triggers when a message contains an attachment

#### Flagged Scam links

* Triggers on messages that have scam links flagged by SinkingYachts and BitFlow AntiPhishing APIs

### Condition Types

#### **Ignore roles**

* Ignore users with at **** least one of these roles from this rule
  * **Role:** The list of roles to ignore.&#x20;

#### **Require roles**

* Require at **** least one of these roles on the user to trigger the rule
  * **Role:** The list of roles to ignore.&#x20;

#### **Ignore channels**

* Ignore the following channels
  * **Channel:** The list of channels to ignore.&#x20;

#### **Whitelist channels**

* Only check the following channel
  * **Channel:** The list of channels **** to check.&#x20;

#### **Account age above**

* Ignore users whose accounts age is less than the specified threshold
  * **Age in minutes:** The age specified to check upon

#### **Account age below**

* Ignore users whose accounts age is greater than the specified threshold
  * **Age in minutes:** The age specified to check upon

#### **Server members duration more than**

* Require members to have been on the server for more than x minutes
  * **Age in minutes:** The age specified to check upon

#### **Server member duration less than**

* Require members to have been on the server for less than x minutes
  * **Age in minutes:** The age specified to check upon

#### **Ignore bots**

* Ignore all bots

**Only bots**

* Only trigger on bots

#### **Ignore categories**&#x20;

* Ignore channels in the following categories
  * **Categories:** The list of categories to check

#### **Active in categories**&#x20;

* Only check channels in the following categories
  * **Categories:** The list of categories to check

### Effect Types

Effects with ability to add custom messages are capped to 150 characters.

#### **Delete Message**

* Deletes the message

#### **+Violation**

* Adds a violation **** (use with violation trigger)
  * **Name:** The violation key you are adding a violation too.

#### **Kick user**

* Kicks the user

#### **Ban user**

* Bans the user

#### **Mute user**

* Mutes the user
  * **Duration (Minute):** Duration to mute the user for.

#### **Warn user**

* Warns the user

#### **Set Nickname**

* Sets the nickname of the user
  * **New Nickname (empty for removal):** Set a new nickname for the user, if you leave it empty, it will reset the nickname.

#### **Reset violations**

* Resets the violations of a user.
  * Name

#### **Delete multiple messages**

* Deletes a certain number of the users last messages in this channel.
  * Number of messages
  * Max age (seconds)

#### **Give role**

* Gives the specified role to the user, optionally with a duration after which the role is removed from the user.
  * Duration in seconds, 0 for permanent
  * Role

#### **Enable Channel slowmode**

* Enables Discord's builtin slowmode in the channel for the specified duration, or forever.
  * Duration in seconds, 0 for permanent
  * Ratelimit in seconds between messages per user

#### **Remove role**

* Removes the specified role from the user, optionally with a duration after which the role is added back to the user.
  * Duration in seconds, 0 for permanent
  * Role

#### **Send Message**

* Sends the message on the channel the rule was triggered
  * Custom message
  * Delete sent message after x seconds (0 for non-deletion):
  * Ping user committing the infraction
  * Channel to send message in (Leave None to send message in same channel):

## Limitations

There are some limitations you need to be aware of when using Automoderator V2, which are listed below.

{% hint style="info" %}
**Note:** 'Normal' here means a normal server without YAGPDB Premium, 'Premium' means one with YAGPDB Premium.
{% endhint %}

* **Max message-based triggers:** 20 for normal, 100 for premium.
* **Max violation triggers:** 20 for normal, 100 for premium.
* **Max total rules:** 25 for normal, 150 for premium.
* **Max lists:** 5 for normal, 25 for premium.
* **Max rule parts:** This means the maximum amount of triggers, conditions, and effect in total you may have per rule. These will be truncated if they go over the limit.\
  __\
  __20 for both normal and premium.
* **Max rulesets:** 10 for normal, 25 for premium.

## Automoderator 1.0 to 2.0

### Slowmode&#x20;

{% tabs %}
{% tab title="Old version" %}
![](../.gitbook/assets/Slowmode1.0.PNG)
{% endtab %}

{% tab title="New version" %}
![](../.gitbook/assets/slowmode.PNG)
{% endtab %}
{% endtabs %}

### Mass Mention

{% tabs %}
{% tab title="Old version" %}
![](<../.gitbook/assets/Mass mention1.0.PNG>)
{% endtab %}

{% tab title="New version" %}
![](<../.gitbook/assets/Mass mention.PNG>)
{% endtab %}
{% endtabs %}

### Server Invite

{% tabs %}
{% tab title="Old version" %}


![](<../.gitbook/assets/Server Invite1.0.PNG>)
{% endtab %}

{% tab title="New version" %}
![](<../.gitbook/assets/Server Invite.PNG>)
{% endtab %}
{% endtabs %}

### Links

{% tabs %}
{% tab title="Old version" %}
![](../.gitbook/assets/Links1.0.PNG)
{% endtab %}

{% tab title="New version" %}
![](../.gitbook/assets/Links.PNG)
{% endtab %}
{% endtabs %}

### Banned Words

{% tabs %}
{% tab title="Old version" %}
![](<../.gitbook/assets/Banned Words1.0.PNG>)
{% endtab %}

{% tab title="New version" %}
![](<../.gitbook/assets/image (18).png>)
{% endtab %}
{% endtabs %}

### Banned Websites

{% tabs %}
{% tab title="Old version" %}
![](<../.gitbook/assets/Banned Websites1.0.PNG>)
{% endtab %}

{% tab title="New version" %}
![](<../.gitbook/assets/Banned Websites.PNG>)
{% endtab %}
{% endtabs %}
