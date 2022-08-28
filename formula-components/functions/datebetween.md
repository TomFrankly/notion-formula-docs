---
description: Learn how to use the dateBetween function in Notion formulas.
---

# dateBetween

The `dateBetween()` function returns the amount of time between two [dates](../../formula-basics/data-types/date-data-type.md), based on a specified unit of time. The function returns a [number](../../formula-basics/data-types/number.md), and requires three arguments in the following order:

* Date 1 (must be a [date](../../formula-basics/data-types/date-data-type.md) data type)
* Date 2 (must be a date data type)
* A unit

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

`dateBetween()` returns a positive number when the first date is _later_ than the second date.

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume now() == June 23, 2022 and Date == June 1, 2022
dateBetween(now(),prop("Date"),"days") // Output: 22

// Assume now() == June 23, 2022 and Date == June 30, 2022
dateBetween(now(),prop("Date"),"days") // Output: -6

// Assume now() == June 23, 2022 and Date == December 25, 2022
dateBetween(now(),prop("Date"),"months") // Output: -6
```
{% endcode %}

## Example Database



### View and Duplicate Database



### Property Formula



#### Other formula components used in this example:



#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
