---
description: >-
  Learn the definition of a Notion formula and what formulas can do in your
  databases.
---

# What is a Notion Formula?

Notion formulas are bits of code that can make your Notion databases much more useful.

Formulas in Notion are like a limited programming language. They're written and used in [Formula properties](https://learn.thomasjfrank.com/notion-formula-reference/) within Notion databases ([learn about databases with my complete beginner's guide](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/)).

![](<.gitbook/assets/First Notion Formula Example.png>)

Formulas can take in data from all other database properties, process it using [constants](formula-components/constants/), [operators](formula-components/operators/), and built-in [functions](formula-components/functions/), and then output new data.

Using formulas, you can do things in your Notion databases that are otherwise impossible.

{% hint style="info" %}
This site is a **comprehensive** reference for creating, using, and debugging Notion formulas. Since Notion launched, it has lacked a full reference for the formulas feature. This is that reference.&#x20;

_Every_ formula [constant](formula-components/constants/), [operator](formula-components/operators/), and [function](formula-components/functions/) has been fully documented with example code and one or more working example databases, complete with **templates** you can duplicate.

You'll also find reference guides on things like [operator precedence](reference/operator-precedence-and-associativity.md), [data type conversion](reference/converting-data-types.md), [debugging](reference/debugging-formulas.md), and [regular expressions](reference/regular-expressions-in-notion-formulas.md).
{% endhint %}

## A Formula Example

Let's say you're a sales manager with several existing clients. You want to make sure you check in with each client every three months.

Notion formulas will let you create a database view like this (**assume "today" is August 18, 2022** - the day I wrote this guide):

![](<.gitbook/assets/Client Dashboard - Notion Formulas Example.png>)

**View and duplicate this example:**

{% embed url="https://thomasfrank.notion.site/2d4ed3716253411fabcc837ea731f457?v=eefcad689529410da49aea98bb810735" %}

Not only is your **Next Check-In** date automatically calculated based on your **Last Check-In,** but the view is also grouped (using Notion's [grouping feature](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#grouping)) so that you can easily see any check-ins that need to happen within the next seven days.

Two formulas power this database view: **Next Check-In** and **Next  7 Days.**

The Next Check-In formula looks at the date set in the **Last Check-In** property and calculates the next date by adding three months. To accomplish this, it uses the [dateAdd](formula-components/functions/dateadd.md) function.

![](<.gitbook/assets/Next Check-In.png>)

{% code overflow="wrap" lineNumbers="true" %}
```javascript
dateAdd(prop("Last Check-In"), 3, "months")
```
{% endcode %}

The Next 7 Days formula is slightly more complex. Using the [if function](formula-components/operators/if.md), it uses branching logic to output one of two different strings.

If the date displayed in Next Check-In is less than eight days away (from today's date), then the formula outputs, "Next 7 Days".

Otherwise, it outputs, "More than 7 Days Out".

To determine how far out the Next Check-In date is, we use the [dateBetween](formula-components/functions/datebetween.md) function as the first argument in our if-statement.

![](<.gitbook/assets/Next 7 Days.png>)

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Compressed
if(dateBetween(prop("Next Check-In"), now(), "days") < 8, "Next 7 Days", "More than 7 Days Out")

// Expanded
if(
    dateBetween(
        prop("Next Check-In"), 
        now(), 
        "days"
    ) < 8, 
    "Next 7 Days", 
    "More than 7 Days Out"
)
```
{% endcode %}

Now that we have a formula which can output two different strings of text, we use them in this database view's **Group By** setting:

![](<.gitbook/assets/Grouping Settings.png>)

## Formula Terms

Throughout this reference, I'll mention many different terms related to Notion formulas. Here are a few of the most important terms and what they mean.

### Formula Components

I use the term "components" to collectively refer to the following tools that you have at your disposal when constructing formulas:

* [Properties](formula-basics/reference-properties-in-formulas.md) - these are the other properties that exist in your database.
* [Constants](formula-components/constants/) - mathematical constants $$e$$​ and $$π$$​, plus the Boolean values true and false.
* [Operators](formula-components/operators/) - symbols that perform operations on 1-3 operands. Includes mathematical operators (such as [add](formula-components/operators/add.md)), Boolean operators (such as [not](formula-components/operators/not.md)), and the [ternary operator (if)](formula-components/operators/if.md).
* [Functions](formula-components/functions/) - pre-defined formulas that you can use to accomplish complex things quickly. Examples include [concat](formula-components/functions/concat.md) (combines strings) and [dateAdd](formula-components/functions/dateadd.md) (adds `x` units of time to a date).

### Data Types

Notion formulas work with - and output - one of four different [data types](formula-basics/data-types/):

* [String](formula-basics/data-types/string.md)
* [Number](formula-basics/data-types/number.md)
* [Boolean (Checkbox)](formula-basics/data-types/boolean-checkbox.md) - Notion refers to these as "Checkbox" values, but under the hood, they're classic Boolean true/false values.
* [Date](formula-basics/data-types/date-data-type.md)

Understanding data types is crucial for comfortably working with Notion formulas. Every property outputs a specific data type (except Formulas and Rollups, which can output several).

Additionally, every operator and function accepts specific data types in its argument(s). They also output data of a specific type - and that type is often different than the data types taken as inputs.

#### **Data Type Example**

Here's an example using the [dateAdd](formula-components/functions/dateadd.md) function:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
dateAdd(now(),5,"days")
```
{% endcode %}

This function requires three arguments, which _must_ be (in this order):

1. A date
2. A number
3. A string (this must also be one of the accepted units, such as "days" or "years")

If the arguments are not passed data of the correct type, the formula will throw a **Type Mismatch error.**

![](<.gitbook/assets/Type Mismatch Error.png>)

{% hint style="info" %}
**Good to know:** Unlike many programming languages, Notion does _not_ do automatic type conversion within formulas. You'll need to provide data of the correct type within all function arguments.

_The only exceptions to this are the_ [_test_](formula-components/functions/test.md)_,_ [_replace_](formula-components/functions/replace.md)_, and_ [_replaceAll_](formula-components/functions/replaceall.md) _functions. These are advanced functions, so I won't cover their details here._

You'll also need to make sure the final output of your formula has only one data type.
{% endhint %}

#### About the Author

<img src=".gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
