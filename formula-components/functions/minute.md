---
description: Learn how to use the minute function in Notion formulas.
---

# minute

The `minute()` function returns an integer ([number](../../formula-basics/data-types/number.md)) between `0` and `59` that corresponds to the minute of its [date](../../formula-basics/data-types/date-data-type.md) argument.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
minute(date)
```
{% endcode %}

`minute()` (and its sibling functions [hour](hour.md), [day](day.md), [date](date.md), [month](month.md), and [year](year.md)) is useful for manipulating dates within Notion formulas.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
minute(now()) // Output: 25 (When current time was 11:25 AM)

// Assume a propety called Date with a current date of June 24, 2022 11:29 AM
minute(prop("Date")) // Output: 29
```
{% endcode %}

`minute()` can be used with other functions such as [dateSubtract](datesubtract.md) to change the value of a date, like so:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume the value of now() is June 24, 2022 11:34 AM
dateSubtract(now(), minute(now()), "minutes") 
// Output: June 24, 2022 11:00 AM
```
{% endcode %}

You can take this concept even further to “hard-code” any date into a Notion formula. See the section on [Hard-Coding Dates into Formulas](now.md#use-now-to-hard-code-a-specific-date-in-a-notion-formula) within the [now](now.md) article for more on how to do this.

## Example Database

This example database shows both the current time (using the [now](now.md) function), as well as the current time rounded to the nearest hour.

<figure><img src="../../.gitbook/assets/Minute Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/minute-ef5884e0a9c64500bb6684bdecb04c91" %}

### "Nearest Hour" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(minute(now()) < 30, dateSubtract(now(), minute(now()), "minutes"), dateAdd(now(), 60 - minute(now()), "minutes"))

// Expanded
if(
    minute(
        now()
    ) < 30,
    dateSubtract(
        now(),
        minute(
            now()
        ),
        "minutes"
    ),
    dateAdd(
        now(),
        60 - minute(
            now()
        ),
        "minutes"
    )
)
```
{% endcode %}

First, an [if statement](../operators/if.md) checks if the minute value of [now](now.md) is less than 30.

If so, we subtract `now()`'s minute value from `now()` in order to get to the current hour.

If not, we add `now()`'s minute value to `now()` in order to get to the _next_ hour.

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="now.md" %}
[now.md](now.md)
{% endcontent-ref %}

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
