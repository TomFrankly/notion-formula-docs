---
description: Learn how to group Notion database views by formula output.
---

# Grouping Database Views by Formulas

It is possible to **group** a database view by a formula property in Notion.

If you'd like to learn the basics of database grouping, check out this section in my database guide:

{% embed url="https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#grouping" %}

When grouping a view by a formula property, the [data type](../formula-basics/data-types/) of the formula's **return value (i.e the output)** determines your grouping options.&#x20;

Notion formulas can output one of four different data types:

| Data Type                                                                               | Examples                 |   |
| --------------------------------------------------------------------------------------- | ------------------------ | - |
| [String](../formula-basics/data-types/string.md)                                        | `"King of the Pirates"`  |   |
| [Number](../formula-basics/data-types/number.md)                                        | `9001`                   |   |
| [Boolean](../formula-basics/data-types/boolean-checkbox.md) (called Checkbox in Notion) | `true`, `false`          |   |
| [Date](../formula-basics/data-types/date-data-type.md)                                  | `"2022-11-11T12:00:00Z"` |   |

When your formula outputs a string value, you'll have the following grouping options:

* Exact Name
* Alphabetical (using the first letter of the output)

With number output, grouping is done by number ranges. The following options will be available:

* Group Range (e.g. 0 - 1,000,000)
* Group Every - a.k.a. the interval (e.g. 0 - 99,999, 100,000 - 199,999...)

When the formula returns a date, the following options will be available:

* Relative
* Day
* Week
* Month
* Year

Finally, when the formula returns a Boolean/Checkbox value, your view will be grouped by row that are checked vs. unchecked (no additional options are available).

## Example Database

This example database contains four separate views; each one is grouped by a formula property that returns data of a different type - string, number, date, and Boolean/Checkbox.

<figure><img src="../.gitbook/assets/Group Notion Database Views by Formula Property.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/Grouping-Database-Views-by-Formula-Values-aa02adce677445e0bb3f1dc000d5d8a0" %}

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
