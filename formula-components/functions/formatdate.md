---
description: Learn how to use the formatDate function in Notion formulas.
---

# formatDate

The `formatDate()` function formats a [date](../../formula-basics/data-types/date-data-type.md) as a [string](../../formula-basics/data-types/string.md) using the Moment standard time format.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
formatDate(date, string [must conform to Moment format])
```
{% endcode %}

It accepts two arguments in the following order:

1. A [date](../../formula-basics/data-types/date-data-type.md) (can be passed via properties - Date, Created Time, Last Edited Time - or via date functions such as [now](now.md), [fromTimestamp](fromtimestamp.md), [dateAdd](dateadd.md), [dateSubtract](datesubtract.md))
2. A [string](../../formula-basics/data-types/string.md) specifying the Moment formatting for the date output

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
formatDate(now(), "MMMM DD YYYY") // Output: June 24 2022

formatDate(now(), "dddd, MMMM DD, YYYY hh:mm A zz") 
// Output: Friday, June 24, 2022 10:45 AM MDT
```
{% endcode %}

You can also use brackets (`[]`) to escape any characters that you’d like to render explicitly (i.e. not use a Moment formatting commands):

{% code overflow="wrap" lineNumbers="true" %}
```jsx
formatDate(now(), "[Month of] MMMM, YYYY") // Output: Month of June, 2022
```
{% endcode %}

`formatDate()` uses Moment.js to do date formatting. By specifying the formatting options you want within the function’s second argument, you can customize your date format.

Refer to the Moment.js documentation so see all possible formatting options:

{% embed url="https://momentjscom.readthedocs.io/en/latest/moment/04-displaying/01-format/" %}

### Limitations

`formatDate()` returns a [string](../../formula-basics/data-types/string.md), not a [date](../../formula-basics/data-types/date-data-type.md). Therefore, it is not possible to do date math on its output.

{% hint style="info" %}
**Good to Remember:** Notion formulas are picky about [data types](../../formula-basics/data-types/). The formula editor will almost never do automatic [type conversion](../../reference/converting-data-types.md), so you must pass the correct data types when you use functions.
{% endhint %}

For example, you cannot use [dateAdd](dateadd.md) or [dateSubtract](datesubtract.md) on the output of `formatDate()`:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// ERROR: Type mismatch formatDate(now(), "MMMM DD YYYY") is not a Date.
dateAdd(formatDate(now(),"MMMM DD YYYY"),4,"months")
```
{% endcode %}

It is also very difficult to perform date comparisons using the output of `formatDate()`. While equality comparisons work well:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
formatDate(now(), "MMM DD YYYY") == formatDate(prop("Date"), "MMM DD YYYY")
```
{% endcode %}

...it is much more difficult to perform "earlier than" or "later than" comparisons.

Therefore, it is recommended to use functions such as [timestamp](timestamp.md), [date](date.md), [month](month.md), [year](year.md), etc. to make these kinds of comparisons.

It is also not possible to create date-based [filters](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#filters) in a database view using a formula property that outputs a date string via `formatDate()`.

However, it is possible to work with the output of `formatDate()` using the [Notion API](https://developers.notion.com/).

For an example, see this recurring tasks tutorial that uses [Make.com](http://make.com) and the Notion API to parse the output of `formatDate()`:

{% embed url="https://thomasjfrank.com/notion-automated-recurring-tasks/#automated-recurring-tasks-with-makecom" %}

## Example Database

This example database shows the numbered week of year that matches the date in the Date property. `formatDate()` uses Moment.js for date formatting.

<figure><img src="../../.gitbook/assets/formatDate - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/formatDate-b98249fbe11040e19fd07e3faa4cea26" %}

### “Week” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
formatDate(prop("Date"), "wo")
```
{% endcode %}

### “Detailed Format” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
formatDate(prop("Date"), "dddd, MMMM Do, YYYY, HH:mm A, wo [week of the year]")
```
{% endcode %}

The Detailed Format property demonstrates many of the available formatting options. To see all formatting options, [visit the Moment.js reference](https://momentjscom.readthedocs.io/en/latest/moment/04-displaying/01-format/).

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
