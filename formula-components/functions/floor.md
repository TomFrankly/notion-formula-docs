---
description: Learn how to use the floor function in Notion formulas.
---

# floor

The `floor()` function returns the largest integer that is less than or equal to its argument.

In other words, `floor()` rounds a non-whole [number](../../formula-basics/data-types/number.md) to the next smallest integer. When used on an integer, it will return that integer.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
floor(4.2) // Output: 4

floor(3.845) // Output: 3

floor(4) // Output: 4
```
{% endcode %}

### Negative Values

It’s worth noting that `floor()` rounds “downward towards negative infinity”, while its counterpart, [ceil](ceil.md), rounds “upward towards positive infinity”

When a negative value is passed as `floor()`'s argument, you’ll still get a smaller value.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
floor(-3.7) // Output: -4
```
{% endcode %}

`floor()` _does not_ round “towards zero”, and ceil does not round “away from zero”.

In JavaScript, the [Math.trunc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Math/trunc) function rounds “towards” zero. It simply removes all decimal values from a non-whole number - e.g. `Math.trunc(3.7) == 3` and `Math.trunc(-3.7) == -3`.

Notion does not have a `trunc()` function, but you can create one using an [if-then](../operators/if.md) statement:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a number property exists called Num
prop("Num") >= 0 ? floor(prop("Num")) : ceil(prop("Num"))
```
{% endcode %}

## Example Database

As stated above, Notion does not currently provide a `trunc()` function.&#x20;

The example database below provides a working example of a `trunc()` polyfill (a.k.a. custom code that replicates the functionality of a missing function), which uses both `floor()` and [ceil](ceil.md).

Floor and ceiling values are also provided for reference.

![](<../../.gitbook/assets/Floor Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/13afd5d04b9d4e038639870d20d90710?v=c0332ae024d34e43be923839cacd9988" %}

### “Trunc” Property Formula

```jsx
// Written with ternary operator (? and :)
prop("Num") >= 0 ? floor(prop("Num")) : ceil(prop("Num"))

// Written with if() and expanded
if(
    prop("Num") >= 0,
    floor(
        prop("Num")
    )
    ceil(
        prop("Num")
    )
)
```

A proper `trunc()` function (which does not exist in Notion) would simply chop all of the digits after the decimal off of a number and return the integer.

To create an effective polyfill for this function, we must first determine if our input number is positive or negative. We do this with `prop("Num") >= 0`, though the same could be accomplished with the [sign](sign.md) function: `sign(prop("Num")) == 1`

If the input number is positive, we pass it as an argument to `floor()`.

If it is negative, we must instead pass it as an argument to [ceil](ceil.md).

You can check this in the example table above by comparing the output in the **Trunc** column to that of the **Floor** and **Ceil** columns.

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="ceil.md" %}
[ceil.md](ceil.md)
{% endcontent-ref %}

{% content-ref url="../operators/largereq.md" %}
[largereq.md](../operators/largereq.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
