---
description: Learn how to use the dateAdd function in Notion formulas.
---

# dateAdd

The `dateAdd()` function accepts a [date](../../formula-basics/data-types/date-data-type.md) argument and adds to it, returning a new date. It requires three arguments in the following order:

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
dateAdd(prop("Date"),3,"months") // Output: September 1, 2022

dateAdd(prop("Date"),5,"days") // Output: June 6, 2022
```
{% endcode %}

You can nest multiple `dateAdd()` functions to add multiple different types of units to a date:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a property called "Date" with a current row value
// of June 1, 2022
dateAdd(dateAdd(prop("Date"),3,"months"),5,"days") 
// Output: September 6, 2022
```
{% endcode %}

`dateAdd()` accepts negative values:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a property called "Date" with a current row value
// of June 1, 2022
dateAdd(prop("Date"), -3, "months") // Output: March 1, 2022
```
{% endcode %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
