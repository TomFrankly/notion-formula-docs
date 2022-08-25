---
description: Learn about the String data type in Notion formulas.
---

# String

The String data type holds and represents text content. Strings can hold nearly any character by default.

You can create a string by wrapping characters within quotation marks `"`. This includes numbers, "true/false", etc. If you wrap characters in quotation marks, you'll create a string.

{% code overflow="wrap" lineNumbers="true" %}
```javascript
"Monkey D. Luffy"

"42"

"true"
```
{% endcode %}

Strings can be **concatenated,** i.e. combined. You can do so with the [concat](../../formula-components/functions/concat.md) function and with the [add](../../formula-components/operators/add.md) operator `+`:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
"Monkey D. Luffy" + " will be " + "King of the Pirates!"
// Output: Monkey D. Luffy will be King of the Pirates!

concat("Monkey D. Luffy", " will be ", "King of the Pirates!")
// Output: Monkey D. Luffy will be King of the Pirates!
```
{% endcode %}

You cannot perform mathematical operations on strings. Notion does not do automatic type conversion, so you'll need to convert strings to numbers manually.

If a string contains nothing but a number, you can convert it using the [toNumber](../../formula-components/functions/tonumber.md) function or the [unaryPlus](../../formula-components/operators/unaryplus.md) operator `+`:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Invalid: Will throw a Type Mismatch error
add(2, "2")

// Valid
add(2, toNumber("2"))

// Also valid
add(2, +"2")
```
{% endcode %}

## Comparing Strings

You can compare strings using the equal `==` and unequal `!=` operators and related functions.

{% hint style="info" %}
**Good to know:** As noted above, Notion formulas do not do automatic type conversion. Therefore, the equal and unequal operators test for **strict equality.** In JavaScript, this would be done with the `===` operator.
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```javascript
"Monkey" == "Monkey" // Output: true

"Monkey" == "monkey" // Output: false (comparison is case-sensitive)

"Goku" != "Vegeta" // Output: true
```
{% endcode %}

## Escaping Characters

Some special characters must be **escaped** with the backslash character `\` in order to represented property in a Notion formula.

| Character        | Escape Sequence |
| ---------------- | --------------- |
| Double Quote `"` | `\"`            |
| Backslash `\`    | `\\`            |
| Newline          | `\n`            |
| Tab              | `\t`            |
| Carriage Return  | `\r`            |

**Important notes:**

* Double quotes `"` will become un-escaped whenever you re-open and edit your formula. You'll need to re-escape them every time you make an edit.
* Single quotes `'` do not need to be escaped. If you wrap a string in single quotes, they'll be converted to double quotes the next time you open the formula for editing.

Here's a reference database that contains all of these escaped characters, which you can duplicate:

{% embed url="https://thomasfrank.notion.site/Character-Escapes-14ebcf5e74144b07bfe00d03ef8d9312" %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
