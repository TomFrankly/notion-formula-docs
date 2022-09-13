---
description: Learn how to use the cbrt function in Notion formulas.
---

# cbrt

The `cbrt()` function returns the cube root of its argument. `cbrt()` accepts only [numbers](../../formula-basics/data-types/number.md).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
cbrt(number)
```
{% endcode %}

The argument is $$a$$ where:

$$
\sqrt[3]{a}
$$

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
cbrt(8) // Output: 2

cbrt(64) // Output: 4

// Total surface area of cube with Volume 300m³
// using formula 6a², where a = edge length
6 * cbrt(300)^2 // Output: 268.88428479343

```
{% endcode %}

## Example Database

The example database below calculates several properties of a cube given a specific **volume.**

![](<../../.gitbook/assets/Cube Root cbrt Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/cbrt-2e40d661145947c4a677ac4e5faafd47" %}

### Formula Explanations

```jsx
// Side Length
format(round(cbrt(prop("Volume (m³)")) * 100) / 100) + "m"

// Side Area
format(round(100 * cbrt(prop("Volume (m³)")) ^ 2) / 100) + "m²"

// LSA (Lateral Surface Area - 4 sides)
format(round(4 * cbrt(prop("Volume (m³)")) ^ 2 * 100) / 100) + "m²"

// TSA (Total Surface Area - all 6 sides)
format(round(6 * cbrt(prop("Volume (m³)")) ^ 2 * 100) / 100) + "m²"

// Face Diagonal Length
format(round(cbrt(prop("Volume (m³)")) * sqrt(2) * 100) / 100) + "m"

// Solid Diagonal Length
format(round(cbrt(prop("Volume (m³)")) * sqrt(3) * 100) / 100) + "m"
```

Each formula in this example contains the mathematical formula for its intended operation.

Next, the operation is run through the [round](round.md) function. We multiply within `round()` and then divide by 100 in order to round to two decimal places: `round(n*100)/100`

Finally, we apply the [format](format.md) function to turn the [number](../../formula-basics/data-types/number.md) into a [string](../../formula-basics/data-types/string.md), allowing us to combine it with its unit of measurement.

#### Other formula components used in this example:

{% content-ref url="round.md" %}
[round.md](round.md)
{% endcontent-ref %}

{% content-ref url="format.md" %}
[format.md](format.md)
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
