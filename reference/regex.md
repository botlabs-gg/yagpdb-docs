# Using RegEx

## Basic Regex

**Basics of Regular Expressions**

{% tabs %}
{% tab title="Match" %}
You can match a word by putting it between two brackets.

_As example, this will only match the word "Dinosaur":_ `(Dinosaur)`
{% endtab %}

{% tab title="Don\'t match" %}
If you don't want to match something you will have to put a `?:` before it.

_As example, this will not match the word "Donkey":_ `(?:Donkey)`
{% endtab %}

{% tab title="Match A or B" %}
You may also want to catch multiple options, for that we use a _"Vertical bar"_ or also known as a _"Pipe"_ between linux users.

_As example, this will match if either "Cat" or "Dog" is present:_ `(Cat|Dog)`
{% endtab %}
{% endtabs %}

To match anything of any length, use `(?)`.

**Character classes**

{% tabs %}
{% tab title="Words" %}
To match a word, you put it between two brackets. 

Example: `(Banana)`
{% endtab %}

{% tab title="Characters" %}
For matching characters there are multiple options:

#### Matching specific characters:

For matching a specific character, you put them in square brackets.

This will match A, B and C: `([abc])`

This will match every character from a-Z: `([a-Z])`

This will match every number: `([0-9])`
{% endtab %}

{% tab title="Special Characters" %}
Sometimes you have to use special characters but it may cause conflicts. In this case, you will have to use an escape character.

For example, this is a star that doesn't interfere with other matches `\*`.
{% endtab %}
{% endtabs %}

## Understanding Regex

If you still do not know what Regex are or want to know more. Check out the cheat sheet on the site below. 

{% embed url="https://www.computerhope.com/jargon/r/regex.htm" %}

## Great tools for writing and testing Regex

{% embed url="https://regex-golang.appspot.com/" %}

{% embed url="https://regex101.com/" %}



