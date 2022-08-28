---
description: Learn how to use the year function in Notion formulas.
---

# year

The `year()` function returns an integer ([number](../../formula-basics/data-types/number.md)) that corresponds to the year of its [date](../../formula-basics/data-types/date-data-type.md) argument.

`year()` (and its sibling functions [minute](minute.md), [hour](hour.md), [day](day.md), [date](date.md), and [month](month.md)) is useful for manipulating dates within Notion formulas.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
year(now()) // Output: 2022 (When now() = June 24, 2022)

// Assume a propety called Date with a current date of June 24, 2022
year(prop("Date")) // Output: 2022
```
{% endcode %}

`year()` can be used with other functions such as [dateSubtract](datesubtract.md) to change the value of a date, like so:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume the value of now() is June 24, 2022
dateSubtract(now(), 10, "years")
// Output: June 24, 2012
```
{% endcode %}

You can take this concept even further to “hard-code” any date into a Notion formula. See the section on [Hard-Coding Dates into Formulas](now.md#use-now-to-hard-code-a-specific-date-in-a-notion-formula) within the [now](now.md) article for more on how to do this.

## Example Database



### View and Duplicate Database



### Property Formula



#### Other formula components used in this example:



#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
