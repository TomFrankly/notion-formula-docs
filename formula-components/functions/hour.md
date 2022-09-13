---
description: Learn how to use the hour function in Notion formulas.
---

# hour

The `hour()` function returns an integer ([number](../../formula-basics/data-types/number.md)) between `0` and `23` that corresponds to the hour of its [date](../../formula-basics/data-types/date-data-type.md) argument.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
hour(date)
```
{% endcode %}

`hour()` (and its sibling functions [minute](minute.md), [day](day.md), [date](date.md), [month](month.md), and [year](year.md)) is useful for manipulating dates within Notion formulas.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
hour(now()) // Output: 11 (When current time was 11:25 AM)

// Assume a propety called Date with a current date of June 24, 2022 11:29 AM
hour(prop("Date")) // Output: 11
```
{% endcode %}

`hour()` can be used with other functions such as [dateSubtract](datesubtract.md) to change the value of a date, like so:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume the value of now() is June 24, 2022 11:34 AM
dateSubtract(now(), hour(now()), "hours")
// Output: June 24, 2022 12:34 AM
```
{% endcode %}

You can take this concept even further to “hard-code” any date into a Notion formula. See the section on [Hard-Coding Dates into Formulas](now.md#use-now-to-hard-code-a-specific-date-in-a-notion-formula) within the [now](now.md) article for more on how to do this.

## Example Database

This example database groups events in a Renaissance Faire by their time of day - Morning, Afternoon, and Evening. These three options are returned by the Time of Day formula property.

<figure><img src="../../.gitbook/assets/Hour Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/hour-3b9108f7a368431a84e686827e47ece5" %}

### "Time of Day" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(hour(prop("Date")) >= 18, "🌔 Evening", if(hour(prop("Date")) >= 12, "🌤 Afternoon", "🌄 Morning"))

// Expanded
if(
    hour(
        prop("Date")
    ) >= 18,
    "🌔 Evening",
    if(
        hour(
            prop("Date")
        ) >= 12,
        "🌤 Afternoon",
        "🌄 Morning"
    )
)
```
{% endcode %}

Here, we use a nested if statement to first check if the `hour()` value of the Date property is [greater than or equal to](../operators/largereq.md) 18 (which is 6:00 PM in 12-hour time).

If yes, the formula returns "🌔 Evening".

If not, we then check if the `hour()` value is greater than or equal to 12 (noon in 12-hour time).

If yes, the formula returns "🌤 Afternoon". If no, it returns "🌄 Morning".

From there, we can set the database view to Group by the output of this formula property:

<figure><img src="../../.gitbook/assets/Group by Formula Output in Notion.png" alt=""><figcaption></figcaption></figure>

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="../operators/largereq.md" %}
[largereq.md](../operators/largereq.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
