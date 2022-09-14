---
description: >-
  Learn how to use the Boolean inequality (!=) operator and unequal() function
  in Notion formulas.
---

# unequal

The inequality (`!=`) operator returns [true](../constants/true.md) if its operands are not equal. It accepts operands of all [data types](../../formula-basics/data-types/) - [strings](../../formula-basics/data-types/string.md), [numbers](../../formula-basics/data-types/number.md), [Booleans](../../formula-basics/data-types/boolean-checkbox.md), and [dates](../../formula-basics/data-types/date-data-type.md).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
string != string
number != number
Boolean != Boolean
date != date

unequal(string, string)
unequal(number, number)
unequal(Boolean, Boolean)
unequal(date, date)
```
{% endcode %}

{% hint style="info" %}
**Good to know:** Notion does not allow for comparisons between different [data types](../../formula-basics/data-types/). You must convert all data to a common type before making a comparison (e.g. by using [format()](../functions/format.md) to create a string value).
{% endhint %}

You can also use the function version, `unequal()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
1 != 2 // Output: True

1 != 1 // Output: False

unequal("Cat","Dog") // Output: True

"1" != 2 // Type mismatch error

2^3 != 10 // Output: True
```
{% endcode %}

{% hint style="info" %}
**Good to know:** The inequality (`!=`) operator _cannot_ be chained in a Notion formula. A formula like `1 != 2 != 3` won't work. Use the [and](and.md) operator to get around this - e.g. `1 != 2 and 2 != 3`.
{% endhint %}

## Example Database

The example database below contains a **Cat Status** property that will inform you on whether or not your lawyer is a cat.

![](<../../.gitbook/assets/Unequal Test Database Notion.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/unequal-e0cbfc53d4cb421ea21f86a0ce11c652" %}

### “Cat Status” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
(prop("Type") != "Cat") ? "Your lawyer is not a cat." : "Your lawyer is a cat."
```
{% endcode %}

{% hint style="success" %}
If you understand this well, you may want to check out the more complex example on the [equality](equal.md) (`==`) operator's page.
{% endhint %}

#### Other formula components used in this example:

{% content-ref url="if.md" %}
[if.md](if.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
