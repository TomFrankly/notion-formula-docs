---
description: Learn how to use the Boolean "and" operator in Notion formulas.
---

# and

The **and** operator returns [true](../constants/true.md) if _and only if_ both of its operands have a `true` [Boolean](../../formula-basics/data-types/boolean-checkbox.md) value. Otherwise, it will return [false](../constants/false.md). It accepts [Boolean](../../formula-basics/data-types/boolean-checkbox.md) operands.

**And** is useful for testing that two or more things are true.

{% hint style="info" %}
**Good to know:** Notion is picky, so `&&`, `AND`, and `And` won’t work here. Only the case-sensitive `and` will be accepted.
{% endhint %}

You can also use the function version, `and()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
true and true // Output: true

true and false // Output: false

and(1>0,0<4) // Output: true

if(true and true, "Happy", "Sad") // Output: "Happy"

if(true and false, "Happy", "Sad") // Output: "Sad"

if(5>4 and 1<3, true, false) // Output: true

if(length("Monkey D. Luffy") > 5 and length("Monkey D. Luffy") < 100, true, false) // Output: true
```
{% endcode %}

The `and` operator can also be chained together multiple times:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
4>2 and 3<4 and 5>2 and 7==7 ? true : false // Output: true
```
{% endcode %}

## Example Database

The example database below shows a list of **shore leave requests** from a pirate crew. The captain will only approve a request if **both** are true:

* The request doesn’t fall on one of that crew member’s **watch duty days**
* The crew member has less than $10,000 in **gambling debt**

The **Approved?** formula uses the **and** operator to ensure that both of these conditions are true. If so, it’ll output `true` and the request will be approved. If not, it’ll output `false` and the request will be denied.

![](<../../.gitbook/assets/Shore Leave Requests.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/a163ff267e7c4a4e812016ba5338faf8?v=95184fe8800543afa7cc7ea5ce82f3e7" %}

### "Approved?" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(prop("Gambling Debt") < 10000 and not contains(prop("Watch Duty Days"), formatDate(prop("Request Date"), "dddd")), true, false)

// Expanded
if(
  prop("Gambling Debt") < 10000 
	and 
	not contains(
    prop("Watch Duty Days"),
    formatDate(
      prop("Request Date"),
      "dddd"
    )
  ),
  true,
  false
)
```
{% endcode %}

This formula uses an [if](if.md) statement to check that both of the captain’s conditions are true:

* The first operand checks that the crew member’s gambling debt is `< 10000`
* The second operand checks the request date against the crew member’s assigned watch days:
  * The [contains](../functions/contains.md) function checks to see if the **Request Date’s** day of the week is contained in the **Watch Duty Days** list for each row.
  * The [formatDate](../functions/formatdate.md) function uses the [Moment.js](https://momentjscom.readthedocs.io/en/latest/moment/04-displaying/01-format/) string `dddd` to convert the **Request Date** into a named day of the week (i.e. “**Wednesday**”) so it can be compared against the tags in the **Watch Duty Days** property.
  * Finally, the [not](not.md) operator negates the boolean output of the `contain()` function, ensuring the `and` operator only returns `true` if the **Request Date** DOESN’T match an assigned **Watch Duty Day.**

#### Other formula components used in this example:

{% content-ref url="smaller.md" %}
[smaller.md](smaller.md)
{% endcontent-ref %}

{% content-ref url="if.md" %}
[if.md](if.md)
{% endcontent-ref %}

{% content-ref url="../functions/contains.md" %}
[contains.md](../functions/contains.md)
{% endcontent-ref %}

{% content-ref url="not.md" %}
[not.md](not.md)
{% endcontent-ref %}

{% content-ref url="../functions/formatdate.md" %}
[formatdate.md](../functions/formatdate.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
