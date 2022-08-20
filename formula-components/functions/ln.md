---
description: Learn how to use the ln function in Notion formulas.
---

# ln

The `ln()` function returns the natural logarithm of a [number](../../formula-basics/data-types/number.md).

The natural logarithm is $$\log_e$$, where $$e$$ is [Euler’s Constant](../constants/e.md) (approximately `2.718281828459045`).

For reference, here are the named components of a logarithm:

$$
\log_{base} argument = exponent
$$

A **logarithm** is the exponent of the base that returns the argument.

Learn more about the natural logarithm:

{% embed url="https://betterexplained.com/articles/demystifying-the-natural-logarithm-ln/" %}

<details>

<summary>A Mathematical Example</summary>

In plain English, $$log_e$$ helps us find out **how many periods (i.e. how long) of continuous growth are needed** for a starting value to reach a target end value.

$$e$$ denotes a continuous rate of growth.

Recall from the article on [Euler’s Constant (e)](../constants/e.md), that we can find a starting population’s end number with the following formula:

$$n * e^x$$

…where $$n$$ is our starting population, and $$x$$ is the number of periods.

Let’s say we start out with a population of 1,000, which grows continuously for three years ([you can check this answer on WolframAlpha](https://www.wolframalpha.com/input?i=1000+\*+e%5E%283%29)):

$$1000 * e^3 = 20,085$$

At the end of three years, our final population is 20,085.

If you want to fully understand why this works, I highly recommend [this guide on exponential functions](https://betterexplained.com/articles/an-intuitive-guide-to-exponential-functions-e/).

Now let’s look at $$log_e$$.

Where $$e^x$$ tells us how much growth we’ll experience given a number of periods, $$log_ex$$ tells us how many periods it’ll take to get a specific end result $$x$$.

Here’s the natural logarithm of our earlier result. We’ll take the full result, 20,085, and divide it by the starting population of 1,000 ([Check this on WolframAlpha](https://www.wolframalpha.com/input?i=ln%2820085%2F1000%29)):

$$log_e(20,085/1000) = log_e(20.085) =  3$$

We can now see that $$log_ex$$ is the inverse of $$e^x$$. Therefore, these two are roughly equivalent (20,085 is rounded from the actual result of the first equation):

$$log_e(20.085) = e^3$$

This also means:

$$log_ee^3 = 3$$

Hopefully this aside has helped to demystify $$log_e$$ a bit for you!

</details>

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
ln(20) // Output: 2.995732273554

ln(e) // Output: 1
```
{% endcode %}

## Example Database

This example database calculates the calculates the **number of years** needed for a starting population to reach a target end number given a specific **growth rate**.

![](<../../.gitbook/assets/Ln Function - Notion Formulas (1).png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/c4244f553795406399f11c492ef62d4b?v=7fc508aa92ed432690efbf24f9a74a7b" %}

### “Years Needed” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
round(ln(prop("Target Num") / prop("Starting Num")) / prop("Growth Rate") * 100) / 100

// Expanded
round(
    ln(
        prop("Target Num") / 
        prop("Starting Num")
    ) / 
    prop("Growth Rate") 
    * 100
) / 100
```
{% endcode %}

The first part of this formula replicates the mathematical example in the toggle block above.

First, we find the natural logarithm of the quotient of the **Target Num** and the **Starting Num:**

$$
log_e(Target Num/Starting Num)
$$

This is done with the following code: `ln(prop("Target Num") / prop("Starting Num"))`

Next, we divide this result by the **Growth Rate.**

Finally, the result is passed through the [round](round.md) function, and we use the following trick to round it to two decimal places: `round(result * 100)/100`

#### Other formula components used in this example:

{% content-ref url="round.md" %}
[round.md](round.md)
{% endcontent-ref %}

{% content-ref url="../operators/multiply.md" %}
[multiply.md](../operators/multiply.md)
{% endcontent-ref %}

{% content-ref url="../operators/divide.md" %}
[divide.md](../operators/divide.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
