---
description: Learn how to use the multiplication (*) operator in Notion formulas.
---

# multiply

The **multiply (`*`)** operator allows you to multiply two [numbers](../../formula-basics/data-types/number.md) together and get their product.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
number * number
multiply(number, number)
```
{% endcode %}

The `*` operator follows the standard mathematical order of operations (PEMDAS). For more detail, see [Operator Precedence](../../reference/operator-precedence-and-associativity.md).

You can also use the function version, `multiply()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
12 * 4 // Output: 48

multiply(12,-4) // Output: -48
```
{% endcode %}

### Working with 3 or More Operands

Since **multiply** is a binary operator, it can only work on two _operands -_ the objects which are being operated on ([if](if.md) - the _ternary operator -_ is the only operator that works on three operands).

If you need to work with more than two operands, the shorthand `*` is by far the easiest way to do it.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
4 * 5 * 5 // Output: 100

multiply(multiply(4,5),5) // Output: 100
```
{% endcode %}

<details>

<summary>Can I switch the order of the numbers in a multiplication statement?</summary>

Yes! Remember that the [commutative property of multiplication](https://www.khanacademy.org/math/cc-sixth-grade-math/cc-6th-factors-and-multiples/properties-of-numbers/a/properties-of-multiplication) states that the factors in a multiplication problem can be switched around without changing the final product.

</details>

## Example Database

The example database below shows the interest owned by three pirates who smartly invest some of their savings.&#x20;

The **Interest Earnings** formula shows the total amount of interest that their investment generates over a number of years, given a specific interest rate.

![](<../../.gitbook/assets/Interest Calculator.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/multiply-90dfbe43a01a4c128473987a270f45a6" %}

This example uses the simple interest formula $$Prt$$, where:

* $$P$$ is the principal
* $$r$$ is the rate of interest converted to a decimal (e.g. 7% is converted to 0.07)
* $$t$$ is the number of period (in this case, years)

<details>

<summary>Note: This formula only returns the total interest earned.</summary>

To get a final balance (principal + simple interest), you’d use the formula $$A=P(1+rt)$$.

See that example at the [Simple Interest Calculator](broken-reference) database, or learn more with this [Calculator Soup calculator](https://www.calculatorsoup.com/calculators/financial/simple-interest-plus-principal-calculator.php).

</details>

### "Interest Earnings" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
prop("Investment") * prop("Interest Rate") * prop("Years")
```
{% endcode %}

Instead of using hard-coded numbers, I’ve called in each property using the `prop()` function.

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
