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

The [now](now.md) formula example shows how to “hard-code” a date into a Notion formula without a specific year. The example database below does the same thing, except it allows you to specify a year using a Number property.

<figure><img src="../../.gitbook/assets/Year Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/year-1125c7ee0d7a42dfa5e5ebe0a0222e35" %}

### "Date" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
dateAdd(dateAdd(dateAdd(dateSubtract(dateSubtract(dateSubtract(dateSubtract(dateSubtract(now(), minute(now()), "minutes"), hour(now()), "hours"), date(now()) - 1, "days"), month(now()), "months"), year(now()), "years"), toNumber(replace(replace(replace(replace(replace(replace(replace(replace(replace(replace(replace(replace(prop("Month"), "January", "0"), "February", "1"), "March", "2"), "April", "3"), "May", "4"), "June", "5"), "July", "6"), "August", "7"), "September", "8"), "October", "9"), "November", "10"), "December", "11")), "months"), prop("Day") - 1, "days"), prop("Year"), "years")

// Expanded
dateAdd(
    dateAdd(
        dateAdd(
            dateSubtract(
                dateSubtract(
                    dateSubtract(
                        dateSubtract(
                            dateSubtract(
                                now(), 
                                minute(
                                    now()
                                ), 
                                "minutes"
                            ), 
                            hour(
                                now()
                            ), 
                            "hours"
                        ), 
                        date(
                            now()
                        ) - 1, 
                        "days"
                    ), 
                    month(
                        now()
                    ), 
                    "months"
                ),
                year(
                    now()
                ),
                "years"
            ), 
            toNumber(
                replace(
                    replace(
                        replace(
                            replace(
                                replace(
                                    replace(
                                        replace(
                                            replace(
                                                replace(
                                                    replace(
                                                        replace(
                                                            replace(
                                                                prop("Month"),
                                                                "January",
                                                                "0"
                                                            ),
                                                            "February",
                                                            "1"
                                                        ),
                                                        "March",
                                                        "2"
                                                    ),
                                                    "April",
                                                    "3"
                                                ),
                                                "May",
                                                "4"
                                            ),
                                            "June",
                                            "5"
                                        ),
                                        "July",
                                        "6"
                                    ),
                                    "August",
                                    "7"
                                ),
                                "September",
                                "8"
                            ),
                            "October",
                            "9"
                        ),
                        "November",
                        "10"
                    ),
                    "December",
                    "11"
                )
            ), 
            "months"
        ), 
        prop("Day")-1, 
        "days"
    ),
    prop("Year"),
    "years"
)
```
{% endcode %}

This formula works the same way as the formula in the [now](now.md#date-property-formula) article, except we're now adding one extra instance of [dateAdd](dateadd.md) and [dateSubtract](datesubtract.md). These final instances:

* Use `year()` to take the current year and set it to 0.
* Then add the specified year in the Year property.

#### Other formula components used in this example:

{% content-ref url="dateadd.md" %}
[dateadd.md](dateadd.md)
{% endcontent-ref %}

{% content-ref url="datesubtract.md" %}
[datesubtract.md](datesubtract.md)
{% endcontent-ref %}

{% content-ref url="../operators/subtract.md" %}
[subtract.md](../operators/subtract.md)
{% endcontent-ref %}

{% content-ref url="replace.md" %}
[replace.md](replace.md)
{% endcontent-ref %}

{% content-ref url="tonumber.md" %}
[tonumber.md](tonumber.md)
{% endcontent-ref %}

{% content-ref url="now.md" %}
[now.md](now.md)
{% endcontent-ref %}

{% content-ref url="minute.md" %}
[minute.md](minute.md)
{% endcontent-ref %}

{% content-ref url="hour.md" %}
[hour.md](hour.md)
{% endcontent-ref %}

{% content-ref url="date.md" %}
[date.md](date.md)
{% endcontent-ref %}

{% content-ref url="month.md" %}
[month.md](month.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
