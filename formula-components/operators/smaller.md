---
description: Learn how to use the Boolean "smaller" (<) operator in Notion formulas.
---

# smaller

The smaller (`<`) operator returns [true](../constants/true.md) if its left operand is less than its right operand. It accepts [numeric](../../formula-basics/data-types/number.md), [date](../../formula-basics/data-types/date-data-type.md), and [Boolean](../../formula-basics/data-types/boolean-checkbox.md) operands.

You can also use the function version, `smaller()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
2 < 1 // Output: false

42 < 50 // Output: true

// Boolean values equate to 1 (true) and 0 (false).
false < true // Output: true

true < true // Output: false

// For dates, "less than" equates to "before".
now() < dateAdd(now(), 1, "months") // Output: true
```
{% endcode %}

{% hint style="info" %}
**Good to know:** When comparing dates, "larger" = "later".
{% endhint %}

## Example Database

The example database below tracks votes amongst a pirate crew. For each issue, a quorum must be reached; at least 3 members must vote. Once a quorum is reached, only proposals that receive more **Yays** than **Nays** will be passed and enacted.

The **Result** formula displays the status of each proposal.

![](<../../.gitbook/assets/Vote Tracker - Smaller Operator Example - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/smaller-2a187281656048f2a55cf6e464eab556" %}

### “Result” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
(+((not empty(prop("Luffy"))) ? true : false) + +((not empty(prop("Nami"))) ? true : false) + +((not empty(prop("Sanji"))) ? true : false) + +((not empty(prop("Zoro"))) ? true : false) < 3) ? "✋ Quorum Not Reached!" : ((+replaceAll(replaceAll(prop("Luffy"), "Nay", "-1"), "Yay", "1") + +replaceAll(replaceAll(prop("Nami"), "Nay", "-1"), "Yay", "1") + +replaceAll(replaceAll(prop("Sanji"), "Nay", "-1"), "Yay", "1") + +replaceAll(replaceAll(prop("Zoro"), "Nay", "-1"), "Yay", "1") < 1) ? "👎 Rejected" : "👍 Passed")

// Expanded
(
    +((not empty(prop("Luffy"))) ? true : false) + 
    +((not empty(prop("Nami"))) ? true : false) + 
    +((not empty(prop("Sanji"))) ? true : false) + 
    +((not empty(prop("Zoro"))) ? true : false) < 3
    ) ? 
    "✋ Quorum Not Reached!" : 
    (
        (+replaceAll(replaceAll(prop("Luffy"), "Nay", "-1"), "Yay", "1") + 
        +replaceAll(replaceAll(prop("Nami"), "Nay", "-1"), "Yay", "1") + 
        +replaceAll(replaceAll(prop("Sanji"), "Nay", "-1"), "Yay", "1") + 
        +replaceAll(replaceAll(prop("Zoro"), "Nay", "-1"), "Yay", "1") < 1) ? 
        "👎 Rejected" : 
        "👍 Passed"
)
```
{% endcode %}

This vote tracker works by giving each group member their own **Yay/Nay** property. A **Select** property is used because there are actually _three_ potential states for each crew member’s vote:

1. Yay
2. Nay
3. Abstained/didn’t vote

Therefore, a [Boolean/Checkbox](../../formula-basics/data-types/boolean-checkbox.md) property won’t work here.

The formula first checks that each member’s vote is not empty, using the [empty](../functions/empty.md) function and the [not](not.md) operator. “Not empty” returns a value of `true`, which is converted to a score of `1` using [unaryPlus](unaryplus.md). Similarly, an empty property will return a `false` value, which is converted to `0`.

The scores are added up, and if they total less than three (`< 3`), the formula outputs **“✋ Quorum Not Reached!”**

If they total 3 or higher, we move to the “then” clause, which is a [nested if-then statement](if.md#nested-if-then-statements).

Here, we use a pair of nested [replaceAll](../functions/replaceall.md) functions to convert each member’s vote into a score: `(+replaceAll(replaceAll(prop("Luffy"), "Nay", "-1"), "Yay", "1")`.

`replaceAll()` is a function that searches a string for a pattern, then replaces **all** instances of that pattern with another pattern:

* The first `replaceAll()` searches the voter’s property (e.g. `prop("Luffy")`) for “Nay”. If found, “Nay” is converted to “-1” (which is a [string](../../formula-basics/data-types/string.md) value at this point).
* The second (outer) `replaceAll()` searches the result of the inner `replaceAll()` (which will either contain “Yay” or “-1” at this point) for “Yay”. If found, “Yay” is converted to “1”.
* Now the vote’s text has been turned _either_ to “-1” or “1”.

Next, the `+` ([unaryPlus](unaryplus.md)) operator converts this numeric string to an actual [number](../../formula-basics/data-types/number.md). This is done for each voter’s property, and finally all the scores are added up.

If the score is less than 1 (`<1`), then the formula outputs, **"👎 Rejected"**. If it is 1 or greater, it outputs, **"👍 Passed"**.

#### Other formula components used in this example:

{% content-ref url="unaryplus.md" %}
[unaryplus.md](unaryplus.md)
{% endcontent-ref %}

{% content-ref url="if.md" %}
[if.md](if.md)
{% endcontent-ref %}

{% content-ref url="../functions/replaceall.md" %}
[replaceall.md](../functions/replaceall.md)
{% endcontent-ref %}

{% content-ref url="not.md" %}
[not.md](not.md)
{% endcontent-ref %}

{% content-ref url="../functions/empty.md" %}
[empty.md](../functions/empty.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
