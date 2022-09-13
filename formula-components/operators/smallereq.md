---
description: >-
  Learn how to use the Boolean "smaller or equal" (<=) operator in Notion
  formulas.
---

# smallerEq

The smaller or equal (`<=`) operator returns [true](../constants/true.md) if its left operand is less than or equal to its right operand. It accepts [numeric](../../formula-basics/data-types/number.md), [date](../../formula-basics/data-types/date-data-type.md), and [Boolean](../../formula-basics/data-types/boolean-checkbox.md) operands.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
number <= number
Boolean <= Boolean
date <= date

smallerEq(number, number)
smallerEq(Boolean, Boolean)
smallerEq(date, date)
```
{% endcode %}

You can also use the function version, `smallerEq()`.

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
2 <= 3 // Output: true

42 <= 42 // Output: true

// Boolean values equate to 1 (true) and 0 (false).
false <= true // Output: true

true <= true // Output: true

// For dates, "less than" equates to "before".
now() <= now() // Output: true
```
{% endcode %}

{% hint style="info" %}
**Good to know:** When comparing dates, "larger" = "later".
{% endhint %}

## Example Database

This example database is an _extremely_ simplified tax calculator. It uses the **Gross Income** for each person to determine that person’s tax bracket, and outputs their total tax liability in the **Total Tax** property.

{% hint style="warning" %}
_**Note:** This example uses the_ [_2022 Federal income tax brackets_](https://www.irs.gov/newsroom/irs-provides-tax-inflation-adjustments-for-tax-year-2022)_, but does not include deductions, exemptions, or credits._
{% endhint %}

![](<../../.gitbook/assets/Tax Brackets - SmallerEq Operator - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/smallerEq-50fa1b35dc2f4c2793ae8dc55823167d" %}

### “Total Tax” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
(prop("Gross Income") <= 10275) ? (prop("Gross Income") * 0.1) : ((prop("Gross Income") <= 41775) ? (prop("Gross Income") * 0.12 + 1027.5) : ((prop("Gross Income") <= 89075) ? (prop("Gross Income") * 0.22 + 4807.5) : ((prop("Gross Income") <= 1.7005e+5) ? (prop("Gross Income") * 0.24 + 15213.5) : ((prop("Gross Income") <= 2.1595e+5) ? (prop("Gross Income") * 0.32 + 34657.5) : ((prop("Gross Income") <= 5.399e+5) ? (prop("Gross Income") * 0.35 + 49335.5) : (prop("Gross Income") * 0.37 + 1.62718e+5))))))

// Expanded
(prop("Gross Income") <= 10275) ? (prop("Gross Income") * 0.1) : 
((prop("Gross Income") <= 41775) ? (prop("Gross Income") * 0.12 + 1027.5) : 
((prop("Gross Income") <= 89075) ? (prop("Gross Income") * 0.22 + 4807.5) : 
((prop("Gross Income") <= 1.7005e+5) ? (prop("Gross Income") * 0.24 + 15213.5) : 
((prop("Gross Income") <= 2.1595e+5) ? (prop("Gross Income") * 0.32 + 34657.5) : 
((prop("Gross Income") <= 5.399e+5) ? (prop("Gross Income") * 0.35 + 49335.5) : 
(prop("Gross Income") * 0.37 + 1.62718e+5))))))
```
{% endcode %}

This formula uses a series of [nested if-then statements](if.md#nested-if-then-statements) (using the conditional operators `?` and `:`) to "step through" a series of income caps.

For example: `(prop("Gross Income") <= 10275) ? (prop("Gross Income") * 0.1)` simply checks to see if **Gross Income** is less than or equal to $10,275, which is the cap for the 10% tax bracket.

If so, then Gross Income is multiplied by 10% to return the total tax. If not, then the formula goes to the next bracket, checks Gross Income against its cap, and so on.

#### Other formula components used in this example:

{% content-ref url="if.md" %}
[if.md](if.md)
{% endcontent-ref %}

{% content-ref url="multiply.md" %}
[multiply.md](multiply.md)
{% endcontent-ref %}

{% content-ref url="add.md" %}
[add.md](add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
