---
description: Learn how to use the abs function in Notion formulas.
---

# abs

The `abs()` function calculates the absolute value of a [number](../../formula-basics/data-types/number.md).

A number’s absolute value is simply **how far it is away from zero.** Therefore, the absolute value of a negative number is equal to its positive equivalent - e.g. `abs(-5) == 5.`

In mathematical notation, absolute values are expressed by wrapping a number in || signs:

$$
|-12\;| = 12
$$

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
abs(-42) // Output: 42

abs(42) // Output: 42
```
{% endcode %}

## Example Database

Notion’s [dateBetween](datebetween.md) function subtracts the second argument from the first, and returns a number depending on the specified unit of time (e.g. “hours” or “seconds”).

If the second argument is a later date than the first argument’s date, `dateBetween()` will return a negative number. The formula in the table below uses the `abs()` function to ensure that the output is **always** positive.

![](<../../.gitbook/assets/Absolute Value abs Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/1e87813c4c844b718d44051b53f657f5?v=e24586c4a7864f57b8d5c4d9364fb975" %}

### “Seconds Between” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
abs(dateBetween(prop("Date 1"), prop("Date 2"), "seconds"))
```
{% endcode %}

#### Other formula components used in this example:

{% content-ref url="datebetween.md" %}
[datebetween.md](datebetween.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
