---
description: Learn how to use the sqrt function in Notion formulas.
---

# sqrt

The `sqrt()` function returns the square root of its argument. `sqrt()` accepts only [numbers](../../formula-basics/data-types/number.md).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
sqrt(number)
```
{% endcode %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
sqrt(16) // Output: 4

sqrt(100) // Output: 10

sqrt(73-3^2) // Output: 8
```
{% endcode %}

## Example Database

This example database uses the Pythagorean Theorem to solve for the missing side of any right triangle. Two of the three side lengths must be provided; the Calculator property will solve for the missing one.

<figure><img src="../../.gitbook/assets/Sqrt Function - Square Root - Notion Formulas (1).png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/sqrt-30437a7238fd4c99a36a4dd4cda9ed01" %}

### "Calculator" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(empty(prop("Hypotenuse")) and empty(prop("Side 1")) or empty(prop("Hypotenuse")) and empty(prop("Side 2")) or empty(prop("Side 1")) and empty(prop("Side 2")), "Not enough information!", if(empty(prop("Hypotenuse")), "Hypotenuse: " + format(round(sqrt(prop("Side 1") ^ 2 + prop("Side 2") ^ 2) * 100) / 100), if(empty(prop("Side 1")), "Side 1: " + format(round(sqrt(prop("Hypotenuse") ^ 2 - prop("Side 2") ^ 2) * 100) / 100), "Side 2: " + format(round(sqrt(prop("Hypotenuse") ^ 2 - prop("Side 1") ^ 2) * 100) / 100))))

// Expanded
if(
    empty(
        prop("Hypotenuse")
    ) and empty(
        prop("Side 1")
    ) or empty(
        prop("Hypotenuse")
    ) and empty(
        prop("Side 2")
    ) or empty(
        prop("Side 1")
    ) and empty(
        prop("Side 2")
    ),
    "Not enough information!",
    if(
        empty(
            prop("Hypotenuse")
        ),
        "Hypotenuse: " +
        format(
            round(
                sqrt(
                    prop("Side 1")^2 + prop("Side 2")^2
                ) * 100
            ) / 100
        ),
        if(
            empty(
                prop("Side 1")
            ),
            "Side 1: " + 
            format(
                round(
                    sqrt(
                        prop("Hypotenuse")^2 - 
                        prop("Side 2")^2
                    ) * 100
                ) / 100
            ),
            "Side 2: " + 
            format(
                round(
                    sqrt(
                        prop("Hypotenuse")^2 - 
                        prop("Side 1")^2
                    ) * 100
                ) / 100
            )
        )
    )
)
```
{% endcode %}

I'll start this explanation off by saying that you can create a much simpler Pythagorean Theorem calculator that solves for the Hypotenuse only with: `sqrt(prop("Side 1") ^ 2 + prop("Side 2") ^ 2)`.

The example above goes a few steps further. It rounds its answer to two decimal places using the [round](round.md) function (see that function's page for tips on how to round to specific decimal places).

It also solves for _any_ missing side of a right triangle, so long as the other sides have been provided.

The formula first checks to make sure there's enough information to make a calculation. We use the [empty](https://app.gitbook.com/o/uX0b6x9kReic3MbNhHWv/s/WPoeEmtiEf1Sk7i11bvB/) function for this, and we must do so several times since we're checking to see if any two of the three number properties are empty.

{% hint style="info" %}
**Good to know:** The [or](../operators/or.md) operator has lower [operator precedence](../../reference/operator-precedence-and-associativity.md) than the [and](../operators/and.md) operator, so this part of the formula executes as `(empty(prop("Hypotenuse")) and empty(prop("Side 1"))) or (empty(prop("Hypotenuse")) and empty(prop("Side 2")))`.

In other words, all of the `and` clauses are executed _before_ the first `or` clause.
{% endhint %}

After this error-checking stage, the formula uses a [nested if-statement](../operators/if.md#nested-if-then-statements) to determine the correct calculation to perform.

If the hypotenuse is missing, we use the following formula to solve for it, where Side 1 and Side 2 are $$a$$ and $$b$$  respectively:

$$
\sqrt{a^2+b^2}
$$

If one of the sides is missing, we instead use this formula, where $$c$$ is the hypotenuse, and $$b$$ is the non-missing side:

$$
\sqrt{c^2-b^2}
$$

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="empty.md" %}
[empty.md](empty.md)
{% endcontent-ref %}

{% content-ref url="../operators/and.md" %}
[and.md](../operators/and.md)
{% endcontent-ref %}

{% content-ref url="../operators/or.md" %}
[or.md](../operators/or.md)
{% endcontent-ref %}

{% content-ref url="format.md" %}
[format.md](format.md)
{% endcontent-ref %}

{% content-ref url="round.md" %}
[round.md](round.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

{% content-ref url="../operators/multiply.md" %}
[multiply.md](../operators/multiply.md)
{% endcontent-ref %}

{% content-ref url="../operators/divide.md" %}
[divide.md](../operators/divide.md)
{% endcontent-ref %}

{% content-ref url="../operators/pow.md" %}
[pow.md](../operators/pow.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
