---
description: Learn how to use Notion formulas within database filters.
---

# Formulas in Database Filters

Database filters in Notion can target any type of property, including formula properties. However, there are some important rules to understand about how formulas and filters interact.

This page will explain those rules, and hopefully help you understand Notion's limitations when combining filters and formulas.

<figure><img src="../.gitbook/assets/Notion Formulas and Database Filters.png" alt=""><figcaption></figcaption></figure>

Here's the TL;DR version:

1. Filter options for formula properties depend of the [data type](data-types/) of your formula output ([string](data-types/string.md), [number](data-types/number.md), [Boolean/Checkbox](data-types/boolean-checkbox.md), or [date](data-types/date-data-type.md)).
2. Formula properties are [**read-only**](formulas-in-database-filters.md#formulas-are-read-only-properties)**.**
3. A formula filter will prevent a new row from being inserted into current view unless the filter **fits the default output that formula would already have**.&#x20;
4. In other words, formula filters **cannot** act as [forcing functions](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#forcingfunctions). They cannot change the output of the formula. Formula output is determined solely by the formula itself and the variable data within any [properties the formula references](reference-properties-in-formulas.md).
5. **Created by, Create time, Last edited by,** and **Last edited time** properties are [_initially empty_](formulas-in-database-filters.md#undefined)_._ This can cause confusion when filtering by them, or by formulas that reference them, so it's good to understand this bit of nuance.

If you'd like to learn more about how to use filters in Notion databases, check out the filter section in my databases guide:

{% embed url="https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#filters" %}

## Example Database

All of the concepts explained in this article can be seen at work in this example database, which contains several unique views. Each view filters by one or more formulas.



### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/Formulas-in-Database-Filters-5ff409fd5d0947b883833a3aec549d48" %}

## Target a Formula with a Filter

Creating a filter that targets a formula property is no different than creating any other kind of filter.

You can create either a **basic** or **advanced** filter; either way, simply choose the formula property you want when setting up the filter:

<figure><img src="../.gitbook/assets/Creating a Filter for a Formula Property in a Notion Database.png" alt=""><figcaption></figcaption></figure>

Notion's filter builder treats formula properties differently depending on the [data type](data-types/) of their output.

<details>

<summary>String output</summary>

Formulas that output [strings](data-types/string.md) are treated like text properties.&#x20;

Options include:

* Is
* Is not
* Contains
* Does not contain
* Starts with
* Ends with
* Is empty
* Is not empty&#x20;

</details>

<details>

<summary>Number output</summary>

Formulas that output [numbers](data-types/number.md) are treated like number properties.&#x20;

Options include:

* \= (equal)
* ≠ (not equal)
* \> (greater than)
* < (less than)
* ≥ (greater than or equal to)
* ≤ (less than or equal to)
* Is empty
* Is not empty

</details>

<details>

<summary>Date output</summary>

Formulas that output [dates](data-types/date-data-type.md) are treated like date properties. Options include:

* Comparisons:
  * Is
  * Is before
  * Is after
  * Is on or before
  * Is on or after
  * Is within
  * Is empty
  * Is not empty
* Dates:
  * Today
  * Tomorrow
  * Yesterday
  * One week ago
  * One week from now
  * One month ago
  * One month from now
  * Custom date

</details>

<details>

<summary>Boolean/Checkbox output</summary>

Formulas that output [Boolean/Checkbox](data-types/boolean-checkbox.md) values are treated like checkbox properties.&#x20;

Options include:

* Comparions:
  * Is
  * Is not
* Choices:
  * Checked
  * Unchecked

</details>

In most aspects, a filter targeting a formula will behave exactly like a formula targeting another property type that outputs the same type of data.

Howevere, this is one **major** difference: **Formulas are read-only!**

This has two major implications:

* You cannot create a [forcing function](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#forcingfunctions) that influences the output of a formula property.
* If your filter does not match the _initial_ value of the formula, new rows will open directly as pages. They may also not show up in the database view that contains that filter.

The term "_initial_" is important in that latter point because the **Created by, Created time, Edited by, and Edited time** properties have a little-known quirk: [Notion initially sees them as **empty**](formulas-in-database-filters.md#undefined) **** when a new row is created!

Likewise, any formula that references a property that has one of these types will _also_ start off empty from Notion's perspective.

The time/person is filled in so quickly that users never perceive this, but it does have important implications for filter design. [Click here](formulas-in-database-filters.md#undefined) to go to the section of this article that about this quirk.

## Formulas are Read-Only Properties

The most important thing to understand about formula properties in Notion databases is that they are **read-only properties.**

This means that you cannot click into a formula and directly change that formula's output on a per-database-row basis.

In each database row, the return value of a formula property is determined **solely** by:

* The underlying formula - a.k.a. the "code" that you've entered into the formula editor
* Any properties which the formula references

<figure><img src="../.gitbook/assets/Formula Code and Property References - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

Formulas can have variable results on a per-row basis only when **writeable** properties they reference contain variable data.

Consider this formula:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Property name: Times 2
prop("Number") * 2
```
{% endcode %}

This formula takes the value of the Number property and multiplies it by 2. Let's say we have three database rows, with the following Number property values:

* 5
* 10
* 15

The formula's output for these rows will be, respectively:

* 10
* 20
* 30

<figure><img src="../.gitbook/assets/Notion Formula - Multiplier.png" alt=""><figcaption></figcaption></figure>

Now that you hopefully understand this concept, let's cover the first major rule of formula/filter design.

## Filters Must Match Default Formula Output for New Rows

If you're designing a database view in which new rows **do not need to be created directly,** then this section isn't important.

_Example: You're creating a "reporting" view for a database. This view simply gives you information about rows that have already been created in other views. In this case, set your filters however you want._

However, in many database views, you want to retain the ability to **create new rows directly in the view.**

{% embed url="https://thomasjfrank.com/wp-content/uploads/2022/09/Filters-And-Formulas-Default-Values-Notion-Formulas.m4v" %}

To retain this ability, your filter critiera must match the **default** output that the formula would have. In other words, the filter cannot attempt to change the output of the formula.

Filters cannot act as [forcing functions](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#forcingfunctions), applying specific values to formula properties.&#x20;

{% hint style="info" %}
**Good to know:** It's worth noting that they also cannot do this for _any_ read-only property type, including Rollup, Created by, Created Time, Last edited by, and Last edited time (additionally, they can't set a non-empty value on a Files & Media property).
{% endhint %}

Here are a few examples of formulas (one for each data type), along with a **valid** and **invalid** filter for each. _Again, this is only important in views where you want to be able to directly create new rows that stay in the view._

### String Example

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Property name: Priority
"Priority: " + prop("Priority")
```
{% endcode %}

* **Valid:** Priority contains "Priority:"
* **Invalid:** Priority is "The Priority:"

_Note how the invalid filter is looking for output that the formula doesn't output by default._

### Number Example

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Property name: Timestamp
timestamp(now())
```
{% endcode %}

* **Valid:** Timestamp > 0
* **Invalid:** Timestamp = 0

### Boolean/Checkbox Example

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Property name: Truth
if( 10 > 5, true, false)
```
{% endcode %}

* **Valid:** Truth is checked
* **Invalid:** Truth is unchecked

### Date Example

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Property name: One More Day
dateAdd(now(), 1, "days")
```
{% endcode %}

* **Valid:** One More Day is Tomorrow
* **Invalid:** One More Day is Today

### Formula Cannot Change Referenced Property Values

It's worth noting that a filter/formula combination _cannot_ influence or change the output of a property that is referenced within that formula.

What does this mean? Let's go back to our multiplier example. The formula there is:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Property name: Times 2
prop("Number") * 2
```
{% endcode %}

Here, I cannot simply create a filter like:

*

## "Created Time" and Similar Properties

Notion sees the following properties types as initially **empty** whenever a new database row is created:

* Created by
* Created time
* Last edited by
* Last edited time

When you create a new row in a database, it _looks_ like these values are instantly filled in. But under the hood, they start empty. They're just filled so quickly that users don't perceive this default empty state.

This has important implications for filter design.

When you use Notion on a desktop platform (i.e. not on a mobile device), creating a new row in a database does not open that row's page by default. Instead, you'll just get a new row or card, and you'll be able to set the row's title right away:



#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
