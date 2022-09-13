---
description: Learn how to use the add (+) operator in Notion formulas.
---

# add

The **add** (`+`) operator allows you to:

* Perform addition on [numbers](../../formula-basics/data-types/number.md)
* Concatenate [strings](../../formula-basics/data-types/string.md) - i.e. combine them (also doable with [concat](../functions/concat.md))

When used in mathematical equations, the `+` operator follows the standard mathematical order of operations (PEMDAS). For more detail, see [Operator Precedence](../../reference/operator-precedence-and-associativity.md).

You can also use the function version, `add()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
2 + 5 // Output: 7

"Monkey D." + " Luffy" // Output: Monkey D. Luffy

add(4,7) // Output: 11

add("Monkey D."," Luffy") // Output: Monkey D. Luffy
```
{% endcode %}

### Working with 3 or More Operands

Since **add** is a binary [operator](./), it can only work on two _operands -_ the objects which are being operated on ([if](if.md) - the _ternary operator -_ is the only operator that works on three operands).

If you need to work with more than two operands, the shorthand `+` is by far the easiest way to do it.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
4 + 3 + 6 + 9 // Output: 20

add(add(4,3),add(6,9)) // Output: 20

"King" + " of the " + "Pirates" // Output: King of the Pirates

add(add("King"," of the "),"Pirates") // Output: King of the Pirates 
```
{% endcode %}

## Example Database

The example database below tracks a week of treasure-collecting by three pirates. The **Total** formula adds up all the treasure gathered by the three pirates collectively.

![](<../../.gitbook/assets/Treasure Collected.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/add-37fb95f8d8564fae8d7f9ccdc2996e96" %}

Note how I’ve set the **number format** of each column to **U.S. Dollar.** I’ve also set each column’s **Calculate** value to **Sum,** allowing me to see the total of all rows put together.

### "Total" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
prop("Luffy") + prop("Zoro") + prop("Nami")
```
{% endcode %}

Instead of using hard-coded numbers, I’ve called in each property using the `prop()` function.

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
