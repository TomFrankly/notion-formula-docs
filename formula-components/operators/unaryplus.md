---
description: Learn how to use the unaryPlus (+) operator in Notion formulas.
---

# unaryPlus

The **unaryPlus (`+`)** operator is used to convert [Booleans](../../formula-basics/data-types/boolean-checkbox.md) and numeric [strings](../../formula-basics/data-types/string.md) to [numbers](../../formula-basics/data-types/number.md).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
+string
+Boolean

unaryPlus(string)
unaryPlus(Boolean)
```
{% endcode %}

Unlike [toNumber](../functions/tonumber.md), it cannot convert [dates](../../formula-basics/data-types/date-data-type.md) to numbers. Otherwise, it is functionally equivalent, and it can be written with the `+` operator for quick use.

You can also use the function version, `unaryPlus()`.

{% hint style="info" %}
**Good to know:** A _unary_ operator only has a single operand, while a _binary_ operator has two. unaryPlus and unaryMinus are, as their names imply, unary operators. Examples of binary operators include [add](add.md), [divide](divide.md), [pow](pow.md), etc.
{% endhint %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
+"42" // Output: 42

+true // Output: 1

+false // Output: 0

unaryPlus("42") // Output: 42
```
{% endcode %}

`unaryPlus()` can be combined with other operators, including [unaryMinus](unaryminus.md) and even [add](add.md), which uses the same `+` character.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
20 + + "30" // Output: 50

-+"30" // Output: -30

20 + - + "30" // Output? -10 [Notion will rewrite this to 20 + -(+"30")]
```
{% endcode %}

## Example Database: Daily Habit Score

The example database below tracks daily habits with a checkbox property for each habit. The **Score** property converts each checkbox’s Boolean value into a number, and then adds up a total score for the day.

![](<../../.gitbook/assets/Daily Habit Score - unaryPlus.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/unaryPlus-c01b055e99eb46688e5d4b596f0dd4d6" %}

### "Score" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
+prop("Deck Swabbed") + +prop("Teeth Brushed") + +prop("Lime Eaten")
```
{% endcode %}

#### Other formula components used in this example:

{% content-ref url="add.md" %}
[add.md](add.md)
{% endcontent-ref %}

## Example Database: Numeric Phone Numbers

Notion's **Phone Number** property type outputs a string (see it listed in the [API Reference](https://developers.notion.com/reference/property-object#database-properties) for more detail).

The example database below uses unaryPlus and the [replaceAll](../functions/replaceall.md) function to turn phone numbers into true numbers, even if they have additional formatting.

![](<../../.gitbook/assets/Phone Number Converter.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/unaryPlus-c01b055e99eb46688e5d4b596f0dd4d6" %}

### “Number” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
+replaceAll(prop("Phone"), "[() -]", "")
```
{% endcode %}

unaryPlus can’t operate on a string that contains non-numeric characters such as `(` or `-`. So **Number** first uses the [replaceAll](../functions/replaceall.md) function to remove them. It does this by passing a [regular expression](../../reference/regular-expressions-in-notion-formulas.md) in its matching argument - `"[() -]"` - where the special bracket `[]` characters equate to:

> “Match _any_ character listed here.”

This includes the `space`.

Next, `replaceAll()`'s replacement argument replaces all matched characters with an empty string - `""` - in effect removing them. The result is a phone number converted to a purely numeric string - e.g. `(482) 491-5813` is converted to `4824915813`.

Finally, the `+` operator converts this numeric string into a true number.

#### Other formula components used in this example:

{% content-ref url="../functions/replaceall.md" %}
[replaceall.md](../functions/replaceall.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
