---
description: Learn how to use the dateSubtract function in Notion formulas.
---

# dateSubtract

The `dateSubtract()` function accepts a [date](../../formula-basics/data-types/date-data-type.md) argument and subtracts from it, returning a new date. It requires three arguments in the following order:

1. A [date](../../formula-basics/data-types/date-data-type.md) (must be an actual date data type)
2. A [number](../../formula-basics/data-types/number.md)
3. A unit

Accepted units include:

* “years”
* “quarters”
* “months”
* “weeks”
* “days”
* “hours”
* “minutes”
* “seconds”
* “milliseconds”

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a property called "Date" with a current row value
// of June 1, 2022
dateSubtract(prop("Date"),3,"months") // Output: March 1, 2022

dateSubtract(prop("Date"),5,"days") // Output: May 27, 2022
```
{% endcode %}

You can nest multiple `dateSubtract()` functions to subtract multiple different types of units from a date:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a property called "Date" with a current row value
// of June 1, 2022
dateSubtract(dateSubtract(prop("Date"),3,"months"),5,"days") 
// Output: February 24, 2022
```
{% endcode %}

`dateSubtract()` accepts negative values:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a property called "Date" with a current row value
// of June 1, 2022
dateSubtract(prop("Date"), -3, "months") // Output: September 1, 2022
```
{% endcode %}

## Example Database

This example database demonstrates how to output a date object set to January 1, 12:00 AM in the current year, in your current time zone.

<figure><img src="../../.gitbook/assets/dateSubtract - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/dateSubtract-281fc3d6cee940ab93a32abc5e01f227" %}

### "Jan 1" Property Formula

<pre class="language-jsx" data-overflow="wrap" data-line-numbers><code class="lang-jsx"><strong>// Compressed
</strong>dateSubtract(dateSubtract(dateSubtract(dateSubtract(now(), minute(now()), "minutes"), hour(now()), "hours"), date(now()) - 1, "days"), month(now()), "months")

// Expanded
dateSubtract(
    dateSubtract(
        dateSubtract(
            dateSubtract(
                now(), 
                minute(
                    now()
                ), 
                "minutes"
            ), 
            hour(
                now()
            ), 
            "hours"
        ), 
        date(
            now()
        ) - 1, 
        "days"
    ), 
    month(
        now()
    ), 
    "months"
)</code></pre>

This formula uses multiple instances of `dateSubtract()` to remove different units of time from the output of the [now](now.md) function in order to arrive at Jan 1, 12:00 AM.

The amount of time that is subtracted from `now()` is actually derived from `now()` itself. For example:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
dateSubtract(
    now(), 
    minute(
        now()
    ), 
    "minutes"
)
```
{% endcode %}

Here, `minute(now())` gets the [minute](minute.md) value from `now()`.

So, if it's currently 3:12 PM, this essentially says:

> Subtract 12 minutes from 3:12 PM.

The resulting output would be 3:00 PM.

The formula then takes this output and does the same thing using [hour](hour.md), [date](date.md), and [month](month.md).

The only caveat is that `1` must be substracted from the output of `date()`, since there is no "January 0".

#### Other formula components used in this example:

{% content-ref url="now.md" %}
[now.md](now.md)
{% endcontent-ref %}

{% content-ref url="minute.md" %}
[minute.md](minute.md)
{% endcontent-ref %}

{% content-ref url="hour.md" %}
[hour.md](hour.md)
{% endcontent-ref %}

{% content-ref url="../../formula-basics/create-a-formula-property.md" %}
[create-a-formula-property.md](../../formula-basics/create-a-formula-property.md)
{% endcontent-ref %}

{% content-ref url="month.md" %}
[month.md](month.md)
{% endcontent-ref %}

{% content-ref url="../operators/subtract.md" %}
[subtract.md](../operators/subtract.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
