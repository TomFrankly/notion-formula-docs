---
description: Learn how to use the log10 function in Notion formulas.
---

# log10

The `log10()` function returns the base-10 logarithm of a [number](../../formula-basics/data-types/number.md).

For reference, here are the named components of a logarithm:

$$
\log_{base} argument = exponent
$$

A **logarithm** is the exponent of the base that returns the argument.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
log10(1000) // Output: 3

log10(10) // Output: 1
```
{% endcode %}

Want to learn more about logarithms? Check out this resource:

{% embed url="https://betterexplained.com/articles/using-logs-in-the-real-world/" %}

### Computing Logs with Other Bases (Log Base X)

Notion only provides `log10()`, [log2](log2.md), and [ln](ln.md) because those are by far the most commonly-used log bases.

However, if you need to compute a log with a different base, you can use the [change of base formula](https://www.khanacademy.org/math/algebra2/x2ec2f6f830c9fb89:logs/x2ec2f6f830c9fb89:change-of-base/a/logarithm-change-of-base-rule-intro):

$$
\log_x y= (\frac{\ln y}{\ln x})
$$

So, for example:

$$
\log_3 81 = (\frac{\ln 81}{\ln 3})
$$

Here’s a Notion formula to compute this:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
ln(81) / ln(3) // Output: 4
```
{% endcode %}

## Example Database

$$log_{10}$$ can be used to perform an interesting mathematical trick – finding the length (i.e. number of digits) in any number. It is done by taking the **floor value** of a number’s $$log_{10}$$, then adding one:

$$
\lfloor log_{10}n \rfloor + 1
$$

The example database below shows this trick in action.

![](<../../.gitbook/assets/Log10 Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/log10-a6d3e62f27f34319b69582b02085fe36" %}

### "Length" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
floor(log10(prop("Num"))) + 1

// Expanded
floor(
    log10(
        prop("Num")
    )
) + 1
```
{% endcode %}

If you’re curious about the math behind why this trick works, check out this thread:

{% embed url="https://math.stackexchange.com/questions/231742/proof-how-many-digits-does-a-number-have-lfloor-log-10-n-rfloor-1" %}

The formula itself is quite simple:

1. We pass `prop("Num")` to the `log10()` function.
2. This value is then run through the [floor](floor.md) function in order to round it to its nearest integer of lower or equal value.
3. Finally, we add `1`.

#### Other formula components used in this example:

{% content-ref url="floor.md" %}
[floor.md](floor.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
