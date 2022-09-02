---
description: Learn how to return a null (or empty) value from a Notion formula.
---

# Return Null/Empty Values in Formulas

[Unlike JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/null), Notion formulas do have a **null** data type. However, it is possible to make a formula return a null/empty value using a couple of easy workarounds.

To return a null/empty string, use a pair of double quotes `""`:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
""
```
{% endcode %}

To return a null/empty number, use the following formula (c_redit to_ [_aNotioneer on Twitter_](https://twitter.com/aNotioneer/status/1565799381756006407) _for this number workaround_):

{% code overflow="wrap" lineNumbers="true" %}
```javascript
toNumber("")
```
{% endcode %}

Likewise, you can return a null/empty date object using this formula:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
fromTimestamp(toNumber(""))
```
{% endcode %}

There is no possible null/empty state for Booleans/Checkboxes. However, you can convert Booleans to strings with format in order to create a setup where true/false/_empty_ is possible:

<pre class="language-javascript" data-overflow="wrap" data-line-numbers><code class="lang-javascript">// Assume "Checkbox" is a Boolean/Checkbox property.

// Invalid; will throw a Type Mismatch error:
if( 1 > 2, prop("Checkbox"), "")

// Valid. Will output "true", "false", or an empty value.
<strong>if( 1 > 2, format(prop("Checkbox")), "")</strong></code></pre>

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
