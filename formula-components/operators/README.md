---
description: A reference list of all operators available for use in Notion formulas.
---

# Operators

Operators are symbols that tell Notion's formula engine to perform specific operations.

Here's a very simple example:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
2 + 2
```
{% endcode %}

This statement uses the [add](add.md) (`+`) operator to perform addition on two numbers. This formula will return a result of `4`.

The numbers on each side of the `+` operator are called **operands.** Operands are the discrete data objects that are either evaluated or manipulated by the operator.

In Notion formulas, operands have one of four [data types](../../formula-basics/data-types/) - [string](../../formula-basics/data-types/string.md), [number](../../formula-basics/data-types/number.md), [Boolean (checkbox)](../../formula-basics/data-types/boolean-checkbox.md), and [date](../../formula-basics/data-types/date-data-type.md).&#x20;

Operands can be hard-coded:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
"Monkey D. Luffy will be " + "King of the Pirates!"
```
{% endcode %}

They can also pass data from another database property:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
prop("First Name") + prop("Last Name")
```
{% endcode %}

You can also mix and match:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
prop("First Name") + " " + prop("Last Name") + " will be King of the Pirates!"
```
{% endcode %}

{% hint style="info" %}
**Good to know:** Notion's formula engine does not do automatic type conversion, so binary operators (operators with two operands) must have operands of the same data type.

E.g. `2 + "2"` will throw a **Type Mismatch** error because one operand is a [number](../../formula-basics/data-types/number.md) and the other is a [string](../../formula-basics/data-types/string.md). You must [convert](../../reference/converting-data-types.md) one or the other so they are of the same type.
{% endhint %}

Notion's formula editor provides three types of operators:

1. Mathematical operators
2. Logical operators
3. Comparison operators
4. Special Operators

## Mathematical Operators

Mathematical operators allow you to do math on numbers.&#x20;

Here are all the mathematical operators Notion provides. Note that Notion also provides a [function](../functions/) version of each one, which I've listed in the reference table.

| Operator                    | Symbol | Function Version | Example               |
| --------------------------- | ------ | ---------------- | --------------------- |
| [add](add.md)               | `+`    | `add()`          | `2 + 2`               |
| [subtract](subtract.md)     | `-`    | `subtract()`     | `4 - 2`               |
| [multiply](multiply.md)     | `*`    | `multiply()`     | `5 * 5`               |
| [divide](divide.md)         | `/`    | `divide()`       | `21 / 3`              |
| [pow](pow.md)               | `^`    | `pow()`          | `2 ^ 3`               |
| [mod](mod.md)               | `%`    | `mod()`          | `12 % 5`              |
| [unaryMinus](unaryminus.md) | `-`    | `unaryMinus()`   | `-4` (same as `-(4))` |

## Logical Operators

Logical operators return a Boolean value, and often allow you to combine and evaluate multiple expressions.

Notion provides three logical operators.

{% hint style="info" %}
**Good to know:** Notion is picky about how you must write logical operators. Only the listed symbols will work, and they are case-sensitive.

E.g. You must use `and` for the [and](and.md) operator - `And`, `AND`, and `&&` will not work in Notion.
{% endhint %}

| Operator      | Symbol | Function Version | Example              |
| ------------- | ------ | ---------------- | -------------------- |
| [and](and.md) | `and`  | `and()`          | `2 > 3 and 4 < 8`    |
| [or](or.md)   | `or`   | `or()`           | `2 > 1 or 6 > 5`     |
| [not](not.md) | `not`  | `not()`          | `not empty("Hello")` |

## Comparison Operators

Comparison operators allow you to compare operands that share a data type.

Notion provides six comparison operators:

| Operator                  | Symbol | Function Version | Example  |
| ------------------------- | ------ | ---------------- | -------- |
| [equal](equal.md)         | `==`   | `equal()`        | `2 == 2` |
| [unequal](unequal.md)     | `!=`   | `unequal()`      | `4 != 2` |
| [larger](larger.md)       | `>`    | `larger()`       | `5 > 3`  |
| [largerEq](largereq.md)   | `>=`   | `largerEq()`     | `4 >= 4` |
| [smaller](smaller.md)     | `<`    | `smaller()`      | `6 < 9`  |
| [smallerEq](smallereq.md) | `<=`   | `smallerEq()`    | `9 <= 9` |

## Special Operators

Notion also provides two special operators that don't fit neatly into the categories above.

The [unaryPlus](unaryplus.md) operator is the only operator that does [type conversion](../../reference/converting-data-types.md); it converts [strings](../../formula-basics/data-types/string.md) and [Booleans](../../formula-basics/data-types/boolean-checkbox.md) to [numbers](../../formula-basics/data-types/number.md) (use [toNumber](../functions/tonumber.md) or [timestamp](../functions/timestamp.md) if you need to convert a [date](../../formula-basics/data-types/date-data-type.md) to a number).

The [if](if.md) operator - also known as the ternary operator - lets you create if-then statements and branching logic in Notion formulas.

| Operator                  | Symbol      | Function Version | Example               |
| ------------------------- | ----------- | ---------------- | --------------------- |
| [unaryPlus](unaryplus.md) | `+`         | `unaryPlus()`    | `+"3"` = `3`          |
| [if](if.md)               | `?` and `:` | `if()`           | `2==2 ? true : false` |

## Operator Precedence

Notion formulas can contain many operators, which can let you solve complex problems.

For example:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Output: true
-((+"5")^2) < 20 - 10 ? true : false
```
{% endcode %}

When multiple operators are present in a Notion formula, their order of execution is determined by Notion's operator precedence rules:

{% content-ref url="../../reference/operator-precedence-and-associativity.md" %}
[operator-precedence-and-associativity.md](../../reference/operator-precedence-and-associativity.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
