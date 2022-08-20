---
description: Learn how to use the mathematical constant pi in Notion formulas.
---

# pi

The mathematical constant _pi_ ($$π$$) equals (roughly) `3.1415926559`.

$$π$$ is the **ratio between the circumference and diameter of a circle.** This ratio is shared by _all_ circles, no matter the size.

$$π$$ can be used to calculate the circumference and area of a circle, volume and surface area of a sphere, and more.

You can learn more about $$π$$ here:

{% embed url="https://betterexplained.com/articles/prehistoric-calculus-discovering-pi/" %}

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
pi * 10
```
{% endcode %}

The above formula will calculate the circumference of a circle with a **diameter** of 10cm. It uses the simple equation $$πd$$, where $$d$$ is the diameter of the circle.

In this case, the circumference would be approximately $$31.4159265cm$$.

## Example Database

In this example database, the **Formula (num)** property calculates the area of a circle with a given radius, set in the **Circle Radius (cm)** property.

![](<../../.gitbook/assets/area of a circle.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/c8925e4115304b7391c937b2ccc7f77e?v=af44e83960a644d7bbf466ee6d59739d" %}

### "Formula (Num)" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
pi * prop("Circle Radius (cm)") ^ 2
```
{% endcode %}

The formula to calculate the area inside a circle is $$πr^2$$. We can create this equation in a Notion formula using the code above:

* `pi` is the Notion constant for $$π$$
* `prop("Circle Radius (cm)")` uses the `prop()` function to pull in the value of the `Circle Radius (cm)` Number property
* `^ 2` squares the radius of the circle

**Other formula components used in this example:**

{% content-ref url="../operators/multiply.md" %}
[multiply.md](../operators/multiply.md)
{% endcontent-ref %}

{% content-ref url="../operators/pow.md" %}
[pow.md](../operators/pow.md)
{% endcontent-ref %}

### "Pretty Formula" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
format(round(prop("Formula (num)") * 100) / 100) + "cm²"
```
{% endcode %}

This formula:

1. Intakes the output of the previous formula
2. Rounds it to the nearest hundredth (i.e. two decimal places)
3. Converts the resulting number to a String
4. Appends “cm²”

Note that Notion formulas do not support text formatting, so I’m using the actual `²` symbol. You can find this symbol here:

{% embed url="https://fsymbols.com/signs/square/" %}

To round the decimal to two decimal places, I use the following trick:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
round(prop("Formula (num)")*100)/100
```
{% endcode %}

Notion’s built-in `round()` function only rounds numbers to the nearest whole integer. But this trick will output a rounded number to two decimals places instead. Learn more about this trick:

{% content-ref url="../../formula-examples/round-numbers-to-specific-decimal-places.md" %}
[round-numbers-to-specific-decimal-places.md](../../formula-examples/round-numbers-to-specific-decimal-places.md)
{% endcontent-ref %}

**Other formula components used in this example:**

{% content-ref url="../operators/multiply.md" %}
[multiply.md](../operators/multiply.md)
{% endcontent-ref %}

{% content-ref url="../operators/divide.md" %}
[divide.md](../operators/divide.md)
{% endcontent-ref %}

{% content-ref url="../functions/round.md" %}
[round.md](../functions/round.md)
{% endcontent-ref %}

{% content-ref url="../functions/format.md" %}
[format.md](../functions/format.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
