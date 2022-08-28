---
description: Learn how to use the round function in Notion formulas.
---

# round

The `round()` function rounds its argument to the nearest integer (whole number).

The exact midpoint between two whole numbers will round up towards positive infinity, not “away from zero”.

For example: `round(-4.5)` will round up to `4`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
round(4.5) // Output: 5

round(4.49) // Output: 4

round(-4.49) // Output: -4

round(-4.5) // Output: -4

round(-4.51) // Output: -5
```
{% endcode %}

## Rounding to Specific Decimal Places

The `round()` function doesn’t accept additional arguments, so it can’t natively round a number to a specific decimal place.

However, you can accomplish this using the following formula:

```jsx
// Round to two decimal places
round([number]*100)/100

// Round to three decimal places
round([number]*1000)/1000
```

The number of zeroes corresponds to the number of decimal places to which your number will be rounded.

```jsx
round(9.24551*10)/10 // Output: 9.2

round(4.158015*100)/100 // Output: 4.16

round(5145.018394*10000)/10000 // Output: 5145.0184
```

## Example Database

The example database below contains a formula that rounds the input number to several different decimal places.

<figure><img src="../../.gitbook/assets/Round Funtion - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/round-22cb0304a2214e35b287c214279fd792" %}

### “Rounded” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
"One Decimal: " + format(round(prop("Number") * 10) / 10) + "\n Two Decimals: " + format(round(prop("Number") * 100) / 100) + "\n Three Decimals: " + format(round(prop("Number") * 1000) / 1000) + "\n Four Decimals: " + format(round(prop("Number") * 10000) / 10000) + "\n Five Decimals: " + format(round(prop("Number") * 100000) / 100000)

// Expanded
"One Decimal: " + format(round(prop("Number") * 10) / 10) + 
"\n Two Decimals: " + format(round(prop("Number") * 100) / 100) + 
"\n Three Decimals: " + format(round(prop("Number") * 1000) / 1000) + 
"\n Four Decimals: " + format(round(prop("Number") * 10000) / 10000) + 
"\n Five Decimals: " + format(round(prop("Number") * 100000) / 100000)
```
{% endcode %}

This formula demonstrates decimal-rounding to five different places.

Each rounded number is then converted to a [string](../../formula-basics/data-types/string.md) using the [format](format.md) function, allowing us to craft a five-line block of text.

Note how `\n` allows us to create a new line in the formula output.

#### Other formula components used in this example:

{% content-ref url="format.md" %}
[format.md](format.md)
{% endcontent-ref %}

{% content-ref url="../operators/multiply.md" %}
[multiply.md](../operators/multiply.md)
{% endcontent-ref %}

{% content-ref url="../operators/divide.md" %}
[divide.md](../operators/divide.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
