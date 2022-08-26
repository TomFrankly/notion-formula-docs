---
description: Learn about the Number data type in Notion formulas.
---

# Number

The Number data type holds and represents numbers. Numbers can be used with mathematical operators such as add `+` and divide `/` to perform mathematical operations and calculations.

{% code overflow="wrap" lineNumbers="true" %}
```javascript
2 + 2 // Output: 4

6 / 2 // Output: 3
```
{% endcode %}

Mathematical operations follow the standard mathematical order of operations (PEMDAS).&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```javascript
3 + 4 * 5 // Output: 23

(3 + 4) * 5 // Output: 35
```
{% endcode %}

To learn more, see the guide on operator precedence and associativity:

{% content-ref url="../../reference/operator-precedence-and-associativity.md" %}
[operator-precedence-and-associativity.md](../../reference/operator-precedence-and-associativity.md)
{% endcontent-ref %}

Notion will automatically convert numbers with more than 21 digits to scientific notation:

<figure><img src="../../.gitbook/assets/Scientific Notation in Numbers.png" alt=""><figcaption></figcaption></figure>

See this in action in this example database:

{% embed url="https://thomasfrank.notion.site/Scientific-Notation-for-Numbers-d8533f5b29ac4705a21e40960e57325f" %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
