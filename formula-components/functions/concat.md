---
description: Learn how to use the concat function in Notion formulas.
---

# concat

The `concat()` function concatenates (aka combines) its arguments. It accepts one or more [string](../../formula-basics/data-types/string.md) arguments, and outputs a single combined string.

`concat()` can accept any number of arguments.

{% hint style="info" %}
**Good to know:** You can also concatenate strings with the [add](../operators/add.md) (`+`) operator.
{% endhint %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
concat("Roronoa ","Zoro") // Output: Roronoa Zoro

"Roronoa " + "Zoro" // Output: Roronoa Zoro

concat("Chopper") // Output: Chopper (this is pointless, but it works)

concat("Monkey", " D.", "Luffy", " will ", "be", " King of the Pirates")
// Output: Monkey D. Luffy will be King of the Pirates

// use "\n" to create line breaks
concat("Luffy \n", "Zoro \n", "Sanji \n", "Nami \n")
// Output:
// Luffy
// Zoro
// Sanji
// Nami
```
{% endcode %}

You can use conversion functions like [format](format.md) or [formatDate](formatdate.md) to convert other [data types](../../formula-basics/data-types/) into strings before concatenating them:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
concat("Today is ", formatDate(now(), "MMMM DD, YYYY"))
// Output: Today is June 17, 2022 (this will change with the value of now())
```
{% endcode %}

## Example Database

This example database collects several different pieces of customer information, including first name, last name, phone number, and location. The **Info** formula neatly formats all of this information into a single cell.

To display phone numbers in a more consistent manner, there is a helper property - **Ph Format** - which formats the data from the **Phone** property. **Info** then pulls from **Ph Format** rather than **Phone** directly.

![](<../../.gitbook/assets/Concat Example - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/5f9f4090c0ae4d9690c389a3a2f7d644?v=e48584527f7247e79d054638e7f07ecf" %}

### “Info” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
concat("🧑 ", prop("First Name"), " ", prop("Last Name"), "\n📍 ", prop("Location"), "\n☎️ ", prop("Ph Format"))

// Expanded
concat(
    "🧑 ", 
    prop("First Name"), 
    " ", 
    prop("Last Name"), 
    "\n📍 ", 
    prop("Location"), 
    "\n☎️ ", 
    prop("Ph Format")
)
```
{% endcode %}

Here, we simply use `concat()` with multiple arguments to combine all of our properties. We also pass some useful formatting strings as arguments, such as `"🧑 "` and `"\n📍 "`. The `\n` characters create new lines.

### “Ph Format” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
"(" + slice(replaceAll(prop("Phone"), "[() .-]", ""), 0, 3) + ") " + slice(replaceAll(prop("Phone"), "[() .-]", ""), 3, 6) + "-" + slice(replaceAll(prop("Phone"), "[() .-]", ""), 6, 10)

// Expanded
"(" + 
slice(
    replaceAll(
        prop("Phone"), "[() .-]", ""
    ), 0, 3
) + 
") " + 
slice(
    replaceAll(
        prop("Phone"), "[() .-]", ""
    ), 3, 6
) + 
"-" + 
slice(
    replaceAll(
        prop("Phone"), "[() .-]", ""
    ), 6, 10
)
```
{% endcode %}

The **Ph Format** formula is a slightly more complex formula that uses the [add](../operators/add.md) (`+`) operator for concatenation instead of `concat()`. In many cases, you’ll find `+` to be a far quicker way to combine strings.

Here’s how the formula formats the phone numbers, which are originally string values from the **Phone** property:

1. We use the [slice](slice.md) function multiple times to chop the phone number into three discrete pieces.
   1. For each piece, we use [replaceAll](replaceall.md) and the [regular expression](../../reference/regular-expressions-in-notion-formulas.md) `"[() .-]"` to remove any non-numeric characters. The brackets (`[]`) indicate that every matched instance of _any_ character between them should be replaced.
2. Next, we use the `+` operator to concatenate these number slices with useful formatting (e.g. `"("` and `"-"`) to get our standard format: `(xxx) xxx-xxxx`.

#### Other formula components used in this example:

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

{% content-ref url="slice.md" %}
[slice.md](slice.md)
{% endcontent-ref %}

{% content-ref url="replaceall.md" %}
[replaceall.md](replaceall.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
