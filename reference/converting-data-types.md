---
description: Learn how to convert data to another type in a Notion formula.
---

# Converting Data Types

Notion formulas can only return data of a single type. For reference, Notion formulas work with four distinct [data types](../formula-basics/data-types/):

* [String](../formula-basics/data-types/string.md)
* [Number](../formula-basics/data-types/number.md)
* [Boolean (Checkbox)](../formula-basics/data-types/boolean-checkbox.md)
* [Date](../formula-basics/data-types/date-data-type.md)

Additionally, you can only compare data that share the same type when you use comparison operators such as [equal](../formula-components/operators/equal.md), [and](../formula-components/operators/and.md), or [larger](../formula-components/operators/larger.md) (and some require a specific data type).

Therefore, you'll often need to convert data from one type to another in order to get your formula to work.

Here are all the methods you can use to convert data to another type.

## Converting Strings

To numbers:

| Function/Method                                                 | Example          |
| --------------------------------------------------------------- | ---------------- |
| [toNumber](../formula-components/functions/tonumber.md)         | `toNumber("42")` |
| [unaryPlus](../formula-components/operators/unaryplus.md) (`+`) | `+"42"`          |

To Booleans:

| Function/Method                             | Example                                   |
| ------------------------------------------- | ----------------------------------------- |
| [if](../formula-components/operators/if.md) | `if(prop("Text") == "true", true, false)` |

{% hint style="info" %}
**Good to know:** You can't truly _convert_ strings, numbers, or dates to Boolean values. What you can do is write a simple statement that outputs a Boolean true/false value using your starting piece of data as criteria.
{% endhint %}

## Converting Numbers

To strings:

| Function/Method                                     | Example      |
| --------------------------------------------------- | ------------ |
| [format](../formula-components/functions/format.md) | `format(42)` |

To Booleans:

| Function/Method                             | Example                              |
| ------------------------------------------- | ------------------------------------ |
| [if](../formula-components/operators/if.md) | `if(prop("Num") == 42, true, false)` |

To dates:

| Function/Method                                                   | Example                      |
| ----------------------------------------------------------------- | ---------------------------- |
| [fromTimestamp](../formula-components/functions/fromtimestamp.md) | `fromTimestamp(prop("Num"))` |

_Note: fromTimestamp only works if its argument is a valid Unix timestamp._

{% hint style="info" %}
**Good to know:** [replace](../formula-components/functions/replace.md), [replaceAll](../formula-components/functions/replaceall.md), and [test](../formula-components/functions/test.md) are able to automatically convert [numbers](../formula-basics/data-types/number.md) and [Booleans](../formula-basics/data-types/boolean-checkbox.md) (but not [dates](../formula-basics/data-types/date-data-type.md)) to strings. Manual [type conversion](converting-data-types.md) is not needed.
{% endhint %}

## Converting Booleans

To strings:

| Function/Method                                     | Example        |
| --------------------------------------------------- | -------------- |
| [format](../formula-components/functions/format.md) | `format(true)` |

To numbers:

| Function/Method                                                 | Example          |
| --------------------------------------------------------------- | ---------------- |
| [toNumber](../formula-components/functions/tonumber.md)         | `toNumber(true)` |
| [unaryPlus](../formula-components/operators/unaryplus.md) (`+`) | `+true`          |

## Converting Dates

To strings:

| Function/Method                                             | Example                            |
| ----------------------------------------------------------- | ---------------------------------- |
| [format](../formula-components/functions/format.md)         | `format(now())`                    |
| [formatDate](../formula-components/functions/formatdate.md) | `formatDate(now(), "MMM DD YYYY")` |

To numbers:

| Function/Method                                           | Example            |
| --------------------------------------------------------- | ------------------ |
| [timestamp](../formula-components/functions/timestamp.md) | `timestamp(now())` |
| [toNumber](../formula-components/functions/tonumber.md)   | `toNumber(now())`  |
| [minute](../formula-components/functions/minute.md)       | `minute(now())`    |
| [hour](../formula-components/functions/hour.md)           | `hour(now())`      |
| [day](../formula-components/functions/day.md)             | `day(now())`       |
| [date](../formula-components/functions/date.md)           | `date(now())`      |
| [month](../formula-components/functions/month.md)         | `month(now())`     |
| [year](../formula-components/functions/year.md)           | `year(now())`      |

{% hint style="info" %}
**Good to know:** The [toNumber](../formula-components/functions/tonumber.md) function converts dates to their Unix timestamp, just like the [timestamp](../formula-components/functions/timestamp.md) function.
{% endhint %}

To Booleans:

| Function/Method                             | Example                                  |
| ------------------------------------------- | ---------------------------------------- |
| [if](../formula-components/operators/if.md) | `if(prop("Date") == now(), true, false)` |

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
