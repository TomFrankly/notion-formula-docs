---
description: Learn how to use the timestamp function in Notion formulas.
---

# timestamp

The `timestamp()` function converts a [date](../../formula-basics/data-types/date-data-type.md) argument into its corresponding Unix timestamp (also known as Unix Time or Epoch Time), which is a [number](../../formula-basics/data-types/number.md).

The Unix timestamp is the number of seconds since January 1, 1970 at 00:00 UTC.

Notion’s `timestamp()` function specifically outputs a **millisecond** timestamp.

You can use this site to convert human-readable dates to Unix timestamps, or vice-versa:

{% embed url="https://www.epochconverter.com/" %}

{% hint style="info" %}
**Good to know:** Since Notion returns a _millisecond_ timestamp, pasting the timestamp for very early dates (e.g. January 8, 1970) can cause conversion tools like the website above to return an incorrect date.

To account for this, remove the final three zeroes (000) from Notion’s timestamp before pasting into a conversion tool.
{% endhint %}

Learn more about Unix time:

{% embed url="https://www.howtogeek.com/759337/what-is-the-unix-epoch-and-how-does-unix-time-work/" %}

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
timestamp(now()) // Output: 1656012120000 (will change with the value of now()
```
{% endcode %}

## Example Database



### View and Duplicate Database



### Property Formula



#### Other formula components used in this example:



#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
