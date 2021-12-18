# Using RegEx

Full RE2 syntax reference at > [https://github.com/google/re2/wiki/Syntax](https://github.com/google/re2/wiki/Syntax)\
Go RegExp doc at > [https://golang.org/pkg/regexp/](https://golang.org/pkg/regexp/)\
More about general concepts > [http://www.regular-expressions.info](http://www.regular-expressions.info)

## Basic Regex

**Basics of Regular Expressions**

{% tabs %}
{% tab title="Match" %}
You can match a word by putting it between two brackets.

_As example, this will only match the word "Dinosaur":_ `(Dinosaur)`
{% endtab %}

{% tab title="Don't match" %}
Using `?:` after opening parenthesis of a capturing group creates a non-capturing group. Useful for example with template function `reFindAllSubmatches`.

_This will not sub-match the words "red, blue, green":_ \
__``{{ reFindAllSubmatches `(?:color=)(red|blue|green)` "color=red beautiful" }}``&#x20;

To clarify more - it will not show `dateid,` because it's a whole match:\
``{{ slice (index (reFindAllSubmatches `(?:dateid=)([0-9]{5})` "dateid=12345") 0) 1 }}``
{% endtab %}

{% tab title="Match A or B" %}
You may also want to catch multiple options, for that we use a _"Vertical bar"_ or also known as a _"Pipe"_ between linux users.

_As example, this will match if either "Cat" or "Dog" is present:_ `(Cat|Dog)`
{% endtab %}
{% endtabs %}

To match anything of any length, use `.*`.

**Character classes**

{% tabs %}
{% tab title="Words" %}
To match a word, you put it between two brackets.&#x20;

Example: `(Banana)`
{% endtab %}

{% tab title="Characters" %}
For matching characters there are multiple options:

#### Matching specific characters:

For matching a specific character, you put them in square brackets.

This will match A, B and C: `([abc])`

This will match every character from A-z: `([A-z])`

This will match every number: `([0-9])`
{% endtab %}

{% tab title="Special Characters" %}
Sometimes you have to use special characters but it may cause conflicts. In this case, you will have to use an escape character.

For example, this is a star that doesn't interfere with other matches `\*`.
{% endtab %}
{% endtabs %}

## Understanding Regex

If you still do not know what Regex are or want to know more. Check out the cheat sheet on the site below.&#x20;

{% embed url="https://www.computerhope.com/jargon/r/regex.htm" %}

## Great tools for writing and testing Regex

{% embed url="https://regex-golang.appspot.com/" %}

{% embed url="https://regex101.com/" %}

