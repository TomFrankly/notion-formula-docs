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

The example database below uses the `timestamp()` function to determine which of two dates is the later one.

<figure><img src="../../.gitbook/assets/Timestamp Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/timestamp-e5d3c683ee8641e18478f5a7c6b3ddf9" %}

### "Later Date" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(timestamp(prop("Date 1")) == timestamp(prop("Date 2")),"Date 1 and Date 2 are the same.",if(timestamp(prop("Date 1")) > timestamp(prop("Date 2")),"Date 1 is later than Date 2.","Date 2 is later than Date 1."))

// Expanded
if(
    timestamp(
        prop("Date 1")
    ) == timestamp(
        prop("Date 2")
    ),
    "Date 1 and Date 2 are the same.",
    if(
        timestamp(
            prop("Date 1")
        ) > timestamp(
            prop("Date 2")
        ),
        "Date 1 is later than Date 2.",
        "Date 2 is later than Date 1."
    )
)
```
{% endcode %}

This formula uses a [nested if-statement](../operators/if.md#nested-if-then-statements) to first check if the timestamp values of the two dates are [equal](../operators/equal.md). If they are, the formula returns, "Date 1 and Date 2 are the same."

If not, the next block checks to see if Date 1's timestamp is [larger](../operators/larger.md) than Date 2's timestamp.

Depending on the result of this comparison, the formula will return, "Date 1 is later than Date 2," or "Date 2 is later than Date 1."

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="../operators/equal.md" %}
[equal.md](../operators/equal.md)
{% endcontent-ref %}

{% content-ref url="../operators/larger.md" %}
[larger.md](../operators/larger.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
