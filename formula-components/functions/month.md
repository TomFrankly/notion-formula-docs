---
description: Learn how to use the month function in Notion formulas.
---

# month

The `month()` function returns an integer ([number](../../formula-basics/data-types/number.md)) between `0` and `11` that corresponds to the month of its [date](../../formula-basics/data-types/date-data-type.md) argument.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
month(date)
```
{% endcode %}

`month()` (and its sibling functions [minute](date.md), [hour](hour.md), [day](day.md), [date](date.md), and [year](year.md)) is useful for manipulating dates within Notion formulas.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
month(now()) // Output: 5 (when now() = June 24, 2022)

// Assume a propety called Date with a current date of Jan 1, 2022
month(prop("Date")) // Output: 0
```
{% endcode %}

`month()` can be used with other functions such as [dateSubtract](datesubtract.md) to change the value of a date, like so:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume the value of now() is June 24, 2022
dateSubtract(now(), month(now()), "months") 
// Output: January 24, 2022
```
{% endcode %}

You can take this concept even further to “hard-code” any date into a Notion formula. See the section on [Hard-Coding Dates into Formulas](now.md#use-now-to-hard-code-a-specific-date-in-a-notion-formula) within the [now](now.md) article for more on how to do this.

## Example Database

The example database below determines each person’s next birthday based on their Birth Date, as well as the current date.

<figure><img src="../../.gitbook/assets/Month Function - Notion Formulas.png" alt=""><figcaption><p>Screenshot taken Sept 1, 2022.</p></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/month-5dc0a4f7f0bf4a8588c47bda80cb0e0a" %}

### "Next Birthday" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
dateAdd(prop("Birth Date"), year(now()) - year(prop("Birth Date")) + if(month(prop("Birth Date")) == month(now()) and date(prop("Birth Date")) >= date(now()) or month(prop("Birth Date")) > month(now()), 0, 1), "years")

// Expanded
dateAdd(
    prop("Birth Date"),
    year(
        now()
    ) - 
    year(
        prop("Birth Date")
    ) + 
    if(
        month(
            prop("Birth Date")
        ) == month(
            now()
        ) and date(
            prop("Birth Date")
        ) >= date(
            now()
        ) or month(
            prop("Birth Date")
        ) > month(
            now()
        ),
        0,
        1
    ),
    "years"
)
```
{% endcode %}

Here's the logic behind this formula:

* Start with the birth year.
* Add a number of years to it using [dateAdd](dateadd.md), determined by the year output of now minus the birth year itself (E.g. 2022 - 1991 = 31).
* Determine if the person's birthday has already happened this year. If not, add one more year (since we're determining their _next_ birthday).

To check whether or not the person's birthday has already happened, we use an [if statement](../operators/if.md) and multiple comparisons using [comparison operators](../operators/#comparison-operators). If one of the following is true:

* The current month and the birth month are equal AND the current day of the month (determined with [date](date.md)) is equal to or later than the birth date's day of the month
* OR the birth month is later than the current month

...then this indicates that the person's birthday has NOT yet happened this year. Therefore, we add 0 to the count.

Otherwise, we add 1 to the count.

{% hint style="info" %}
**Good to know:** The [or](../operators/or.md) operator has a lower [operator precedence](../../reference/operator-precedence-and-associativity.md) than the [and](../operators/and.md) operator, meaning that any "and" comparisons will be executed before the first "or" comparison.
{% endhint %}

#### Other formula components used in this example:

{% content-ref url="dateadd.md" %}
[dateadd.md](dateadd.md)
{% endcontent-ref %}

{% content-ref url="date.md" %}
[date.md](date.md)
{% endcontent-ref %}

{% content-ref url="now.md" %}
[now.md](now.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

{% content-ref url="../operators/subtract.md" %}
[subtract.md](../operators/subtract.md)
{% endcontent-ref %}

{% content-ref url="../operators/equal.md" %}
[equal.md](../operators/equal.md)
{% endcontent-ref %}

{% content-ref url="../operators/largereq.md" %}
[largereq.md](../operators/largereq.md)
{% endcontent-ref %}

{% content-ref url="../operators/larger.md" %}
[larger.md](../operators/larger.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
