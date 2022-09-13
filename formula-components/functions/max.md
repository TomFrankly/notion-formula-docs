---
description: Learn how to use the max function in Notion formulas.
---

# max

The `max()` function returns the greatest of one or more [numbers](../../formula-basics/data-types/number.md). `max()` accepts only numbers or properties that output numbers (it will not auto-convert [Booleans](../../formula-basics/data-types/boolean-checkbox.md)).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
max(number)
max(number, number)
max(number, number, ...)
```
{% endcode %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
max(3,5,4) // Output: 5

// Assume prop("Num") contains 20
max(prop("Num"),13,5) // Output: 20

// Other data types must be converted to number
max(1,+true,+"3",9) // Output: 9
// Here, the + operator (unaryPlus) is used to convert
//  true and "3" to numbers.
```
{% endcode %}

{% hint style="info" %}
**Good to know:** `max()` and [min](min.md) are useful for finding maximum and minimum values across multiple _properties._ They're not useful for finding max/min values across multiple database _rows_.

For that, you'll want to associate the rows to another common row via a [Relation](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#relations), then use a [Rollup](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#rollups) to calculate the max value among them. [Here's a small example database](https://thomasfrank.notion.site/391af1e362a64f1e9778e6ec9474d304?v=d2a830fdf69044afbb3ca73b8c5d95b7).

This approach still has limitations, but since Notion hasn't provided a true query language for its database feature, it's the best we can currently do (unless you create an external tool via the [official API](https://developers.notion.com/)).
{% endhint %}

## Example Database

The example database below contains quarterly sales data for a fictional company. The **Max** property displays the dollar amount from the best quarter, while the **Best Quarter** property displays which quarter had the best performance.

![](<../../.gitbook/assets/Max Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/max-0788452dc2e64251840a84c46542eca6" %}

### “Max” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
max(prop("Q1"), prop("Q2"), prop("Q3"), prop("Q4"))
```
{% endcode %}

`max()` accepts numbers or number properties.

Here, we simply pass each quarter’s property to the `max()` function in order to find the maximum quarterly sales value.

### “Best Quarter” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(prop("Q1") == prop("Max"),"Q1",if(prop("Q2") == prop("Max"),"Q2",if(prop("Q3") == prop("Max"),"Q3","Q4")))

// Expanded
if(
    prop("Q1") == prop("Max"),
    "Q1",
    if(
        prop("Q2") == prop("Max"),
        "Q2",
        if(
            prop("Q3") == prop("Max"),
            "Q3",
            "Q4"
        )
    )
)
```
{% endcode %}

Here’s an example of how we can make `max()` more useful.

Using a [nested if statement](../operators/if.md#nested-if-then-statements), we compare the numeric value of each quarter property to that of the **Max** property.

If a quarter’s value matches that of the Max property, we output that quarter’s name.

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
