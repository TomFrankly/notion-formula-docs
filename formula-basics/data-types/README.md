---
description: Learn about the four data types supported in Notion formulas.
---

# Data Types

Notion formulas can accept (and return) four different types of data: String, Number, Boolean (aka Checkbox), and Date.

| Data Type                                                  | Examples                 |   |
| ---------------------------------------------------------- | ------------------------ | - |
| [String](string.md)                                        | `"King of the Pirates"`  |   |
| [Number](number.md)                                        | `9001`                   |   |
| [Boolean](boolean-checkbox.md) (called Checkbox in Notion) | `true`, `false`          |   |
| [Date](date-data-type.md)                                  | `"2022-11-11T12:00:00Z"` |   |

Notion formulas almost never do automatic type conversion.

{% hint style="info" %}
_The only exceptions to this are within the_ [_test_](../../formula-components/functions/test.md)_,_ [_replace_](../../formula-components/functions/replace.md)_, and_ [_replaceAll_](../../formula-components/functions/replaceall.md) _functions. These are advanced functions, so I won't cover their details here._
{% endhint %}

This fact has several implications:

**First, a formula must output data of a single type.** The following will throw a _Type Mismatch error:_

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Type Mismatch
"Monkey D. Luffy is " + 19 + " years old."
```
{% endcode %}

You'll need to [convert](../../reference/converting-data-types.md) the number to a string in order to make this formula work

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Valid
"Monkey D. Luffy is " + format(19) + " years old."
```
{% endcode %}

Now the formula is outputting string data only.

**Second, operators must have operands of the same type, and arguments within functions must be of the type specified by the function.**

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Type Mismatch
"42" == 42

// Valid - unaryPlus operator (+) converts the string to a number
+"42" == 42

// Also valid - format() converts 42 to a string
"42" == format(42)

---

// Type Mismatch - dateBetween's first and second arguments must be dates, not simply strings containing representations of dates
dateBetween("June 1, 2022", "June 30, 2022", "days")

// Valid - the function is now using dates in its first two arguments (assume a date property called "Date" exists)
dateBetween(prop("Date"), now(), "days")
```
{% endcode %}

{% hint style="info" %}
**Good to know:** Since Notion formulas don't do automatic type conversion, the equals (`==`) operator tests for **strict equality** (see the [JavaScript reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict\_equality) page on this)**.**&#x20;

E.g. `"1" == 1` will throw a Type Mismatch error in Notion. In JavaScript, it would return `true`.
{% endhint %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
