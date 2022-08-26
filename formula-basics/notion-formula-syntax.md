---
description: Learn the basics of Notion's formula syntax.
---

# Notion Formula Syntax

Notion formulas are not written in any previously established programming or scripting language.

They're written in "Notion Formula Syntax" – however, you'll find that syntax is _very_ similar to the syntax used within Microsoft Excel/Google Sheets formulas.

You'll likely also see some similarities to Javascript syntax, though Notion Formula Syntax is far simpler.

{% hint style="info" %}
**Good to know:** Notion formulas must be entered into the formula editor as a one-line formula without line breaks or indentation.

Refer to my guide on [writing complex formulas](the-formula-editor.md#writing-complex-formulas-in-vs-code) to see how you can remove these elements before pasting your formulas from a text editor into Notion's editor.
{% endhint %}

In Notion formulas, parentheses `()` are used to open and close functions:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
abs(-20) // Output: 20
```
{% endcode %}

Commas `,` are used to separate arguments in functions:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
add(34,8) // Output: 42
```
{% endcode %}

Quotation marks `"` are used to:

1. Denote [strings](data-types/string.md)
2. Reference property names within the `prop()` function

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Assume the value of the Name property is "Luffy"
concat("Monkey D. ", prop("Name")) // Output: Monkey D. Luffy
```
{% endcode %}

As in most programming languages, the plus sign `+` can be used for both numeric addition and string concatenation:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
38 + 4 // Output: 42

"Monkey" + "D. " + "Luffy" // Output: Monkey D. Luffy
```
{% endcode %}

There are several other operators, which perform calculations on one or more **operands.**&#x20;

Most operators are **binary operators,** which means they work on two operands:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
10 / 2 // Output: 5

(4 + 5) == 9 // Output: true

9 < 8 // Output: false
```
{% endcode %}

The **unary operators** ([unaryPlus](../formula-components/operators/unaryplus.md) and [unaryMinus](../formula-components/operators/unaryminus.md)) operate on a single operand:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
-(-10) // Output: 10

+"42" // Output: 42 (string converted to a number)
```
{% endcode %}

The **ternary operator** (`?` and `:`) operates on three operands, and can be substituted for the [if function](../formula-components/operators/if.md):

{% code overflow="wrap" lineNumbers="true" %}
```javascript
42 > 25 ? "Yes" : "No" // Output: Yes

if( 42 > 25, "Yes", "No") // Output: Yes
```
{% endcode %}

When performing mathematical operations, operators follow standard mathematical order of operations.&#x20;

Refer to the [operator precedence](../reference/operator-precedence-and-associativity.md) guide (which also defines precedence for [Boolean](data-types/boolean-checkbox.md) operators) for more detail, and remember that you can always use parentheses `()` to specify the order you want:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
4 + 8 / 4 - 2^2 // Output: 2
4 + (8 / 4) - (2^2) // Output: 2

(4 + 8) / (4 - 2) ^ 2 // Output: 3
👇 // simplified
(12) / (4) // Output: 3
```
{% endcode %}

Notion's [formula editor](the-formula-editor.md) includes many [functions](../formula-components/functions/), which are reusable blocks of code that you can call.

Functions accept one or more **arguments,** operate on the data of those arguments using internal logic, and output a result.&#x20;

Arguments must be of the correct [data type](data-types/); otherwise, your formula will throw an [error](../reference/fixing-notion-formula-errors.md).

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// function_name(argument_1, argument_2)

divide(10,2) // Output: 5

// Note that spaces between arguments are optional, but
// commas are required.
concat("My", " ", "Chemical", " ","Romance") 
// Output: My Chemical Romance
```
{% endcode %}

Functions can accept other functions as arguments. The inner-most functions are executed first, and their **output** is used as the argument value for the function that contains them.

{% hint style="info" %}
**Good to know:** Since arguments are strict about [data types](data-types/) (as mentioned above), it can be useful to pass a function as an argument that converts data to the correct type.

Note the use of the [format](../formula-components/functions/format.md) function in Example 2 below. It converts the [numeric](data-types/number.md) output of the [add](../formula-components/operators/add.md) and [multiply](../formula-components/operators/multiply.md) functions to [string](data-types/string.md) output, which is required by the [concat](../formula-components/functions/concat.md) function.

Learn more about this concept in my guide on [converting data types](../reference/converting-data-types.md).
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```javascript
/* Example 1 */
// Compressed
divide(add(8,2), subtract(5,3)) // Output: 5

// Expanded
divide(
    add(8,2),
    subtract(5,3)
)

---

/* Example 2 */
// Compressed
if(equal(add(8,4),multiply(3,4)),concat(format(add(8,4))," and ",format(multiply(3,4))," are equal!"),concat(format(add(8,4))," and ",format(multiply(3,4))," are not equal!"))

// Expanded
if(
    equal(
        add(8,4),
        multiply(3,4)
    ),
    concat(
        format(
            add(8,4)
        ),
        " and ",
        format(
            multiply(3,4)
        ),
        " are equal!"
    ),
    concat(
        format(
            add(8,4)
        ),
        " and ",
        format(
            multiply(3,4)
        ),
        " are not equal!"
    )
)
```
{% endcode %}

**Example 2** in the above code block also demonstrates a significant limitation of Notion formulas. **Formulas cannot internally define variables.** Only properties can be used as variables.

Notion formulas also do **not** support:

* Loops (for, while, etc.)
* Recursion
* Arrays
* Objects
* Custom, reusable functions

You will not find yourself using curly braces `{}` or brackets `[]` in Notion formulas.

{% hint style="info" %}
**Advanced tip:** Since Notion doesn't support these common programming features, you'll find that many complex formulas use [regular expressions](../reference/regular-expressions-in-notion-formulas.md) to do a lot of the heavy lifting.

Additionally, you'll learn to start thinking bigger than a single formula. Many complex tasks will require multiple formula properties, "helper" properties that store variables, etc.
{% endhint %}

Now that you have an overall understanding of how Notion formula syntax works, you should be able to fully understand the details and examples provided for each [constant](../formula-components/constants/), [operator](../formula-components/operators/), and [function](../formula-components/functions/).

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
