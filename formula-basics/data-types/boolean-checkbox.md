---
description: Learn about the Boolean (Checkbox) data type in Notion formulas.
---

# Boolean (Checkbox)

Boolean values represent **truth states:** either [true](../../formula-components/constants/true.md) or [false](../../formula-components/constants/false.md).

Notion represents Boolean values as **checkboxes:**

* True is represented by a **checked** box
* False is represented by an **unchecked** box

<details>

<summary>Learn more about Booleans</summary>

These resources aren’t necessary for understanding how to work with Booleans in Notion, but you may find them interesting if you want to dive deeper into how Booleans are used in programming and computer science.

* [Crash Course - Boolean Logic & Logic Gates (YouTube)](https://www.youtube.com/watch?v=gI-qXk7XojA)
* [What is a Boolean Data Type, and What are Some Uses? (Sitepoint)](https://www.sitepoint.com/boolean-data-type/)

</details>

True or false Boolean values are usually determined by the outcome of a statement containing a Boolean operator. For example:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
10 > 5 // Output: True

"Monkey" == "Banana" // Output: False
```
{% endcode %}

However, there are also some values in Notion formulas that are inherently **truthy** or **falsy.**

The following values in a Notion formula are always **falsy:**

* `false`
* `0`
* `-0`
* `""` (an empty [string](string.md))

You can test this for yourself by creating a Notion formula containing this statement, which outputs **false**:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
0 ? true : false // Output: False
```
{% endcode %}

By contrast, the following will output **true:**

{% code overflow="wrap" lineNumbers="true" %}
```javascript
1 ? true : false // Output: True
```
{% endcode %}

All values not listed above are inherently **truthy,** including:

* `true`
* `"0"` - a string containing 0
* `"false"` - a string containing "false"
* `"anything"` - a string containing any text
* `now()` - a [date](date-data-type.md) (the [now](../../formula-components/functions/now.md) function outputs the current date and time as a date object)

You can see proofs of these statements in this example database:

<figure><img src="../../.gitbook/assets/Truthy and Falsy Values.png" alt=""><figcaption></figcaption></figure>

{% embed url="https://thomasfrank.notion.site/Truthy-and-Falsy-Values-44788fab335647fcb3dbe1a8fa6f7a99" %}

## Boolean Operators in Notion

Notion comes with several Boolean [operators](../../formula-components/operators/).&#x20;

These can be used to perform comparisons between two values (which must share the same data type), outputting a [true](../../formula-components/constants/true.md) or [false](../../formula-components/constants/false.md) value.&#x20;

They can be separated into two categories: **logical operators** and **comparison operators.**

### Logical Operators

Logical operators return a Boolean value, and often allow you to combine and evaluate multiple expressions.

Notion provides three logical operators.

{% hint style="info" %}
**Good to know:** Notion is picky about how you must write logical operators. Only the listed symbols will work, and they are case-sensitive.

E.g. You must use `and` for the [and](../../formula-components/operators/and.md) operator - `And`, `AND`, and `&&` will not work in Notion.
{% endhint %}

| Operator                                         | Symbol | Function Version | Example              |
| ------------------------------------------------ | ------ | ---------------- | -------------------- |
| [and](../../formula-components/operators/and.md) | `and`  | `and()`          | `2 > 3 and 4 < 8`    |
| [or](../../formula-components/operators/or.md)   | `or`   | `or()`           | `2 > 1 or 6 > 5`     |
| [not](../../formula-components/operators/not.md) | `not`  | `not()`          | `not empty("Hello")` |

## Comparison Operators

Comparison operators allow you to compare operands that share a data type.

Notion provides six comparison operators:

| Operator                                                     | Symbol | Function Version | Example  |
| ------------------------------------------------------------ | ------ | ---------------- | -------- |
| [equal](../../formula-components/operators/equal.md)         | `==`   | `equal()`        | `2 == 2` |
| [unequal](../../formula-components/operators/unequal.md)     | `!=`   | `unequal()`      | `4 != 2` |
| [larger](../../formula-components/operators/larger.md)       | `>`    | `larger()`       | `5 > 3`  |
| [largerEq](../../formula-components/operators/largereq.md)   | `>=`   | `largerEq()`     | `4 >= 4` |
| [smaller](../../formula-components/operators/smaller.md)     | `<`    | `smaller()`      | `6 < 9`  |
| [smallerEq](../../formula-components/operators/smallereq.md) | `<=`   | `smallerEq()`    | `9 <= 9` |

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
