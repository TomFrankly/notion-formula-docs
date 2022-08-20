---
description: Learn how to use the division (/) operator in Notion formulas.
---

# divide

The **divide (`/`)** operator allows you to divide two numbers and get their quotient.

The `/` operator follows the standard mathematical order of operations (PEMDAS). For more detail, see [Operator Precedence](../../reference/operator-precedence-and-associativity.md).

You can also use the function version, `divide()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
12 / 4 // Output: 3

divide(12,-4) // Output: -3
```
{% endcode %}

### Working with 3 or More Operands

Since **divide** is a binary operator, it can only work on two _operands -_ the objects which are being operated on ([if](if.md) is the only operator that works on three operands).

If you need to work with more than two operands, the shorthand `/` is by far the easiest way to do it.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
40 / 2 / 5 // Output: 4

divide(divide(40,2),5) // Output: 4
```
{% endcode %}

<details>

<summary>Can I switch the order of the numbers in a division statement?</summary>

No - unlike [addition](add.md) and [multiplication](multiply.md), which are **commutative,** division won’t work if you switch around the numbers you’re working with. `8/2 = 4`, but `2/8 = 0.25`.

The same applies when working with 3 or more operands.

`100/2/4/2 = 6.25`, while `(100/2)/(4/2) = 50/2 = 25`.

</details>

## Example Database

The example database below shows the per-person split for several heists carried out by a certain crew of classy thieves. The simple **Split** formula shows the `/` operator in action, and simply divides **Total** by **Shares.**

![](<../../.gitbook/assets/Heist Splitter.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/e23555cd83c345beb00576ec717a5ac7?v=5d30ae65cf614d509d1f50a0a9550fbd" %}

### "Split" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
prop("Total") / prop("Shares")
```
{% endcode %}

Instead of using hard-coded numbers, I’ve called in each property using the `prop()` function.

Curious about how the **Shares** formula is able to get a count from the **Members** property? See that breakdown here: [Count multi-select tags](../../formula-examples/count-multi-select-tags.md)

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
