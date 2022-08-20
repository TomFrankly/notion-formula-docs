---
description: Learn how to use the "if" operator in Notion formulas.
---

# if

The `if()` operator allows you to write **if-then** statements within a Notion formula. If-then statements, also called **conditional statements,** contain:

* The condition - a statement to be evaluated for **truthiness** (i.e. “is it true?”)
* The “then” statement - a statement that is executed if the condition is true
* The “else” statement - a statement that is executed if the condition is false

{% hint style="info" %}
`if()` looks like a function in Notion, but it’s actually considered an operator because an if-then statement can be written with ? and : instead of the `if()` syntax.
{% endhint %}

## Example Formulas

### Simple String Comparison

This formula compares the output of a Select property called **Type** (which has a data type of String) with the string value “Mammal”. If the two are equal, it outputs [true](../constants/true.md); otherwise, [false](../constants/false.md).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
if(prop("Type")=="Mammal",true,false)
```
{% endcode %}

#### Shorthand Syntax

If-then statements can also be written in a shorthand syntax. This uses `?` and `:` as shorthand for `if()`.

* Everything left of the `?` is the statement being evaluated.&#x20;
* Between `?` and `:` is the output if the evaluated statement is true.
* Right of the `:` is the output if the evaluated statement is false.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
[condition] ? ['then' statement] : ['else' statement]
```
{% endcode %}

Here’s our example formula from above, re-written using shorthand:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
prop("Type")=="Mammal" ? true : false
```
{% endcode %}

Taken together, `?` and `:` form what’s called the **conditional (or ternary) operator.** It’s the only operator that takes in three _operands,_ which are objects that are being operated on.&#x20;

Most operators only work with two operands - for example:

* `2 + 5` - the [add](add.md) (`+`) operator is working on `2` and `5`

Check out the two formula properties in this example database; one uses the normal if-then syntax, while the other uses shorthand. You’ll see that their output is the same.

![](<../../.gitbook/assets/Animal Types.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/e4dfb1804cf7456f802a473af1db6fdc?v=27299e0aba994ed9bf16b65f44de41c2" %}

**Other formula components used in this example:**

{% content-ref url="equal.md" %}
[equal.md](equal.md)
{% endcontent-ref %}

### Nested If-Then Statements

{% hint style="info" %}
Writing nested if-statements can become difficult in Notion’s default formula editor. If you’re writing a long formula, I recommend writing it in a free code editor such as [VS Code](https://code.visualstudio.com/), and then minifying it using [Excel Formula Beautifier](https://www.excelformulabeautifier.com/) so it can be pasted into Notion (remove the = sign at the beginning of the formula output if it exists before pasting).
{% endhint %}

Notion does not support the “**else if”** statement that is support by more popular scripting and programming languages, such as [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else#description).

With an **else if** statement, you could write code like this (in Javascript):

{% code overflow="wrap" lineNumbers="true" %}
```jsx
/* This is Javascript code that won't work in a Notion formula */

if (x<13) {
	/* do one thing */
} else if (x<19) {
	/* do another thing */
} else {
	/* do the last thing */
}
```
{% endcode %}

In Notion, what we have to do instead is create **nested if-then statements,** like so:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
if(
	prop("Age") < 13,
	"Child",
	if(
		prop("Age") < 19,
		"Teenager",
		"Adult"
	)
)
```
{% endcode %}

* If the numeric value of a row’s **Age** property is less than 13, the _then_ portion of the if-then statement is executed and the formula returns `Child`.
* If not, the _else_ statement is executed. In this case, our else statement is yet another **if-then statement** - hence, it’s a _nested if-then statement._
  * Within the nested statement, the same logic applies. The condition is tested; if **Age** is less than 19, the _then_ statement executes and outputs `Teenager`. If not, the _else_ statement is executed and outputs `Adult`.

Here’s the logic tree for this nested if-then statement:

{% embed url="https://whimsical.com/nested-if-then-statement-ApM11ByUEfRA77SKwUFhMG" %}

Here’s a compressed version you can paste into a Notion formula property:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// if() syntax
if( prop("Age") < 13, "Child", if( prop("Age") < 19, "Teenager", "Adult" ) )

// ? syntax
prop("Age") < 13 ? "Child" : prop("Age") < 19 ? "Teenager" : "Child"
// Notion will refrormat this to:
(prop("Age") < 13) ? "Child" : ((prop("Age") < 19) ? "Teenager" : "Child")
```
{% endcode %}

{% hint style="info" %}
**Good to know:** As you can see in the code block above, you can create nested statements with the conditional operators `?` and `:` as well.&#x20;

When using these, you don't even need to add your own parentheses `()` to create your nested statement; Notion will add them after you exit the formula editor.
{% endhint %}

In the example database below, you can see the nested if-statements at work:

![](<../../.gitbook/assets/Stages of Life.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/3872d10416354078ab87b10baef88370?v=f38aa4a1196f4479ab975965f7d5b36a" %}

**Other formula components used in this example:**

{% content-ref url="smaller.md" %}
[smaller.md](smaller.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
