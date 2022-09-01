---
description: Learn how to use the slice function in Notion formulas.
---

# slice

The `slice()` function allows you to “slice” up a [string](../../formula-basics/data-types/string.md) and output a smaller piece of it. It accepts three arguments:

1. The input [string](../../formula-basics/data-types/string.md)
2. A starting index, which is **included** in the output string (the start index of the input string is `0`).
3. An ending index, which is **optional** and **excluded** from the output string.

{% hint style="info" %}
**Good to know:** `slice()` works best when you know the indexes you want to use, or when they need to be mathematically derived (e.g. based on a percentage, such as “% of tasks completed”).&#x20;

If you need to define your index by matching a pattern (e.g. “Get the middle name” from a Full Name field), you should use [replace](replace.md) or [replaceAll](replaceall.md) instead (or combine them with slice).
{% endhint %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
slice("Dangerfield",0,6) // Output: Danger

slice("Monkey D. Luffy",0,6) // Output: Monkey

slice("Monkey D. Luffy", 10, 15) // Ouput: Luffy

slice("●●●●●●●●●●",0,6) + slice("○○○○○○○○○○",0,6) // Output: ●●●●●○○○○○
```
{% endcode %}

## Example Database

This example database uses the `slice()` function to create a simple progress bar. The output of the progress bar is determined by the **Percent** number property.

![](<../../.gitbook/assets/Progress Bar - Slice Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/slice-f8046dc7b0c34536bbe9136ff28cd24c" %}

### “Progress” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
slice("●●●●●●●●●●", 0, prop("Percent") * 10) + slice("○○○○○○○○○○", 0, (1 - prop("Percent")) * 10) + " " + format(prop("Percent") * 100) + "%"

// Expanded
slice(
    "●●●●●●●●●●", 
    0, 
    prop("Percent") * 10
) + 
slice(
    "○○○○○○○○○○", 
    0, 
    (1 - prop("Percent")) * 10
) + 
" " + 
format(
    prop("Percent") * 100
) + 
"%"
```
{% endcode %}

This formula creates a progress bar by using two instances of the `slice()` function, along with the unicode characters `●` and `○` (see this [Unicode character reference](https://www.w3.org/TR/xml-entity-names/025.html) for more options).

1. The first `slice()` starts with `●●●●●●●●●●` as the input string. There are 10 `●` symbols. We start at index `0`, and then define the ending index using the **Percent property.**
   1. Note that we have to multiply `prop("Percent")` by 10, since a percent value like 40% actually equates to `0.4`. Since there are 10 `●` characters in our input string, we need an ending index between 0 and 10.
2. The second `slice()` does nearly the same thing with the string: `○○○○○○○○○○`, which represents the “empty” part of the progress bar.
   1. To find the ending index for this string, we use `(1 - prop("Percent")) * 10` in order to get the _remaining_ percentage. E.G. if **Percent** is set to 40% (which would create an end index of `4`), we want to set this ending index to `6`.
3. Finally, the two strings are concatenated. We also show the actual percentage in the string for good measure.

#### Other formula components used in this example:

{% content-ref url="../operators/multiply.md" %}
[multiply.md](../operators/multiply.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

{% content-ref url="../operators/subtract.md" %}
[subtract.md](../operators/subtract.md)
{% endcontent-ref %}

{% content-ref url="format.md" %}
[format.md](format.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
