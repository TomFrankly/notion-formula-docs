---
description: Learn how to use the day function in Notion formulas.
---

# day

The `day()` function returns an integer ([number](../../formula-basics/data-types/number.md)) between `0` and `6` that corresponds to the day of the week of its [date](../../formula-basics/data-types/date-data-type.md) argument:

* `0` = Sunday
* `1` = Monday
* `2` = Tuesday
* `3` = Wednesdy
* `4` = Thursday
* `5` = Friday
* `6` = Saturday

`day()` (and its sibling functions [minute](minute.md), [hour](hour.md), [date](date.md), [month](month.md), and [year](year.md)) is useful for manipulating dates within Notion formulas.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
day(now()) // Output: 5 (when now() = June 24, 2022)

// Assume a propety called Date with a current date of June 1, 2022
day(prop("Date")) // Output: 3
```
{% endcode %}

`day()` can be used with other functions such as [dateSubtract](datesubtract.md) to change the value of a date.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume the value of now() is June 24, 2022 (Friday)
dateSubtract(now(), day(now()), "days")
// Output: June 19, 2022 (Sunday)
```
{% endcode %}

You can take this concept even further to “hard-code” any date into a Notion formula. See the section on [Hard-Coding Dates into Formulas](now.md#use-now-to-hard-code-a-specific-date-in-a-notion-formula) within the [now](now.md) article for more on how to do this.

Additionally, `day()` in particular is useful for determining weekdays and weekends:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Outputs, "It's the weekend!" if now()'s day is Saturday (6) or Sunday (0)
day(now()) == 0 or day(now()) == 6 ? "It's the weekend!" : "It's a weekday."

// This can also be accomplished like so:
test(format(day(now())),"[06]") ? "It's the weekend!" : "It's a weekday."
```
{% endcode %}

## Example Database

This example database finds the number of weekend days between two dates. If the starting and/or ending date is a weekend day, it is included in the count.

<figure><img src="../../.gitbook/assets/Day Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/day-23ddaef5e0964616b2c77186b16d8995" %}

### "Weekend Days" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
floor((prop("Days Between") + day(prop("Date 1"))) / 7) * 2 + if(day(prop("Date 1")) == 0, 1, 0) - if(day(prop("Date 2")) == 6, 1, 0)

// Expanded
floor(
    (
        prop("Days Between") + day(
            prop("Date 1")
        )
    ) / 7
) * 2 + if(
    day(
        prop("Date 1")
    ) == 0, 
    1, 
    0
) - if(
    day(
        prop("Date 2")
    ) == 6, 
    1, 
    0
)
```
{% endcode %}

Let's first cover the **logic** behind this formula:

First, we get the number of weekend days between our two dates, ignoring half-weekends. A half-weekend in the count occurs if:

* Date 1 (Start date) is Sunday
* Date 2 (End date) is Saturday

Then, to account for half-weekends, we run the following checks:

* If Date 1 is Sunday, we add 1.
* If Date 2 is Saturday, we subtract 1.

Now let's talk about the **formula**.

To get the first count, which only counts full weekends, we find the number of days between Date 1 and Date 2 (stored in the Days Between property), and add to it the `day()` integer returned from Date 1.

We divide that number by 7, then remove the trailing decimals by passing it through the [floor](floor.md) function. We then multiply by 2, since there are two days per weekend:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
floor(
    (
        prop("Days Between") + day(
            prop("Date 1")
        )
    ) / 7
) * 2
```
{% endcode %}

{% hint style="info" %}
Note the use of **parentheses** here, which ensures the operations are carried out in the order we've specified above. To fully understand order of operations in Notion formulas, check out the [operator precedence](../../reference/operator-precedence-and-associativity.md) page.
{% endhint %}

Next, we check if Date 1 is Sunday, and if so, add 1:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
if(day(prop("Date 1")) == 0, 1, 0)
```
{% endcode %}

Finally, we check if Date 1 is Saturday, and if so, subtract 1:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
if(day(prop("Date 2")) == 6, 1, 0)
```
{% endcode %}

_Credit is due to IBM; I found the solution to this problem in their documentation for their Cognos Business Intellience Platform:_

{% embed url="https://www.ibm.com/support/pages/calculate-number-weekdays-between-two-dates" %}

#### Other formula components used in this example:

{% content-ref url="floor.md" %}
[floor.md](floor.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

{% content-ref url="../operators/divide.md" %}
[divide.md](../operators/divide.md)
{% endcontent-ref %}

{% content-ref url="../operators/multiply.md" %}
[multiply.md](../operators/multiply.md)
{% endcontent-ref %}

{% content-ref url="../operators/equal.md" %}
[equal.md](../operators/equal.md)
{% endcontent-ref %}

{% content-ref url="../operators/subtract.md" %}
[subtract.md](../operators/subtract.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
