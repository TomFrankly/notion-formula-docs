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



### View and Duplicate Database



### Property Formula



#### Other formula components used in this example:



#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
