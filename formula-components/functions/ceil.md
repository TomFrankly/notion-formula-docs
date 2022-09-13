---
description: Learn how to use the ceil function in Notion formulas.
---

# ceil

The `ceil()` function returns the smallest integer that is greater than or equal to its argument.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
ceil(number)
```
{% endcode %}

In other words, `ceil()` rounds a non-whole [number](../../formula-basics/data-types/number.md) to the next largest integer. When used on an integer, it will return that integer.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
ceil(4.2) // Output: 5

ceil(3.845) // Output: 4

ceil(4) // Output: 4

// Calculate the donated change in a round-up donation
// Assume prop("Subtotal") is $5.34
ceil(prop("Subtotal")) - prop("Subtotal")
// Output: $0.66
```
{% endcode %}

### Negative Values

It’s worth noting that `ceil()` rounds “upward towards positive infinity”, while its counterpart, [floor](floor.md), rounds “downward towards negative infinity”

When a negative value is passed as `ceil()`'s argument, you’ll still get a greater value.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
ceil(-3.7) // Output: -3
```
{% endcode %}

`ceil()` _does not_ round “away from zero”, and floor does not round “towards” zero.

In JavaScript, the [Math.trunc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Math/trunc) function rounds “towards” zero. It simply removes all decimal values from a non-whole number - e.g. `Math.trunc(3.7) == 3` and `Math.trunc(-3.7) == -3`.

Notion does not have a `trunc()` function, but you can create one using an [if-then](../operators/if.md) statement:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a number property exists called Num
prop("Num") >= 0 ? floor(prop("Num")) : ceil(prop("Num"))
```
{% endcode %}

You can see a [working example database](floor.md#example-database) showing this formula in action in the [floor](floor.md) article.

## Example Database

Stores often ask customers if they would like to make a donation to charity along with their purchase.

This example database calculates donations based on four possible options - **$1, $5, Round-Up,** and **no donation**.

A “round-up” donation simply rounds the purchase sub-total to the next greatest whole dollar, and donates the change.

![](<../../.gitbook/assets/Ceil Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/ceil-639508a0283f4b43a4898ca2efaf02ff" %}

### “Donation” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(contains(prop("Donation Choice"),"$"),toNumber(replaceAll(prop("Donation Choice"),"[^\\d]","")),if(prop("Donation Choice") == "Round-Up",ceil(prop("Subtotal")) - prop("Subtotal"),0))

// Expanded
if(
    contains(
        prop("Donation Choice"),
        "$"
    ),
    toNumber(
        replaceAll(
            prop("Donation Choice"),
            "[^\\d]",
            ""
        )
    ),
    if(
        prop("Donation Choice") == "Round-Up",
        ceil(prop("Subtotal")) - prop("Subtotal"),
        0
    )
)
```
{% endcode %}

The **Donation Choice** select property models multiple-choice buttons that customers may press on a point-of-sale system.

This formula calculates the donation based on the customer’s choice of **$1, $5, Round-Up**, or **no donation.**

A [nested if statement](../operators/if.md#nested-if-then-statements) is used to check which option was chosen, and to execute different logic depending on the choice.

First, the [contains](contains.md) function is used to check if the choice contains `$`. If so, we know that the choice was either **$1** or **$5**.

Since Select options are [strings](../../formula-basics/data-types/string.md) by default, we use [replaceAll](replaceall.md) and a small [regular expression](../../reference/regular-expressions-in-notion-formulas.md) to remove any non-numeric character from that string (`[^\\d]` translates to “any character that isn’t a digit”).&#x20;

Then we use [toNumber](tonumber.md) to [convert](../../reference/converting-data-types.md) the resulting string to an actual [number](../../formula-basics/data-types/number.md) and output it.

If the Select option _doesn’t_ contain a `$`, then we check if it is [equal](../operators/equal.md) to `Round-Up`.

If so, we use `ceil()` to find the amount of change donated in the round-up donation: `ceil(prop("Subtotal")) - prop("Subtotal")`.

Finally, if the `None` option was chosen, we set the donation to `$0`.

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="tonumber.md" %}
[tonumber.md](tonumber.md)
{% endcontent-ref %}

{% content-ref url="replaceall.md" %}
[replaceall.md](replaceall.md)
{% endcontent-ref %}

{% content-ref url="contains.md" %}
[contains.md](contains.md)
{% endcontent-ref %}

{% content-ref url="../operators/equal.md" %}
[equal.md](../operators/equal.md)
{% endcontent-ref %}

{% content-ref url="../operators/subtract.md" %}
[subtract.md](../operators/subtract.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
