---
description: Learn how to convert data to another type in a Notion formula.
---

# Converting Data Types

Notion formulas can only return data of a single type. Additionally, you can only compare data that share the same type when you use comparison operators such as [equal](../formula-components/operators/equal.md), [and](../formula-components/operators/and.md), or [larger](../formula-components/operators/larger.md) (and some require a specific data type).

Therefore, you'll often need to convert data from one type to another in order to get your formula to work.

Here are all the methods you can use to convert data to another type.

## Converting Strings

To numbers:

* toNumber
* unaryPlus

To Booleans:

* if

To dates:

* To a timestamp value first, then fromTimestamp (research needed)

## Converting Numbers

To strings:

* format()

## Converting Booleans

To strings:

* format()

To numbers:

* unaryPlus
* toNumber

## Converting Dates

To strings:

* format
* formatDate

To numbers:

* timestamp

To Booleans:

* if

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
