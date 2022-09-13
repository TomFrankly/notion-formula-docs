---
description: Learn how to use the Boolean constant false in Notion formulas.
---

# false

The `false` constant represents the [Boolean](../../formula-basics/data-types/boolean-checkbox.md) output `false`. Its opposite is [true](true.md).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
false
```
{% endcode %}

Type `false` into a Notion formula property, and that property will output an **unchecked checkbox,** representing the value `false`.

A **Boolean** value has only two states, which can be thought of as:

* True or False
* 1 or 0
* On or Off

A Boolean simply represents the two _truth values_ of logic.

Notion represents Boolean values with checked (true) and unchecked (false) checkboxes.

<details>

<summary>Learn more about Booleans</summary>

These resources aren’t necessary for understanding how to work with Booleans in Notion, but you may find them interesting if you want to dive deeper into how Booleans are used in programming and computer science.

* [Crash Course - Boolean Logic & Logic Gates (YouTube)](https://www.youtube.com/watch?v=gI-qXk7XojA)
* [What is a Boolean Data Type, and What are Some Uses? (Sitepoint)](https://www.sitepoint.com/boolean-data-type/)

</details>

## Example Formulas

This formula will simply output `false` in a Notion formula property, displaying as an unchecked checkbox:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
false
```
{% endcode %}

Here’s a slightly more complex example formula that uses Notion’s [if](../operators/if.md) function:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
false ? "😀" : "😭"
```
{% endcode %}

This is an `if()` statement written in shorthand - it could also be written as `if(false,"😀","😭")`. It will simply output 😭 if the **condition** is false. The condition is the first part of the `if()` statement, or what is left of the `?` in the shorthand formula.

Since the Boolean `false` outputs `false` naturally, the result will be 😭. See the **Sad** property in the example database below for proof.

## Example Database

{% hint style="warning" %}
`true` and `false` are **case-sensitive.** Typing `True` or `False` will result in a syntax error.
{% endhint %}

Here you can see how Notion displays `true` and `false` Boolean values. You can also see the output of our **Sad** formula, which is shown above.

![](<../../.gitbook/assets/True and False (1).png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/False-0866870ee81443dba6b677ba8c98262b" %}

**Other formula components used in this example:**

{% content-ref url="true.md" %}
[true.md](true.md)
{% endcontent-ref %}

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
