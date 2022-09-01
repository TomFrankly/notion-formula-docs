---
description: Learn how to use the exp function in Notion formulas.
---

# exp

The `exp()` function allows you to raise [Euler’s Constant](../constants/e.md) $$e$$ (the base of the natural logarithm) to a higher power and get the output, where the argument is the exponent:

$$
e^n = m
$$

$$e$$ approximately equals `2.718281828459045`.

{% hint style="info" %}
**Good to know:** `exp(n)` is equivalent to `e^n`. See [e (Constant)](../constants/e.md) for more.
{% endhint %}

Viewed another way, the `exp()` function helps you find the _argument_ (mathematical term) in a natural logarithm.

In other words, `exp()` accepts $$x$$ as an argument (programming term) and returns $$y$$, where:

$$
\log_e y = x
$$

For reference, here are the named components of a logarithm:

$$
\log_{base} argument = exponent
$$

Learn more about natural logarithms here:

{% embed url="https://betterexplained.com/articles/demystifying-the-natural-logarithm-ln/" %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
exp(2) // Output: 7.389056098931

exp(5) // Output: 148.413159102577
e^5 // Output: 148.413159102577

exp(ln(5)) // Output: 5
ln(exp(5)) // Output 5
```
{% endcode %}

## Example Database

Using `exp()`, we can write a Notion formula that models continuous growth of a starting population by a certain percentage each year over a certain number of years.

This example is also used in the article on [Euler’s Constant (e)](../constants/e.md); its use here demonstrates how `exp(n)` is equivalent to `e^n`.

![](<../../.gitbook/assets/Exp Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/exp-fc9e90520d054e15a4c8d47c8531d3af" %}

### “End Num” Property Formula

```jsx
// Compressed
prop("Starting Num") * exp(prop("Growth Rate") * prop("Periods"))

// Expanded
prop("Starting Num") * 
exp(
    prop("Growth Rate") * 
    prop("Periods")
)
```

As stated in the Euler’s Constant (e) article, continuous growth of a starting number $$n$$ can be expressed as:

$$
n * e^{(rate \ of \ growth \ * \ number \ of \ time \ periods)}
$$

Here, we simply use the `exp()` function, passing `prop("Growth Rate") * prop("Periods")` as the argument.&#x20;

We then multiply it by our starting number, passed via `prop("Starting Num")`.

#### Other formula components used in this example:

{% content-ref url="../operators/multiply.md" %}
[multiply.md](../operators/multiply.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
