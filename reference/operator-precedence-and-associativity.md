---
description: Learn about operator precedence and associativity in Notion formulas.
---

# Operator Precedence and Associativity

Notion [operators](../formula-components/operators/) have a specific operator precedence order. Operators with a higher precedence (11 being the highest) will have their logic executed before operators of lower precedence.

Operators at the same precedence level are executed either left-to-right or right-to-left, depending on their associativity.

Refer to the table below to see the precedence level and associativity of each operator.

<table><thead><tr><th data-type="number">Precedence</th><th>Operator Name</th><th>Associativity</th><th>Symbol</th></tr></thead><tbody><tr><td>11</td><td>Parentheses</td><td>N/A</td><td><code>()</code></td></tr><tr><td>10</td><td>Not</td><td>right-to-left</td><td><code>not</code></td></tr><tr><td>9</td><td>Exponentiation (pow)</td><td>right-to-left</td><td><code>^</code></td></tr><tr><td>8</td><td>unaryPlus, unaryMinus</td><td>right-to-left</td><td><code>+</code>, <code>-</code></td></tr><tr><td>7</td><td>multiply, divide</td><td>left-to-right</td><td><code>*</code>, <code>/</code></td></tr><tr><td>6</td><td>add, subtract</td><td>left-to-right</td><td><code>+</code>, <code>-</code></td></tr><tr><td>5</td><td>larger, largerEq, smaller, smallerEq</td><td>N/A</td><td><code>></code>, <code>>=</code>, <code>&#x3C;</code>, <code>&#x3C;=</code></td></tr><tr><td>4</td><td>unequal, equal</td><td>N/A</td><td><code>!=</code>, <code>==</code></td></tr><tr><td>3</td><td>And</td><td>left-to-right</td><td><code>and</code></td></tr><tr><td>2</td><td>Or</td><td>left-to-right</td><td><code>or</code></td></tr><tr><td>1</td><td>Conditional (if)</td><td>right-to-left</td><td><code>... ? ... : ...</code></td></tr></tbody></table>

Since parentheses `()` have the highest precedence in a Notion formula, you can use them to define a specific order of operations within any formula.

It's also good to understand that **associativity** can be thought of as an implied _default_ setting of parentheses. For example:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Multiply has left-to-right associativity. The following are equivalent:
2 * 3 * 4 // Output: 24
(2 * 3) * 4 // Output: 24

// Exponentiation has right-to-left associativity (the "Tower Rule"). The following are equivalent:
2 ^ 3 ^ 2 // Output: 512
2 ^ (3 ^ 2) // Output: 512
```
{% endcode %}

Certain operators cannot be **chained** in Notion formulas; thus, they do not have associativity. These are marked with "N/A" in the associativity column.

For example, the following formulas will not work in Notion:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Invalid
1 > prop("Number") > 5

// Valid
1 > prop("Number") and prop("Number") < 5 // Output: True

---

// Invalid
1 == +true == +"1"

// Valid
1 == +true and 1 == +"1" // Output: True
```
{% endcode %}

If you want to understand operator precedence and associativity more thoroughly, I'll recommend reading through the Operator Precedence guide for JavaScript on MDN's web docs:

{% embed url="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence" %}

<details>

<summary>Operator Precedence/Associativity Proofs</summary>

Much of my original research on Notion's operator precedence and associativity was based off of the precedence/associativity in JavaScript, for which I've linked the MDN doc above.

However, I also worked to prove that these precedence/associativity rules held for Notion formulas. Here are a few proofs for some of the trickier relationships. Feel free to paste them into a Notion formula editor and see how they work for yourself!

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Proof: Inequality (!=) has higher precedence than "and"
(false and true) != true and true // Output: True
false and true != true and true // Output: False

// Proof: "Not" operator has highest precedence other than ()
1==1 and 2^2==4 // Output: True
1 == 1 and not (2 ^ 2) == 4 // Type Mismatch: (2^2) is not a Checkbox
1 == 1 and not ((2 ^ 2) == 4) // Output: False

// Proof: right-to-left associativity of "Not"
not not true // Output: True (LTR would result in an error)
```
{% endcode %}

</details>

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
