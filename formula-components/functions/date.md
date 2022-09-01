---
description: Learn how to use the date function in Notion formulas.
---

# date

The `date()` function returns an integer ([number](../../formula-basics/data-types/number.md)) between `1` and `31` that corresponds to the day of the month of its [date](../../formula-basics/data-types/date-data-type.md) argument.

`date()` (and its sibling functions [minute](minute.md), [hour](hour.md), [day](day.md), [month](month.md), and [year](year.md)) is useful for manipulating dates within Notion formulas.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
date(now()) // Output: 24 (when now() = June 24, 2022)

// Assume a propety called Date with a current date of June 1, 2022 11:29 AM
date(prop("Date")) // Output: 1
```
{% endcode %}

`date()` can be used with other functions such as [dateSubtract](datesubtract.md) to change the value of a date.

Here, it is used with dateSubtract and [now](now.md) to return a date at the start of the month.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume the value of now() is June 24, 2022
dateSubtract(now(),date(now())-1,"days")
// Output: June 1, 2022
```
{% endcode %}

Note that since the lowest integer value of `date()` is `1`, I have to use `date(now())-1` to get the first day of the month.

You can take this concept even further to “hard-code” any date into a Notion formula. See the section on [Hard-Coding Dates into Formulas](now.md#use-now-to-hard-code-a-specific-date-in-a-notion-formula) within the [now](now.md) article for more on how to do this.

## Example Database

This example database takes a date from the Date property and returns both the first and last day of the month that contains that date.

<figure><img src="../../.gitbook/assets/Date Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/date-51aca1ed0b8c4851ba9d7115fd2effe3" %}

### "First Day of Month" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
dateSubtract(prop("Date"), date(prop("Date")) - 1, "days")

// Expanded
dateSubtract(
    prop("Date"),
    date(
        prop("Date")
    ) - 1,
    "days"
)
```
{% endcode %}

### “Last Day of Month” Property

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
dateSubtract(dateAdd(prop("Date"), 1, "months"), date(prop("Date")), "days")

// Expanded
dateSubtract(
    dateAdd(
        prop("Date"),
        1,
        "months"
    ),
    date(
        prop("Date")
    ),
    "days"
)
```
{% endcode %}

#### Other formula components used in this example:

{% content-ref url="datesubtract.md" %}
[datesubtract.md](datesubtract.md)
{% endcontent-ref %}

{% content-ref url="dateadd.md" %}
[dateadd.md](dateadd.md)
{% endcontent-ref %}

{% content-ref url="../operators/subtract.md" %}
[subtract.md](../operators/subtract.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
