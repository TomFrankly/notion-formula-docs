---
description: Learn how to use the Boolean "larger" (>) operator in Notion formulas.
---

# larger

The larger (`>`) operator returns [true](../constants/true.md) if its left operand is greater than its right operand. It accepts [numeric](../../formula-basics/data-types/number.md), [date](../../formula-basics/data-types/date-data-type.md), and [Boolean](../../formula-basics/data-types/boolean-checkbox.md) operands.

You can also use the function version, `larger()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
2 > 1 // Output: true

42 > 50 // Output: false

// Boolean values equate to 1 (true) and 0 (false).
true > false // Output: true

true > true // Output: false

// For dates, "less than" equates to "before".
now() > dateSubtract(now(), 1, "days") // Output: true
```
{% endcode %}

{% hint style="info" %}
**Good to know:** When comparing dates, "larger" = "later".
{% endhint %}

## Example Database

This example database records the power levels of two fighters at different stages. The **Stronger** formula outputs a sentence stating who the stronger fighter is at that time.

![](<../../.gitbook/assets/Larger Operator Test Database - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/larger-1741d98bc3c14fd18f888bf4b122d610" %}

### "Stronger" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
((prop("Goku") > prop("Vegeta")) ? "Goku is stronger" : "Vegeta is stronger") + " during " + prop("Saga") + "."
```
{% endcode %}

This formula uses the conditional operators `?` and `:` to form an [if-then statement](if.md). The output is then combined with [strings](../../formula-basics/data-types/string.md) and the output of the **Saga** property via the [add](add.md) (`+`) operator (which can concatenate strings).

#### Other formula components used in this example:

{% content-ref url="if.md" %}
[if.md](if.md)
{% endcontent-ref %}

{% content-ref url="add.md" %}
[add.md](add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
