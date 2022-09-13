---
description: Learn how to use the exponentiation (^) operator in Notion formulas.
---

# pow

The **power (`^`)** operator (also known as the _exponentiation_ operator) allows you to raise a [number](../../formula-basics/data-types/number.md) to a higher power.

In technical terms, it raises the first operand to the power of the second operand.

In Notion, the `^` operator has a higher [operator precedence](../../reference/operator-precedence-and-associativity.md) than the [unaryPlus](unaryplus.md) and [unaryMinus](unaryminus.md) operators, and has **right-to-left** associativity.

You can also use the function version, `pow()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
3 ^ 4 // Output: 81

pow(4,3) // Output: 64

2 ^ 2 ^ 3 // Output: 256 - evaluates as 2 ^ (2 ^ 3)
```
{% endcode %}

<details>

<summary>Useful exponent/power rules to remember</summary>

* $$x^0 = 1$$
* $$(x^a)^b = x^{ab}$$
* $$x^{a^b} = x^{(a^b)}$$ _(not all languages respect this, but Notion does)_
* $$x^a * y^a = (xy)^a$$
* $$x^a / y^a = (x/y)^a$$
* $$x^a * x^b = x^{a+b}$$
* $$x^a / x^b = x^{a-b}$$

Learn more and see examples: [Rules of Exponents (Brilliant.org)](https://brilliant.org/wiki/exponential-functions-properties/)

</details>

### Exponent Associativity

In Notion, the `^` operator has **right-to-left** [associativity](../../reference/operator-precedence-and-associativity.md#operator-associativity), which means that `x ^ y ^ z` is evaluated as `x ^ (y ^ z)`.

{% code overflow="wrap" lineNumbers="true" %}
```javascript
4 ^ 3 ^ 2 == 262,144

4 ^ (3 ^ 2) == 4 ^ 9 == 262,144

(4 ^ 3) ^ 2 == 64 ^ 2 == 4,096

// Here's that last one according to the (x^a)^b == x^(ab) "Power Rule":

(4 ^ 3) ^ 2 == 4 ^ (3*2) == 4 ^ 6 = 4,096
```
{% endcode %}

{% hint style="warning" %}
Not every programming and scripting language uses right-to-left associativity for serial exponentiation. [Here's a write-up comparing the methods for many popular languages.](https://codeplea.com/exponentiation-associativity-options) Even though standard mathematical notation has the **"Tower Rule"**, where $$x^{a^b} = x^{(a^b)}$$(aka: "Work top-down"), the computer science community has not come to a strong consensus on whether `x^y^z` should be interpreted in the same way.
{% endhint %}

### Working with Unary Operators

{% hint style="info" %}
**Good to know:** Don't want to memorize these precedence rules? Just use parentheses `()` to make the order of your operations explicit.
{% endhint %}

In Notion, the [unaryPlus](unaryplus.md) operator converts [strings](../../formula-basics/data-types/string.md) and [Booleans](../../formula-basics/data-types/boolean-checkbox.md) to numbers, while the [unaryMinus](unaryminus.md) operator inverts the sign of its operand.

When combining these operators with the `^` operator in Notion, it's useful to understand the following rules:

1. The `^` operator has a higher [operator precedence](../../reference/operator-precedence-and-associativity.md) than the unary operators. This is opposite to [JavaScript's operator precedence!](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator\_Precedence#table) _(Though in JavaScript this is irrelevant, because the language_ [_doesn't allow for ambiguous unary operator usage_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Exponentiation) _in exponentiation)._
2. Notion is smart and will allow for unaryPlus type conversion on the exponent, but will wrap the conversion operation in `()` automatically.
3. Notion will _not_ allow for automatic unaryPlus type conversion on the base number - e.g. `+"8"^2` will throw a type mismatch error.
4. If you write a negative exponent into a formula, Notion parses it as a true negative value instead of a unaryMinus (`-`) operator appended to a number. Your formula will also be re-written to `x ^ (-2)` so the exponent is explicitly defined as negative.
5. &#x20;When using unaryMinus on a base number, Notion will parse it as `-(x^y)`, not `(-x)^y`. _Note that this can result in mathematically incorrect answers depending on your use case - see_ [_Negative Base Numbers_](pow.md#negative-base-numbers) _below._

{% code overflow="wrap" lineNumbers="true" %}
```javascript
-2 ^ 2 // Output: -4 - Notion parses this as -(2^2)

4 ^ -2 // Re-written to 4 ^ (-2), outputs 0.0625
4 ^ -(2) // Re-written to 4 ^ (-2), outputs 0.0625
4 ^ -(-2) // Re-written to 4 ^ (-(-2)), outputs 16

+"8" ^ 2 // Type mismatch error

(+"8") ^ 2 // Output: 64

8 ^ +"-2" // Re-written to 8 ^ (+"-2"), outputs 0.015625

2 ^ +false// Re-written to 2 ^ (+false), outputs 1
```
{% endcode %}

### Negative Base Numbers

If you type `-2^4` directly into Notion's formula box, you'll get an output of **-16**. Assuming you're intending to pass the actual base number `-2`, this answer is incorrect! The true answer is **16**.

Remember that exponentiation is just repeated multiplication of the base number. Therefore:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
-2^4 == (-2)(-2)(-2)(-2) == (4)(-2)(-2) == (-8)(-2) == 16
```
{% endcode %}

So why does `-2^4` return -16 in a Notion formula?

This happens because when you type `-` directly into a Notion formula, you're using the [unaryMinus](unaryminus.md) operator. If you type `-2`, you're _not_ simply typing a negative number into your formula. Rather, you're creating an expression equivalent to `-(2)`.

This distinction is important because exponentiation (`^`) has a higher [operator precedence](../../reference/operator-precedence-and-associativity.md) in Notion than unaryMinus, as noted above.

This means that typing `-2^4` is equivalent to `-(2^4)`!

If your intention is to express a negative base number, you'll need to type `(-2)^4` instead.

{% hint style="info" %}
Negative base numbers passed via a property (e.g. `prop("num")`) will be evaluated correctly, since they're actually passing a negative value, rather than adding a hard-coded unaryMinus (`-`) operator to your formula.
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```javascript
-2^4 // Output: -16 - Notion parses this as -(2^4)

(-2)^4 // Output 16 - Notion parses this as (-2)^4

prop("num") == -2
prop("num")^4 // Output: 16 - Notion parses this as (-2)^4
```
{% endcode %}

{% hint style="warning" %}
**Note:** This convention does not apply to all programming and scripting languages. For example, in Microsoft Excel, the formula `=-2^4` evaluates to **16,** as does `=A1^4` where the value of `A1` is **2.**
{% endhint %}

## Example Database

The table below shows exponentiation at work in a Notion database.

![](<../../.gitbook/assets/Power Raiser.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/pow-fd0d589c9dce48bca46863a4034a5290" %}

### "Power" Property Formula:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
prop("Base") ^ prop("Exponent")
```
{% endcode %}

Instead of using hard-coded numbers, I’ve called in each property using the `prop()` function.

### Further Reading

* [Exponents and the Rules for Exponents (MTSU)](https://www.mtsu.edu/faculty/dotts/exponent-rules.php)
* [JavaScript exponentiation unary operator design decision (Stack Overflow)](https://stackoverflow.com/questions/47068812/javascript-exponentiation-unary-operator-design-decision)

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
