---
description: Learn how to use the format function in Notion formulas.
---

# format

The `format()` function formats its argument as a string. It accepts all [data types](../../formula-basics/data-types/), including [dates](../../formula-basics/data-types/date-data-type.md), [Booleans](../../formula-basics/data-types/boolean-checkbox.md), [numbers](../../formula-basics/data-types/number.md), and even [strings](../../formula-basics/data-types/string.md).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
format(number)
format(Boolean)
format(date)
format(string)
```
{% endcode %}

`format()` is very useful for converting data types within Notion formulas.

{% hint style="info" %}
**Good to know:** Notion formulas can only output a single [data type](../../formula-basics/data-types/), and [comparison operators](../operators/#comparison-operators) can only compare data that share the same type.&#x20;

See [Converting Data Types](../../reference/converting-data-types.md) to learn all of the ways to convert data in Notion formulas.
{% endhint %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
format(4) // Output: 4 (as a string)

format(5+5) // Output: 10 (as a string)

format(true) // Output: true (as a string)

format(5>4) // Output: true (as a string)

format(now()) // Output: June 20, 2022 2:23 PM (changes with now()'s value)

"There are " + format(10) + " Straw Hat members."
// Output: There are 10 Straw Hat members.
```
{% endcode %}

## Example Database

This example database uses the `format()` function to output a string stating the age of each character.

![](<../../.gitbook/assets/Format Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/format-d297d2dc11bb41a4a3a8b27d52e73722" %}

### “Age” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
"⏳ " + prop("Name") + " is " + format(dateBetween(now(), prop("Birthday"), "years")) + " years old."

// Expanded
"⏳ " + 
prop("Name") + 
" is " + 
format(
    dateBetween(
        now(), 
        prop("Birthday"), 
        "years"
    )
) + 
" years old."
```
{% endcode %}

This formula outputs a sentence stating how old each character is based on their birthday.

To obtain the character’s age, we use the [dateBetween](datebetween.md) function to find the number of years between [now](now.md) and the character’s birthday.

`dateBetween()` returns a number, so we use the `format()` function to convert it to a string.

{% hint style="info" %}
**Note:** To keep thinks simple, this example formula doesn't use conditional logic to determine whether the string should output "year" or "years" (accounting for plurality). To see an example that does, check out the [length](length.md) function.
{% endhint %}

#### Other formula components used in this example:

{% content-ref url="datebetween.md" %}
[datebetween.md](datebetween.md)
{% endcontent-ref %}

{% content-ref url="now.md" %}
[now.md](now.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
