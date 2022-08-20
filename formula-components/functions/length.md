---
description: Learn how to use the length function in Notion formulas.
---

# length

The `length()` function outputs a [number](../../formula-basics/data-types/number.md) that corresponds to the length of a [string](../../formula-basics/data-types/string.md).

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
length("Monkey D. Luffy") // Output: 15

length("Supercalifragilisticexpialidocious") // Output: 34

length("Doctor Doom") // Output: 11
```
{% endcode %}

## Example Database

This example database used the `length()` function to return the number of characters in the Name property. It also uses an [if statement](../operators/if.md) to intelligently output “character” or “characters”.

![](<../../.gitbook/assets/Length Function Example - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/690ca7be6c704413b655f31b29153570?v=ca679009d9834a5f89271ac39dbf45d3" %}

### “Characters” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
format(length(prop("Name"))) + " " + ((length(prop("Name")) == 1) ? "character" : "characters")

// Expanded
format(
    length(prop("Name"))
) + 
" " + 
(
    (
        length(
            prop("Name")
        ) == 1
    ) ? 
    "character" : 
    "characters"
)
```
{% endcode %}

This formula first uses the `length()` function to get the number of characters in the Name property. This is wrapped in the [format](format.md) function in order to [convert](../../reference/converting-data-types.md) the number to a string.

Second, an [if statement](../operators/if.md) again uses `length()` to check whether or not the number of characters in the Name property is equal to `1`. If so, it outputs the singular “character”. If not, it outputs the plural “characters.”

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="format.md" %}
[format.md](format.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
