---
description: Learn how to use the end function in Notion formulas.
---

# end

The `end()` function returns the end date from a date range. It accepts a single [date](../../formula-basics/data-types/date-data-type.md) argument.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
end(date)
```
{% endcode %}

`end()` is useful for obtaining the end date from a Date property which contains a date range.

When you pass a single date as the argument - i.e. from a Created Time/Last Edited Time property, or a timestamp - `end()` simply returns that date.

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a property "Date" exists, with 
// a row value of June 23, 2022 → June 27, 2022
end(prop("Date")) // Outpuut: June 27, 2022
```
{% endcode %}

### Date Math within start() and end()

It’s useful to note that date math functions like [dateAdd](dateadd.md) and [dateSubtract](datesubtract.md) return a date object that does not contain a date range - even if their argument does include one.

When these functions are passed a date object that includes a range, they only use a start date.

For this reason, the following two formulas will return the exact same date:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a property "Date" exists, with 
// a row value of June 23, 2022 → June 27, 2022
start(dateAdd(prop("Date"),30,"days")) // Output: July 23, 2022

end(dateAdd(prop("Date"),30,"days")) // Output: July 23, 2022
```
{% endcode %}

Therefore, you must use the `end()` function _within_ your date math function if you wish to operate on the end date in a date range:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a property "Date" exists, with 
// a row value of June 23, 2022 → June 27, 2022
dateAdd(end(prop("Date")), 30, "days") // Output: July 27, 2022
```
{% endcode %}

## Example Database

The example database below contains several events that are happening over multiple days. The **Date Range** property displays their start and end dates, while the **Current State** formula property determines whether the event has passed, is currently ongoing, or is still in the future.

Finally, both the **Table** and **Board** views of the database are grouped by the **Current State** formula’s three possible outputs.

<figure><img src="../../.gitbook/assets/End Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/end-c08d74b22d294a44802e7b0434bc45fd" %}

### "Current State" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(dateBetween(start(prop("Date Range")),now(),"days") > 0,"Future Events",if(dateBetween(end(prop("Date Range")),now(),"days") >= 0,"Currently Active","Past Events"))

// Expanded
if(
    dateBetween(
        start(
            prop("Date Range")
        ),
        now(),
        "days"
    ) > 0,
    "Future Events",
    if(
        dateBetween(
            end(
                prop("Date Range")
            ),
            now(),
            "days"
        ) >= 0,
        "Currently Active",
        "Past Events"
    )
)
```
{% endcode %}

This formula uses a [nested if-statement](../operators/if.md#nested-if-then-statements) and [dateBetween](datebetween.md) to first check if the current date (determined with the [now](now.md) function) is before the start of the event's date range.

If it is not, the next level of the if-statement checks to see if the current date is before the end date of the date range (determined with `end()`).

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="datebetween.md" %}
[datebetween.md](datebetween.md)
{% endcontent-ref %}

{% content-ref url="start.md" %}
[start.md](start.md)
{% endcontent-ref %}

{% content-ref url="../operators/largereq.md" %}
[largereq.md](../operators/largereq.md)
{% endcontent-ref %}

{% content-ref url="../operators/larger.md" %}
[larger.md](../operators/larger.md)
{% endcontent-ref %}

{% content-ref url="now.md" %}
[now.md](now.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
