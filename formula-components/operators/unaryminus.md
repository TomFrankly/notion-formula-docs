---
description: Learn how to use the unaryMinus (-) operator in Notion formulas.
---

# unaryMinus

The **unaryMinus (`-`)** operator negates a [number](../../formula-basics/data-types/number.md).

Unary negation _negates_ a number; it does not simply make it negative. This means you can use it to make a negative number positive.

This is useful to keep in mind since [unaryPlus](unaryplus.md) does not make a number positive; it converts non-numeric data to a number.

You can also use the function version, `unaryMinus()`.

{% hint style="info" %}
**Good to know:** A _unary_ operator only has a single operand, while a _binary_ operator has two. unaryMinus and unaryPlus are, as their names imply, unary operators. Examples of binary operators include [add](add.md), [divide](divide.md), [pow](pow.md), etc.
{% endhint %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
-42 // Output: -42

-(-42) // Output: 42

unaryMinus(42) // Output: -42
```
{% endcode %}

### Expressing Negative Values

It's important to know that Notion's formula editor will sometimes interpret the `-` symbol as a unaryMinus in situations where you're trying to express a truly negative value.

This can happen with the [mod](mod.md) (`%`) operator when the divisor is a hard-coded negative number.

{% code overflow="wrap" lineNumbers="true" %}
```javascript
19 % -12 // Outputs incorrect value of -11.81
19 % (-12) // Correctly outputs 7

// Negative value passed via a property does not need to 
// be wrapped in () symbols

prop("negative num") == -12
19 % prop("negative num") // Output: 7
```
{% endcode %}

As shown in the code block above, this does not apply to negative values passed via a property. Those values will be truly negative since a property can't add a unaryMinus operator (or any operator) to your formula.

You can read more about this distinction in the [Negative Divisors](mod.md#negative-divisors) section of the [mod](mod.md) article.

{% hint style="info" %}
Good to know: Parentheses `()` have the highest [operator precedence](../../reference/operator-precedence-and-associativity.md) in Notion formulas, so you can avoid all sorts of confusion by using them to make the order of your formula's operation explicitly defined.
{% endhint %}

### Type Conversion with unaryPlus

[Unlike in JavaScript,](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Unary\_negation) unaryMinus does not convert other data types (such as [strings](../../formula-basics/data-types/string.md) or [Booleans](../../formula-basics/data-types/boolean-checkbox.md)) to numbers in Notion.

However, you can combine it with [unaryPlus](unaryplus.md) to quickly convert a numeric string or boolean to a number. You can also combine it with [toNumber](../functions/tonumber.md), which can convert [dates](../../formula-basics/data-types/date-data-type.md) to numbers (unaryPlus cannot do this).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
-+"42" // Output: -42

-+"-42" // Output: 42

-+true // Output: -1

-toNumber(now()) // Output: -165479808000 (will change with now()'s timestamp)
```
{% endcode %}

## Example Database

The table below uses unaryMinus with an [if](if.md) statement to create a manual absolute value function. Notion comes with [abs](../functions/abs.md), so building this is just useful as a proof-of-concept.

![](<../../.gitbook/assets/Absolute Value with unaryMinus.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/54a1ae1dffe345df820822bc3db13058?v=a85a875764e54e7ca8b1d41be6798570" %}

### "Abs" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed

if(prop("Num 1") - prop("Num 2") < 0, -(prop("Num 1") - prop("Num 2")), prop("Num 1") - prop("Num 2"))

// Expanded

if(
  prop("Num 1") - prop("Num 2") < 0,
	-(
		prop("Num 1") - prop("Num 2")
	),
  prop("Num 1") - prop("Num 2")
)
```
{% endcode %}

This formula checks whether the difference between Num 1 and Num 2 is less than zero. If it is, it applies the `-` operator to the entire equation in order to get the absolute value.

#### Other formula components used in this example

{% content-ref url="if.md" %}
[if.md](if.md)
{% endcontent-ref %}

{% content-ref url="smaller.md" %}
[smaller.md](smaller.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
