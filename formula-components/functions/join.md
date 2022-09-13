---
description: Learn how to use the join function in Notion formulas.
---

# join

The `join()` function takes its first argument and inserts it in between each of its additional arguments. It accepts only [string](../../formula-basics/data-types/string.md) arguments.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
join(string, string, string)
```
{% endcode %}

`join()` can accept one or more arguments, but needs at least three to perform its intended function.

`join()` acts much like JavaScript’s [Array.prototype.join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/join) method, with all but the first argument acting as the elements inside an array. Note that Notion’s `join()` function does not use a default separator (e.g. `,`), so you’ll always need to define one.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
join(", ","Luffy","Zoro","Nami","Chopper") 
// Output: Luffy, Zoro, Nami, Chopper

// Use "\n" to add line breaks
join("\n","Luffy","Zoro","Nami","Chopper")
// Output:
// Luffy
// Zoro
// Nami
// Chopper
```
{% endcode %}

## Example Database

This example database creates a roster for different missions. Each member in the pirate crew can mark whether or not they’re attending, and the **Roster** formula will output a list of those attending and not attending.&#x20;

The `join()` function is used to create line breaks.

![](<../../.gitbook/assets/Join Example - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/join-7081958e7841470dbd4c7f10fbf160ba" %}

### “Roster” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
join("\n", (prop("Luffy") == true) ? "Luffy attending" : "Luffy not attending", (prop("Sanji") == true) ? "Sanji attending" : "Sanji not attending", (prop("Zoro") == true) ? "Zoro attending" : "Zoro not attending", (prop("Chopper") == true) ? "Chopper attending" : "Chopper not attending")

// Expanded
join(
    "\n", 
    (prop("Luffy") == true) ? "Luffy attending" : "Luffy not attending", 
    (prop("Sanji") == true) ? "Sanji attending" : "Sanji not attending", 
    (prop("Zoro") == true) ? "Zoro attending" : "Zoro not attending", 
    (prop("Chopper") == true) ? "Chopper attending" : "Chopper not attending"
)
```
{% endcode %}

This `join()` example inserts `"\n"` between each string to create line breaks.

### “Roster Pretty” Property Formula

For fun, here’s another take on the **Roster** formula that uses [replace](replace.md) and [replaceAll](replaceall.md) - along with some advanced [regular expressions](../../reference/regular-expressions-in-notion-formulas.md) - to create a single sentence that includes only the members who are attending (complete with commas):

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
replace(replace(replace(replaceAll(join(", ", (prop("Luffy") == true) ? "Luffy" : "", (prop("Sanji") == true) ? "Sanji" : "", (prop("Zoro") == true) ? "Zoro" : "", (prop("Chopper") == true) ? "Chopper" : ""), "(^, | ,)", ""), "[,].$", ""), ",(?!.*,)", ", and"), "^([^,]*), and", "$1 and")

// Expanded
replace(
    replace(
        replace(
            replaceAll(
                join(
                    ", ", 
                    (prop("Luffy") == true) ? "Luffy" : "", 
                    (prop("Sanji") == true) ? "Sanji" : "", 
                    (prop("Zoro") == true) ? "Zoro" : "", 
                    (prop("Chopper") == true) ? "Chopper" : ""
                ), "(^, | ,)", ""
            ), "[,].$", ""
        ), ",(?!.*,)", ", and"
    ), "^([^,]*), and", "$1 and"
)
```
{% endcode %}

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="replace.md" %}
[replace.md](replace.md)
{% endcontent-ref %}

{% content-ref url="replaceall.md" %}
[replaceall.md](replaceall.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
