---
description: Learn how to use the dateBetween function in Notion formulas.
---

# dateBetween

The `dateBetween()` function returns the amount of time between two [dates](../../formula-basics/data-types/date-data-type.md), based on a specified unit of time.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
dateBetween(date, date, string [from unit list])
```
{% endcode %}

The function returns a [number](../../formula-basics/data-types/number.md), and requires three arguments in the following order:

* Date 1 (must be a [date](../../formula-basics/data-types/date-data-type.md) data type)
* Date 2 (must be a date data type)
* A unit

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

`dateBetween()` returns a positive number when the first date is _later_ than the second date.

{% hint style="info" %}
**Good to know:** You can use the [abs](abs.md) function to ensure the output is always positive.
{% endhint %}

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume now() == June 23, 2022 and Date == June 1, 2022
dateBetween(now(),prop("Date"),"days") // Output: 22

// Assume now() == June 23, 2022 and Date == June 30, 2022
dateBetween(now(),prop("Date"),"days") // Output: -6

// Assume now() == June 23, 2022 and Date == December 25, 2022
dateBetween(now(),prop("Date"),"months") // Output: -6
```
{% endcode %}

## Example Database

This example database uses the Birth Date property to determine the age of each person. Additional logic is included to deal with plurality (”year” vs “years”), and to express infant age in months.

<figure><img src="../../.gitbook/assets/dateBetween Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/dateBetween-9078429567644f1b81c183fd6f7aa116" %}

### "Age" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
dateBetween(now(), prop("Birth Date"), "years")
```
{% endcode %}

### "Age (Pretty)" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
prop("Name") + " is " + if(dateBetween(now(), prop("Birth Date"), "years") < 1, format(dateBetween(now(), prop("Birth Date"), "months")) + if(dateBetween(now(), prop("Birth Date"), "months") == 1, " month old.", " months old."), format(dateBetween(now(), prop("Birth Date"), "years")) + if(dateBetween(now(), prop("Birth Date"), "years") == 1, " year old.", " years old."))

// Expanded
prop("Name") + " is " + 
if(
    dateBetween(
        now(),
        prop("Birth Date"),
        "years"
    ) < 1,
    format(
        dateBetween(
            now(),
            prop("Birth Date"),
            "months"
        )
    ) + if(
        dateBetween(
            now(),
            prop("Birth Date"),
            "months"
        ) == 1,
        " month old.",
        " months old."
    ),
    format(
        dateBetween(
            now(),
            prop("Birth Date"),
            "years"
        )
    ) + if(
        dateBetween(
            now(),
            prop("Birth Date"),
            "years"
        ) == 1,
        " year old.",
        " years old."
    )
)
```
{% endcode %}

Here, we create a "pretty" sentence that states the person's name along with their age.

A nested if-statement is used to determine whether the age meets certain criteria. Depending on the result, the formula will return different ending strings:

* If the person is less than 1 year old, the ending output will be "months old" or "month old" depending on the number of months.
* If the person is exactly 1 year old, the ending output will be "year old."
* Otherwise, the ending output will be "years old".

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

{% content-ref url="../operators/smaller.md" %}
[smaller.md](../operators/smaller.md)
{% endcontent-ref %}

{% content-ref url="../operators/equal.md" %}
[equal.md](../operators/equal.md)
{% endcontent-ref %}

{% content-ref url="format.md" %}
[format.md](format.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
