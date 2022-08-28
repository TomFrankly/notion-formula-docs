---
description: Learn how to use the fromTimestamp function in Notion formulas.
---

# fromTimestamp

The `fromTimestamp()` function converts a Unix timestamp into a [date](../../formula-basics/data-types/date-data-type.md).

The Unix timestamp is the number of seconds since January 1, 1970 at 00:00 UTC. It is also known as Unix time or Epoch time.

Note that Notion’s formula editor specifically looks for a Unix **millisecond** timestamp.

This is important to remember, because `fromTimestamp(1656012840)` returns `January 20, 1970 4:00 AM` in Notion (in UTC - it’ll look different based on your timezone).

Unix timestamps are _normally_ expressed in **seconds,** so most epoch converters would express `1656012840` as `June 23, 2022 7:34 PM`.

In Notion, you’d need to write `fromTimestamp(1656012840000)` to get the same date.

You can use this tool to convert human-readable dates to timestamps, and vice-versa:

{% embed url="https://www.epochconverter.com/" %}

Learn more about Unix time:

{% embed url="https://www.howtogeek.com/759337/what-is-the-unix-epoch-and-how-does-unix-time-work/" %}

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
fromTimestamp(1656012840000) // Output: June 23, 2022 7:34 PM (UTC)
```
{% endcode %}

## Example Database



### View and Duplicate Database



### Property Formula



#### Other formula components used in this example:



#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
