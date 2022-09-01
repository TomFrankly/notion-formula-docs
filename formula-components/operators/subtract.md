---
description: Learn how to use the subtract (-) operator in Notion formulas.
---

# subtract

The **subtract (`-`)** operator allows you to subtract two [numbers](../../formula-basics/data-types/number.md) and return their difference.

When used in mathematical equations, the `-` operator follows the standard mathematical order of operations (PEMDAS). For more detail, see [Operator Precedence](../../reference/operator-precedence-and-associativity.md).

You can also use the function version, `subtract()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
12 - 5 // Output: 7

subtract(5,12) // Output: -7
```
{% endcode %}

### Working with 3 or More Operands

Since **subtract** is a binary [operator](./), it can only work on two _operands -_ the objects which are being operated on ([if](if.md) - the _ternary operator -_ is the only operator that works on three operands).

If you need to work with more than two operands, the shorthand `-` is by far the easiest way to do it.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
40 - 10 - 5 // Output: 25

subtract(subtract(40,10),5) // Output: 25
```
{% endcode %}

## Example Database

The example database below tracks a weekend of treasure-spending by three pirates. Each starts with a **Start Budget** of $3,000, and the **Leftover** formula shows how much each has left after the weekend.

![](<../../.gitbook/assets/Subtract Example.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/subtract-93cccb300faf4ca4b7b9d0b2d3c898eb" %}

Note how I’ve set the **number format** of each column to **U.S. Dollar.** I’ve also set each column’s **Calculate** value to **Sum,** allowing me to see the total of all rows put together.

### "Leftover" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
prop("Start Budget") - prop("Saturday") - prop("Sunday")
```
{% endcode %}

Instead of using hard-coded numbers, I’ve called in each property using the `prop()` function.

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
