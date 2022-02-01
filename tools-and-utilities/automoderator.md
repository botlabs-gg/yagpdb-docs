# Basic Automoderator

{% hint style="warning" %}
Remember to enable **Basic Automoderator** in the main interface if you wish to use it, in addition to the individual rulesets you need! Then, click `Save All Settings`.
{% endhint %}

{% hint style="info" %}
Basic Automoderator is fine for setting up a simple automod system, but for more complex auto moderation, you may want to look at [AutomodV2](automoderator-v2.md), as it provides more flexibility but is significantly more complex.
{% endhint %}

## Introduction

Basic Automoderator can be configured through different predefined **rules.** Within these rules, you can set different options to customize it to what you like. For those of you who are familiar with AutomodV2, rules are similar to rulesets, except they have less options.

## Rules

_We will be talking about all these rules and their options in-depth further in this article._

1. **Slowmode**\
   This rule allows you to only let users send a certain amount of messages within a given timespan.
2. **Mass Mention**\
   ****This rule allows you to detect messages which contain more than a certain amount of mentions in them.
3. **Server Invites**\
   ****This rule allows you to delete messages with invite links.
4. **Links**\
   ****This rule allows you to delete messages with links.
5. **Banned words/websites**\
   ****YAGPDB comes with a built-in list of bad words and sites which can be used, or you can configure your own!

## Options available across all rules

There are two things available across all rules, which we will talk about here.

### Violations

Violations are important in both Basic Automoderator and AutomodV2 (if you wish to transition to it later). In Basic Automoderator, **violations** are used to keep track of how many infractions a user has, with an optional expiry time. This is very useful for doing an action after several violations have occurred, such as muting the user if, say, they have spammed three times in a row.

![Violation options (shared for all rules)](<../.gitbook/assets/image (9).png>)

In every rule, you can configure giving violations after an optional expiry time, and act on them if the violations for a given user have gone past a defined amount. The three actions available are:

* Mute after (with configurable mute duration in minutes)
* Kick after
* Ban after

To disable any one or all of these actions, you can set the option the amount of violations to punish after to **0.**

{% hint style="info" %}
Violations are separate / different for each rule, meaning that a violation for **Slowmode** would not trigger a violation action set for **Mass Mention**.
{% endhint %}

### Ignore roles / channels

This one is rather self-explanatory - you can ignore given channels or roles from triggering the rule. For example, let's say we ignore the role `Staff` from triggering the **Slowmode** rule and ignore the channel `counting` from triggering the rule like below:

![](<../.gitbook/assets/image (10).png>)

If we configured everything else correctly, anyone with the `Staff` role would not trigger slowmode. Any message sent in the `#counting` channel would also be ignored.

Now that we've gotten this out of the way, we can move on to the individual rules.

## Rules available

### Slowmode

![Complete options for slowmode](<../.gitbook/assets/image (8).png>)

As we can see, there are several options available after you navigate to the slowmode rule tab. However, we can ignore the part about violations and ignore roles / channels, as they are shared across all rules. Taking those out, we are left with two very self-explanatory options:

![Options for slowmode](<../.gitbook/assets/image (11).png>)

As we can see, the two options are **Number of messages** and **Within (seconds)**. For example, if we set the `Number of messages` option to 5 and the `Within (seconds)` option to 2, the ruleset would trigger if we sent 5 messages in 2 seconds, but not 4 messages in 2 seconds.&#x20;

### Mass Mention

![Options for mass mention](<../.gitbook/assets/image (12).png>)

As we can see, there is only one option for this rule if we take out ignored roles / channels and violations. This is **Mention threshold -** which is how many mentions a user would need to mention _in a single message_ for this ruleset to be triggered.&#x20;

{% hint style="danger" %}
This ruleset will not trigger if you mention the _same_ person, only if you mention different people. For example, if we had the threshold as `2` and we mentioned `Jonas747` twice, it would not trigger. However, if we mentioned `Jonas747` _and_  `YAGPDB`, it would trigger.
{% endhint %}

### Server invites

This one is extremely self explanatory - all you need to do is enable it. It will detect server invites and delete them.

{% hint style="danger" %}
This ruleset will not trigger if you send an invite for the current server you set the ruleset for, only other servers.
{% endhint %}

### Links

Another self-explanatory rule! All you need to do is set it up, and YAGPDB will remove any links sent.

### Banned words

![Unique options for Banned words](<../.gitbook/assets/image (13).png>)

There are two options that you can set for this rule - `Ban built-in swear words` and `Banned words`. The former is a yes/no checkbox. If it is enabled, YAGPDB will use its built-in swear word list (available [here](https://github.com/jonas747/yagpdb/blob/master/automod\_legacy/swearwords.go)) in addition to the ones provided.

The **Banned words** option is a simple list of all the words you wish to ban. They should be separated by either spaces or newlines: i.e `hello,world` would ban both hello and world, while `hello`\
`world` would do the same.&#x20;

{% hint style="danger" %}
Banned words only work on words - meaning not phrases. This translates to "you can only ban words without spaces in them".
{% endhint %}

### Banned websites

![Unique options for Banned websites](<../.gitbook/assets/image (14).png>)

There are also three options that you can set for this rule - `Google safebrowsing` integration, `Scam link protection` and `Banned sites`. The first two are simple checkbox-sliders and they automatically detect sites that contain malware using Google safebrowsing or Scam link APIs by SinkingYachts and BitFlow, in addition to the ones provided.

The **Banned websites** option is a simple list of all the **hosts** you wish to ban, again separated by either spaces or newlines. Note that here, you cannot ban specific subdomains and not the whole site - `google.com` would ban `fun.google.com`. Note the lack of the https protocol in front of the site. To ban `google.com`, we simply banned `google.com`, not `https://google.com`.

