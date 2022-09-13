---
description: Learn how to use the min function in Notion formulas.
---

# min

The `min()` function returns the smallest of one or more [numbers](../../formula-basics/data-types/number.md). `min()` accepts only numbers or properties that output numbers (it will not auto-convert [Booleans](../../formula-basics/data-types/boolean-checkbox.md)).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
min(number)
min(number, number)
min(number, number, ...)
```
{% endcode %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
min(4,1,9,-3) // Output: -3

// Assume prop("Num") contains 3
max(prop("Num"),13,5) // Output: 3

// Other data types must be converted to number
min(3,8,+false) // Output: 0
// Here, the + operator (unaryPlus) is used to convert
// false to a number (0)
```
{% endcode %}

{% hint style="info" %}
**Good to know:** `min()` and [max](max.md) are useful for finding maximum and minimum values across multiple _properties._ They're not useful for finding max/min values across multiple database _rows_.

For that, you'll want to associate the rows to another common row via a [Relation](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#relations), then use a [Rollup](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#rollups) to calculate the max value among them. [Here's a small example database](https://thomasfrank.notion.site/391af1e362a64f1e9778e6ec9474d304?v=d2a830fdf69044afbb3ca73b8c5d95b7).

This approach still has limitations, but since Notion hasn't provided a true query language for its database feature, it's the best we can currently do (unless you create an external tool via the [official API](https://developers.notion.com/)).
{% endhint %}

## Example Database

The example database below contains quarterly sales data for a fictional company. The **Min** property displays the dollar amount from the worst quarter, while the **Worst Quarter** property displays which quarter had the worst performance.

![](<../../.gitbook/assets/Min Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/min-815db718ffad4e36898763f5d32a4cbc" %}

### “Min” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
min(prop("Q1"), prop("Q2"), prop("Q3"), prop("Q4"))
```
{% endcode %}

`min()` accepts numbers or number properties.

Here, we simply pass each quarter’s property to the `min()` function in order to find the minimum quarterly sales value.

### “Worst Quarter” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(prop("Q1") == prop("Min"), "Q1", if(prop("Q2") == prop("Min"), "Q2", if(prop("Q3") == prop("Min"), "Q3", "Q4")))

// Expanded
if(
    prop("Q1") == prop("Min"),
    "Q1",
    if(
        prop("Q2") == prop("Min"),
        "Q2",
        if(
            prop("Q3") == prop("Min"),
            "Q3",
            "Q4"
        )
    )
)
```
{% endcode %}

Here’s an example of how we can make `min()` more useful.

Using a [nested if statement](../operators/if.md#nested-if-then-statements), we compare the numeric value of each quarter property to that of the **Min** property.

If a quarter’s value matches that of the Min property, we output that quarter’s name.

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
