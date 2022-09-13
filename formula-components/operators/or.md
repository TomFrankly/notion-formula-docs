---
description: Learn how to use the Boolean "or" operator in Notion formulas.
---

# or

The **or** operator returns [true](../constants/true.md) if either one of its operands is true. It accepts [Boolean](../../formula-basics/data-types/boolean-checkbox.md) operands.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
Boolean or Boolean
or(Boolean, Boolean)
```
{% endcode %}

{% hint style="info" %}
**Good to know:** Notion is picky, so `||`, `OR`, and `Or` won’t work here. Only the case-sensitive `or` will be accepted.
{% endhint %}

You can also use the function version, `or()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
true or false // Output: true

false or true // Output: true

false or false // Output: false

10 > 20 or "Cat" == "Cat" // Output: true
```
{% endcode %}

The `or` operator can also be chained together multiple times:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
10 > 20 or "Cat" == "Dog" or true // Output: true
```
{% endcode %}

## Example Database

This example database records the results of several Rock, Paper, Scissors matches. The **Winner** formula declares the winner of each match.

![](<../../.gitbook/assets/Rock Paper Scissors - Or Operator Example - Notion Formula.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/or-538fa5be23b6478fa200375a040d44eb" %}

### “Winner” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
(prop("P1 Throw") == prop("P2 Throw")) ? "Tie" : ((prop("P1 Throw") == "Rock" and prop("P2 Throw") == "Scissors" or prop("P1 Throw") == "Paper" and prop("P2 Throw") == "Rock" or prop("P1 Throw") == "Scissors" and prop("P2 Throw") == "Paper") ? prop("Player 1") : prop("Player 2"))

// Expanded
(prop("P1 Throw") == prop("P2 Throw")) ? "Tie" : 
    (  (prop("P1 Throw") == "Rock" and prop("P2 Throw") == "Scissors" or 
        prop("P1 Throw") == "Paper" and prop("P2 Throw") == "Rock" or 
        prop("P1 Throw") == "Scissors" and prop("P2 Throw") == "Paper") ? 
    prop("Player 1") : 
    prop("Player 2"))
```
{% endcode %}

The formula consists of a nested [if-then statement](if.md) (written with the conditional operators `?` and `:`). It first checks to see if the players threw the same choice, and returns **“Tie”** if so. If not, it uses the `or` and [`and`](and.md) operators to determine the winner.

Since the win/lose value of a throw is determined by the other throw, we use a series of three statements to compare Player 1’s throw against Player 2’s.

{% hint style="info" %}
**Good to know:** This example also shows how `or` has a lower [operator precedence](../../reference/operator-precedence-and-associativity.md) than `and`.
{% endhint %}

#### Other formula components used in this example:

{% content-ref url="if.md" %}
[if.md](if.md)
{% endcontent-ref %}

{% content-ref url="equal.md" %}
[equal.md](equal.md)
{% endcontent-ref %}

{% content-ref url="and.md" %}
[and.md](and.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
