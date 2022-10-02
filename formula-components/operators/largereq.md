---
description: >-
  Learn how to use the Boolean "larger or equal" (>=) operator in Notion
  formulas.
---

# largerEq

The larger or equal (`>=`) operator returns [true](../constants/true.md) if its left operand is greater than or equal to its right operand. It accepts [numeric](../../formula-basics/data-types/number.md), [date](../../formula-basics/data-types/date-data-type.md), and [Boolean](../../formula-basics/data-types/boolean-checkbox.md) operands.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
number >= number
Boolean >= Boolean
date >= date

largerEq(number, number)
largerEq(Boolean, Boolean)
largerEq(date, date)
```
{% endcode %}

You can also use the function version, `largerEq()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
2 >= 1 // Output: true

42 >= 42 // Output: true

// Boolean values equate to 1 (true) and 0 (false).
true >= false // Output: true

true >= true // Output: true

// For dates, "less than" equates to "before".
now() >= now() // Output: true
```
{% endcode %}

{% hint style="info" %}
**Good to know:** When comparing dates, "larger" = "later".
{% endhint %}

{% hint style="info" %}
**Good to know:** The largerEq (`>=`) operator _cannot_ be chained in a Notion formula. A formula like `3 >= 2 >= 1` won't work. Use the [and](and.md) operator to get around this - e.g. 3 `` >= `2 and 2 >= 1`.
{% endhint %}

## Example Database

This example database records the powerlifting totals for a few lifters and compares them against the USPA standards for different lifting levels. The Level formula outputs the lifter’s current level.

![](<../../.gitbook/assets/Larger or Equal to Database Example - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/largerEq-e0fdb205a61c4bb387c582fbc20c238e" %}

### Explanation

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
prop("Name") + "'s Level is " + ((prop("Total") >= 1642) ? "Elite" : ((prop("Total") >= 1508) ? "Master" : ((prop("Total") >= 1355) ? "Class I" : ((prop("Total") >= 1191) ? "Class II" : ((prop("Total") >= 1041) ? "Class III" : ((prop("Total") >= 903) ? "Class IV" : "Novice"))))))

// Expanded
prop("Name") + "'s Level is " + (
    (prop("Total") >= 1642) ? "Elite" : 
    ((prop("Total") >= 1508) ? "Master" : 
    ((prop("Total") >= 1355) ? "Class I" : 
    ((prop("Total") >= 1191) ? "Class II" : 
    ((prop("Total") >= 1041) ? "Class III" : 
    ((prop("Total") >= 903) ? "Class IV" : "Novice")
    )))))
```
{% endcode %}

This formula uses a series of nested [if-then statements](if.md) (using the conditional operators `?` and `:`) to check the numeric value in the **Total** property against the minimum requirements for [USPA powerlifting levels](https://www.lift.net/2013/05/09/classification-standards-for-raw-elite-uspa/) (specifically, those for the raw 220 weight class).

#### Other formula components used in this example:

{% content-ref url="if.md" %}
[if.md](if.md)
{% endcontent-ref %}

{% content-ref url="add.md" %}
[add.md](add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
