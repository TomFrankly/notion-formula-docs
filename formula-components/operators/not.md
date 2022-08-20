---
description: Learn how to use the Boolean "not" operator in Notion formulas.
---

# not

The **not** operator inverts the truth value of a [Boolean/Checkbox](../../formula-basics/data-types/boolean-checkbox.md) value in a Notion formula. Another way of thinking about it is that it returns [true](../constants/true.md) only if its operand is [false](../constants/true.md). It accepts [Boolean](../../formula-basics/data-types/boolean-checkbox.md) operands.

It can be used in several ways, including:

* Changing `true` to `false`, or vice-versa
* Checking whether a property is _not_ empty
* Inverting the truth value of an [if](if.md) statement

{% hint style="info" %}
**Good to know:** Notion is picky, so `!`, `NOT`, and `Not` won't work here. Only the case-sensitive `not` will be accepted.
{% endhint %}

You can also use the function version, `not()`.

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
not true // Output: false

not(true) // Output: false

not empty("Hello") // Output: true

not if(50>40,true,false) // Output: false
```
{% endcode %}

## Example Database

This example database shows a list of applications to join a pirate crew. The captain only wants to hire pirates that **have** powers, and he won’t accept anyone with **snot**-based powers. That’d be gross.

The **Interview** checkbox returns true only if both of those conditions are met. The **Interviews** view filters by this checkbox, showing the captain only the candidates that meet his conditions.

![](<../../.gitbook/assets/Crew Applications.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/fe30cce05d9b477ba762e5f6cc4a677d?v=1ac34c9b85de4b62895bffc2d86d257c" %}

### "Interview" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(not empty(prop("Power")) and not test(prop("Power"), "[Ss]not"), true, false)

// Expanded
if(
	not empty(
		prop("Power")
	) and not test(
		prop("Power"), "[Ss]not"
	), 
	true, 
	false
)
```
{% endcode %}

This formula uses a couple other functions:

* [empty](../functions/empty.md) - tests to see if the **Power** property is empty
* [test](../functions/test.md) - tests to see if the first argument (the **Power** property’s string value) contains the second argument, “Snot”.
  * By writing “\[Ss]” the `test()` function will catch both cases; normally, it is case-sensitive.

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
