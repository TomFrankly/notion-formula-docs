---
description: Learn about the Date data type in Notion formulas.
---

# Date (Data Type)

Notion formulas can work with and output **date objects,** which are a special [data type](./).&#x20;

They're different than [strings](string.md), as they can be manipulated with date functions such as [dateAdd](../../formula-components/functions/dateadd.md) and [dateSubtract](../../formula-components/functions/datesubtract.md).

Underneath the hood, Notion's date object consists of three parts:

* Start date
* End date (optional)
* Time zone

You can learn more about how dates are formatted under the hood at the Notion API's property value reference for dates:

{% embed url="https://developers.notion.com/reference/property-value-object#date-property-values" %}

The following Notion property types output (or can output) date objects:

* Date
* Created time
* Edited time
* Rollup (if set to rollup a property outputting a date object, and not set to "show original")
* Formula (if the formula is outputting a date object)

Within a Notion formula, the following [functions](../../formula-components/functions/) output date objects:

| Function                                                             | Example                          | Output                    |
| -------------------------------------------------------------------- | -------------------------------- | ------------------------- |
| [start](../../formula-components/functions/start.md)                 | `start(prop("Date"))`            | August 18, 2022           |
| [end](../../formula-components/functions/end.md)                     | `end(prop("Date"))`              | August 25, 2022           |
| [now](../../formula-components/functions/now.md)                     | `now()`                          | August 18, 2022 2:10 PM   |
| [fromTimestamp](../../formula-components/functions/fromtimestamp.md) | `fromTimestamp(1656012840000)`   | June 23, 2022 1:34 PM     |
| [dateAdd](../../formula-components/functions/dateadd.md)             | `dateAdd(now(),3,"months")`      | November 18, 2022 2:11 PM |
| [dateSubtract](../../formula-components/functions/datesubtract.md)   | `dateSubtract(now(),3,"months")` | May 18, 2022 2:11 PM      |

{% hint style="info" %}
**Good to know:** Notion Formula properties cannot **return** date ranges (i.e. a date object containing both a start and end date). They are only able to output a singular date.

Date properties can output date ranges, as can Rollup properties - though Rollups can only output a range consisting of _start dates_ of multiple rows. Rollups cannot access end dates directly from Date properties.

_A consequence of the Rollup limitation: While this is outside the scope of Notion formulas, I'll mention that it is currently impossible for a Rollup to return a date range for multiple rows that consists of the earliest start date and latest end date._
{% endhint %}

## Time Zones and Dates in Notion

Notion sets it time zone automatically based on the system's time zone.

Depending on the property and/or formula function that is outputting the date object, you can get different results.

The diagram below shows the same Notion database viewed from two different time zones (this was accomplished by setting my system time to a different time zone, then refreshing the page). You can also [view the diagram full-screen on Whimsical](https://whimsical.com/dates-in-notion-YPiVW833k4cWWnNJ8oj7hQ).

{% embed url="https://whimsical.com/dates-in-notion-YPiVW833k4cWWnNJ8oj7hQ" %}

Date properties with set times _always_ display those times in the time zone in which they were set.&#x20;

If you don't specify a time zone manually, then the time zone won't show for you when you're in that time zone; however, users in other time zones will see the time zone displayed along with the date.

Note how the second row does not display `(MDT)` at first. When the system time zone is changed, that row now displays `(MDT)`, and the set time (8:00am) is not changed to reflect the system's new time zone.

This behavior is reflected in the **Date (Formula)** property, which simply referenced the Date property: `prop("Date")`.

However, things are different when dates are derived from a timestamp. The date objects created from the [fromTimestamp](../../formula-components/functions/fromtimestamp.md) function - as well as the [now](../../formula-components/functions/now.md) function - are _always_ displayed in the local time zone's time. In these instances, this behavior cannot be changed, and an alternate time zone cannot be specified.

## A Note about formatDate()

It's important to note that the [formatDate](../../formula-components/functions/formatdate.md) function takes a date object as its main argument and outputs a [string](string.md) value.

For this reason, you cannot pass the output of `formatDate()` to date functions such as [dateAdd](../../formula-components/functions/dateadd.md).

It is also very difficult to perform date comparisons using the output of `formatDate()`. While equality comparisons work well:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
formatDate(now(), "MMM DD YYYY") == formatDate(prop("Date"), "MMM DD YYYY")
```
{% endcode %}

...it is much more difficult to perform "earlier than" or "later than" comparisons.

Therefore, it is recommended to use functions such as [timestamp](../../formula-components/functions/timestamp.md), [date](../../formula-components/functions/date.md), [month](../../formula-components/functions/month.md), [year](../../formula-components/functions/year.md), etc. to make these kinds of comparisons.

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
