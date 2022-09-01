---
description: Learn how to use the empty function in Notion formulas.
---

# empty

The `empty()` function returns [true](../constants/true.md) if its argument is empty, or has a value that equates to empty - including `0` and `false`.

`empty()` accepts all [data types](../../formula-basics/data-types/), including [strings](../../formula-basics/data-types/string.md), [numbers](../../formula-basics/data-types/number.md), [Booleans](../../formula-basics/data-types/boolean-checkbox.md), and [dates](../../formula-basics/data-types/date-data-type.md).

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
empty("") // Output: true

empty(0) // Output: true

empty(false) // Output: true

// Assume a row where the Name property is currently blank
empty(prop("Name")) // Output: true
```
{% endcode %}

`empty()` can be preceded by the [not](../operators/not.md) operator to ensure that a property or value is _not_ empty:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Assume a row where the Name property contains text
not empty(prop("Name")) // Output: true

// The same result can be accomplished with conditional operators
// (Assume the Name property contains text in this row)
empty(prop("Name")) ? false : true // Output: true
```
{% endcode %}

## Example Database

The example database below shows how you can sort sub-tasks by their parent task's due date. This pictured view is simplified for ease-of-use; view the database's **All Properties** tab to see every property at work.

![](<../../.gitbook/assets/Empty Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/empty-0e303017111448ceb798d27e6e58c4f8" %}

### “Parent Due” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(not empty(prop("Parent Task")), prop("Parent Due Rollup"), if(empty(prop("Sub-Tasks")), prop("Due"), if(not empty(prop("Due")), prop("Due"), dateAdd(now(), 100, "years"))))

// Expanded
if(
    not empty(
        prop("Parent Task")
    ), 
    prop("Parent Due Rollup"), 
    if(
        empty(
            prop("Sub-Tasks")
        ), 
        prop("Due"), 
        if(
            not empty(
                prop("Due")
            ), 
            prop("Due"), 
            dateAdd(
                now(),
                100, 
                "years"
            )
        )
    )
)
```
{% endcode %}

This formula uses both `empty()` and `not empty()` in conjunction with multiple [nested if statements](../operators/if.md#nested-if-then-statements) in order to determine a **Parent Due Date.**

The entire database view is then sorted by:

1. Parent Due Date
2. Parent Task Name
3. Due Date

Notice that the formula also calls in a **Parent Due Rollup** property, which is actually configured to pull in the Parent Due Date content of the Parent Task:

![](<../../.gitbook/assets/Parent Due Rollup.png>)

That's right - this is a formula, which pulls in its own output (from other database rows)!

Let's work through what this formula is doing:

1. First, it checks if **Parent Task** is not empty. If so, we know we're dealing with a sub-task, so we output the value of Parent Due Rollup. _Note that Parent Due Rollup's content is determined by the rest of the logic in this formula._
2. If Parent Task _is_ empty, then we check if **Sub-Tasks** is empty as well. If so, we're dealing with a "lone" task - it's not a parent task nor a sub-task. In this case, we output its Due date value.
3. If Sub-Tasks is not empty, then we know we're dealing with a parent task. Next, we check if its **Due** property is not empty.
4. If it does have a date, we output that. If not, we output a standard date of [now](now.md) plus 100 years (using [dateAdd](dateadd.md)). This ensures that parent tasks with no actual due date have a hidden "default" date, enabling sub-tasks to still be sorted underneath them as intended.

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="now.md" %}
[now.md](now.md)
{% endcontent-ref %}

{% content-ref url="dateadd.md" %}
[dateadd.md](dateadd.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
