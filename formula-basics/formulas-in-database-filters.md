---
description: Learn how to use Notion formulas within database filters.
---

# Formulas in Database Filters

Database filters in Notion can target any type of property, including formula properties. However, there are some important rules to understand about how formulas and filters interact.

This page will explain those rules, and hopefully help you understand Notion's limitations when combining filters and formulas.

<figure><img src="../.gitbook/assets/Notion Formulas and Database Filters.png" alt=""><figcaption></figcaption></figure>

If you'd like to learn more about how to use filters in Notion databases, check out the filter section in my databases guide:

{% embed url="https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#filters" %}

## Target a Formula with a Filter

Creating a filter that targets a formula property is no different than creating any other kind of filter.

You can create either a **basic** or **advanced** filter; either way, simply choose the formula property you want when setting up the filter:



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

Formulas that output Boolean/Checkbox values are treated like checkbox properties.&#x20;

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

The term "_initial_" is important in that latter point because the **Created by, Created time, Edited by, and Edited time** properties have a little-known quirk: Notion initially sees them as **empty** when a new row is created!

Likewise, any formula that references a property that has one of these types will _also_ start off empty from Notion's perspective.

The time/person is filled in so quickly that users never perceive this, but it does have important implications for filter design. Click here to go to the section of this article that about this quirk.

## Formulas are Read-Only Properties

The most important thing to understand about formula properties in Notion databases is that they are **read-only properties.**

This means that you cannot click into a formula and directly change that formula's output on a per-database-row basis.

On each database row, the return value of a formula property is determined **solely** by:

* The underlying formula - a.k.a. the "code" that you've entered into the formula editor
* Any properties which the formula references

Formulas can have variable results on a per-row basis only when **writeable** properties they reference contain variable data.

Consider this formula:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
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









{% hint style="info" %}
**Good to know:** It can be _very_ useful to combine an "is" filter with a formula that utilizes a regular expression to output a particular string.
{% endhint %}



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
