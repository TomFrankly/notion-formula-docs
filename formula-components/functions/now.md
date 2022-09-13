---
description: Learn how to use the now function in Notion formulas.
---

# now

The `now()` function returns the current date and time in your local timezone. `now()` accepts no arguments.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
now()
```
{% endcode %}

Notion sets your timezone automatically using your system/OS timezone.

now() and [fromTimestamp](fromtimestamp.md) are the only functions that will allow you to add a true [date object](../../formula-basics/data-types/date-data-type.md) into a formula without pulling from a Date property. To "hard-code" other dates into a formula, use the methods described below.

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
now() // Output: June 23, 2022 12:30 PM (at time of writing)
```
{% endcode %}

### Get the Current Date Without the Time

Use the following formula to remove the current time from `now()`:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
dateSubtract(dateSubtract(now(), minute(now()), "minutes"), hour(now()), "hours")
```
{% endcode %}

Here’s why you might want to do this:

When doing date math operations (e.g. [dateAdd](dateadd.md)/[dateSubtract](datesubtract.md)) in Notion, `now()` can cause problems due to its inclusion of the current time.

Take this formula as an example:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume Date's current value is June 30, and now() is June 23
dateBetween(prop("Date"), now(), "weeks")
```
{% endcode %}

If it’s currently June 23, and the value of the Date property is June 30, then this formula should return `1`. June 30 is 7 days out from June 23, hence one week.

However, this formula will actually return `0` because the values that are implicitly being compared are `June 23, 2022 1:35 PM` and `June 30, 2022 12:00 AM`.

As a result, the gap between the two dates is not 7 _full_ days.

In Notion, dates without times given a default (and normally hidden) time of `00:00`, aka `12:00 AM`.

However, the `now()` function _always_ includes the time. There’s no argument that allows you to customize its output so that it only returns the date.

To do that, you need to use the formula shown at the top of this section: `dateSubtract(dateSubtract(now(), minute(now()), "minutes"), hour(now()), "hours")`.

This uses the [dateSubtract](datesubtract.md) function to subtract `now()`'s current [minute](minute.md) and [hour](hour.md) values from `now()` itself, resulting in a [date object](../../formula-basics/data-types/date-data-type.md) that contains the current date with a time of `00:00`.

### Use now() to “Hard-Code” a Specific Date in a Notion Formula

If you want to hard-code a specific date into a Notion formula (i.e. June 4, 2022 12:00 AM MDT), the primary method you’d use to do that would be the [fromTimestamp](fromtimestamp.md) function.

However, fromTimestamp is mainly used to get an _exact_ date. What if you want to hard-code a date that repeats every year, such as **June 4**?

You can use the `now()` function to do that with the following formula:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
dateAdd(dateAdd(dateSubtract(dateSubtract(dateSubtract(dateSubtract(now(), minute(now()), "minutes"), hour(now()), "hours"), date(now()) - 1, "days"), month(now()), "months"), 5, "months"), 3, "days")

// Expanded
dateAdd(
    dateAdd(
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
        5, 
        "months"
    ), 
    3, 
    "days"
)
```
{% endcode %}

This formula works by first using [dateSubtract](datesubtract.md) several times to get a date object set at the first date of the year, `January 1, 12:00 AM`.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
dateSubtract(dateSubtract(dateSubtract(dateSubtract(now(), minute(now()), "minutes"), hour(now()), "hours"),date(now())-1,"days"),month(now()),"months")

// Expanded
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
)
```
{% endcode %}

Next, we use two instances of [dateAdd](dateadd.md) to add the correct number of months and days to January 1:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// "January 1" is used here to represent the previous dateSubtract() chain
// from the code block above. This code will not actually
// work in Notion's formula editor.
dateAdd(dateAdd(January 1,5,"months"),3,"days")
```
{% endcode %}

## Example Database

The example database below shows how you can “hard-code” dates into a Notion formula using the `now()` function along with [dateAdd](dateadd.md) and [dateSubtract](datesubtract.md). The Date property outputs a date that matches the choices set in the Month and Day properties.

<figure><img src="../../.gitbook/assets/Now Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/now-b5aa81037fee4aa8a5ed862614003476" %}

### "Date" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
dateAdd(dateAdd(dateSubtract(dateSubtract(dateSubtract(dateSubtract(now(), minute(now()), "minutes"), hour(now()), "hours"), date(now()) - 1, "days"), month(now()), "months"), toNumber(replace(replace(replace(replace(replace(replace(replace(replace(replace(replace(replace(replace(prop("Month"),"January","0"),"February","1"),"March","2"),"April","3"),"May","4"),"June","5"),"July","6"),"August","7"),"September","8"),"October","9"),"November","10"),"December","11")), "months"), prop("Day")-1, "days")

// Expanded
dateAdd(
    dateAdd(
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
)
```
{% endcode %}

This example builds on the "hard-code" examples shown above.

Instead of hard-coding a specific date, the formula allows user input via a Select property (Month) and a Number property (Day). This allows the user to select their own specific date, which is still not tied to any particular year. The chosen month/day date will always contain the current year.

To set the month, the [replace](replace.md) function is used (many times) to replace the chosen month's text string with its corresponding [month](month.md) value (0-11). This replacement number is then turned into an actual number via the [toNumber](tonumber.md) function.

#### Other formula components used in this example:

{% content-ref url="replace.md" %}
[replace.md](replace.md)
{% endcontent-ref %}

{% content-ref url="tonumber.md" %}
[tonumber.md](tonumber.md)
{% endcontent-ref %}

{% content-ref url="dateadd.md" %}
[dateadd.md](dateadd.md)
{% endcontent-ref %}

{% content-ref url="datesubtract.md" %}
[datesubtract.md](datesubtract.md)
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

{% content-ref url="../operators/subtract.md" %}
[subtract.md](../operators/subtract.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
