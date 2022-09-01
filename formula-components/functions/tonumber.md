---
description: Learn how to use the toNumber function in Notion formulas.
---

# toNumber

The `toNumber()` function converts its argument to a [number](../../formula-basics/data-types/number.md) if it can do so. It is useful for converting [strings](../../formula-basics/data-types/string.md), [Booleans](../../formula-basics/data-types/boolean-checkbox.md), and [dates](../../formula-basics/data-types/date-data-type.md) to numbers.

Unlike [unaryPlus](../operators/unaryplus.md), `toNumber()` _can_ convert dates to numbers. When used to convert a date, toNumber will convert it to its corresponding Unix timestamp; this behavior matches that of the [timestamp](timestamp.md) function.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
toNumber("42") // Output: 42 (number)

toNumber(true) // Output: 1

toNumber(false) // Output: 0

toNumber(5>3) // Output: 1

toNumber(now()) // Output: 1655757000000 (changes with now()'s value)
```
{% endcode %}

## Example Database

This example database is a simple habit tracker. Each property represents a different habit, and the Habits formula property adds them up and outputs a string reporting the number of habits completed on that day.

![](<../../.gitbook/assets/toNumber Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/toNumber-c0475c7eae804e98b0ce3f1f13cbebd6" %}

### “Habits” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
format(toNumber(prop("💧")) + toNumber(prop("🏃‍♂️")) + toNumber(prop("🏋️‍♀️")) + toNumber(prop("🥦"))) + "/4" + if((toNumber(prop("💧")) + toNumber(prop("🏃‍♂️")) + toNumber(prop("🏋️‍♀️")) + toNumber(prop("🥦"))) == 1," Habit"," Habits")

// Expanded
format(
    toNumber(
        prop("💧")
    ) + 
    toNumber(
        prop("🏃‍♂️")
    ) + 
    toNumber(
        prop("🏋️‍♀️")
    ) + 
    toNumber(
        prop("🥦")
    )
) + 
"/4" + 
if(
    (
        toNumber(
            prop("💧")
        ) + 
        toNumber(
            prop("🏃‍♂️")
        ) + 
        toNumber(
            prop("🏋️‍♀️")
        ) + 
        toNumber(
            prop("🥦")
        )
    ) == 1,
    " Habit",
    " Habits"
)
```
{% endcode %}

This formula uses `toNumber()` to convert the [Boolean](../../formula-basics/data-types/boolean-checkbox.md) output of each habit’s checkbox value into a [number](../../formula-basics/data-types/number.md) - either `1` or `0`. It then adds up all the numbers to get a total number of habits completed for the day.

The [format](format.md) function is then used to [convert](../../reference/converting-data-types.md) this number into a [string](../../formula-basics/data-types/string.md) so that it can be combined with the other string elements in the formula.

Finally, an [if statement](../operators/if.md) uses the same process to determine if the total number of habits completed is equal to `1`. If so, it outputs “Habit”; if not, it outputs the plural “Habits”.

#### Other formula components used in this example:

{% content-ref url="format.md" %}
[format.md](format.md)
{% endcontent-ref %}

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
