---
description: Learn how to use the replaceAll function within a Notion formula.
---

# replaceAll

The `replaceAll()` function searches a [string](../../formula-basics/data-types/string.md) for a pattern (which can be a [regular expression](../../reference/regular-expressions-in-notion-formulas.md)), and replaces ALL matches it finds with another string.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll(string, string [regex supported], string [regex supported])
```
{% endcode %}

Since they can search for pattern matches using regular expressions, `replaceAll()` and its counterpart, [replace](replace.md), are two of the most versatile and powerful functions you can use in your Notion formulas.

{% hint style="info" %}
**Good to know:** `replaceAll()`, [replace](replace.md), and [test](test.md) are able to automatically convert [numbers](../../formula-basics/data-types/number.md) and [Booleans](../../formula-basics/data-types/boolean-checkbox.md) (but not [dates](../../formula-basics/data-types/date-data-type.md)) to strings. Manual [type conversion](../../reference/converting-data-types.md) is not needed.
{% endhint %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("Dogs Dogs Dogs","Dogs","Cats") // Output: Cats Cats Cats

// Matches are case-sensitive
replaceAll("Dogs dogs Dogs","Dogs","Cats") // Output: Cats dogs Cats

// You can use brackets [] to create a set of characters,
// any of which will be matched
replaceAll("Dogs dogs Dogs", "[Dd]ogs", "Cats") // Output: Cats Cats Cats

// You can also create a group with () and then use the | (OR) operator
replaceAll("Dogs dogs Dogs", "(D|d)ogs", "Cats") // Cats Cats Cats

// Accepts regex metacharacters, such as "\\b" which denotes "word boundary".
// Without \\b, this would output "Thwas was Sparta"
replaceAll("This is Sparta","\\bis\\b","was") // Output: This was Sparta

// replaceAll() is a great way to count elements in a string.
// Do this by using a regular expression to remove all characters
// except the commas that separate the elements (see the example
// database below for an in-depth look at this)
replaceAll("Dog, Cat, Monkey, Bat, Gorilla","[^,]","") // Output: ,,,,
// Apply length() + 1 to get the count!
```
{% endcode %}

{% hint style="info" %}
Check out the [regular expressions](../../reference/regular-expressions-in-notion-formulas.md) page to see a **lot** more that you can accomplish using them!
{% endhint %}

## Example Database

This example database uses a multi-select property to track which superpowers each hero has. The **Count** formula uses `replaceAll()` to output a superpower count for each hero.

![](<../../.gitbook/assets/Tag Counter - replaceAll Function - Notion Formulas - version 2.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/replaceAll-7cd44e7721ae4d1d8e5f508ff92995ee" %}

### “Count” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Compressed
prop("Name") + " has " + format(length(replaceAll(prop("Powers"), "[^,]", "")) + 1) + ((length(replaceAll(prop("Powers"), "[^,]", "")) < 1) ? " power." : " powers.")

// Expanded
prop("Name") + 
" has " + 
format(
    length(
        replaceAll(
            prop("Powers"), 
            "[^,]", 
            ""
        )
    ) + 1
) + 
(
    (
        length(
            replaceAll(
                prop("Powers"), 
                "[^,]", 
                ""
            )
        ) < 1
    ) ? 
    " power." : 
    " powers."
)
```
{% endcode %}

When you call a multi-select property from within a formula, you end up with a single string where each select value is separated by a comma - e.g. “Super Strength, Ice Breath, Flight”.

As long as your multi-select options don’t _contain_ commas themselves, we can take advantage of this fact. Since each value is separated by a comma, all we need to do is **count the commas and then add one.**

For example, `“Super Strength, Ice Breath, Flight”` has two commas. Adding one to that number gets us the total number of select options: three.

But how can we count the commas? That’s where `replaceAll()` comes in.

In our formula, we use `replaceAll(prop("Powers"), "[^,]", "")` to replace ALL instances of any character that _isn’t_ a comma with `""` - an empty value. In effect, this removes all characters except the commas.

We target these characters with the [regular expression](../../reference/regular-expressions-in-notion-formulas.md) `[^,]`:

1. The brackets `[]` define a set of characters where any of them will be part of the match. E.g. a regular expression like `[Dd]og` would match both “Dog” and “dog”.
   1. Since we’re using `replaceAll()` instead of [replace](replace.md), using the brackets ensures that _every_ character in our search string that matches a character in the brackets will be replaced.
2. The caret `^` used within the brackets `[]` is a flag that says, “match a character that is _not_ defined in the brackets”. - e.g. `[^d]` would match any character that isn’t “d”.
3. In the brackets, we define the comma `,` as the character after the caret.

In effect, `[^,]` says, “match any character that isn’t a comma”.

This results in a string of commas - e.g. “Super Strength, Ice Breath, Flight” becomes “,,”.

From there, we can use the [length](length.md) function to get the length of our resulting string. `length(",,")` = `2`.

Adding 1, we get the actual number of select tags in the row - in the case, `3`.

Finally, we use [format](format.md) and do some string concatenation with the [add](../operators/add.md) (`+`) operator in order to create a sentence like, “Superman has 3 powers”.

The formula ends with another usage of this `replaceAll()` → `length()` chain within an [if statement](../operators/if.md) (using the conditional operators `?` and `:`) in order to determine if the sentence should end with “power” or “powers”.

#### Other formula components used in this example:

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

{% content-ref url="format.md" %}
[format.md](format.md)
{% endcontent-ref %}

{% content-ref url="length.md" %}
[length.md](length.md)
{% endcontent-ref %}

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="../operators/smaller.md" %}
[smaller.md](../operators/smaller.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
