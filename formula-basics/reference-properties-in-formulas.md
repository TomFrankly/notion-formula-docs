---
description: >-
  Learn how to reference other properties in Notion formulas in order to access
  their data.
---

# Reference Properties in Formulas

Within a Notion formula, you can use the `prop()`function to reference and "pull in" the data from any other property in the same database.

When using `prop()`, encapsulate the property name in quotes – e.g. `prop("Name")`.

Notion formulas can work with four different [data types](data-types/) - [string](data-types/string.md) (text content), [number](data-types/number.md), [Boolean](data-types/boolean-checkbox.md) (checkbox), and [date](data-types/date-data-type.md).

All database property types in Notion output a specific data type.&#x20;

{% hint style="info" %}
**Good to know:** Any time this reference states that a function "accepts only numbers as arguments" (or any of the other data types), understand that the function can also accept `prop()` as an argument, so long as the referenced property is outputting that data type.

Example: Assume a property called **Num** is a Number-type property. The [max](../formula-components/functions/max.md) function accepts numbers, so `max(5,10,prop("Num"))` would be valid.
{% endhint %}

Refer to the following table to see the data type of each property:

<table><thead><tr><th>Property</th><th data-type="select" data-multiple>Data Type</th><th>Notes</th></tr></thead><tbody><tr><td>Title</td><td></td><td>This is the default "Name" property that all database are required to have.</td></tr><tr><td>Text</td><td></td><td></td></tr><tr><td>Number</td><td></td><td></td></tr><tr><td>Select</td><td></td><td></td></tr><tr><td>Multi-Select</td><td></td><td>Returns a comma-separated string of all values present in the Multi-Select property.</td></tr><tr><td>Status</td><td></td><td>Returns a string even if the Status property is displayed as a Checkbox.</td></tr><tr><td>Date</td><td></td><td>Use the <a href="../formula-components/functions/start.md">start</a> and <a href="../formula-components/functions/end.md">end</a> functions to access dates in a date range.</td></tr><tr><td>Person</td><td></td><td></td></tr><tr><td>Files &#x26; Media</td><td></td><td>Returns the URL of the asset</td></tr><tr><td>Checkbox</td><td></td><td></td></tr><tr><td>URL</td><td></td><td></td></tr><tr><td>Email</td><td></td><td></td></tr><tr><td>Phone</td><td></td><td></td></tr><tr><td>Formula</td><td></td><td>Can return any of the data types. Must output only one. Use <a href="../reference/converting-data-types.md">type conversion</a> to work with multiple data types.</td></tr><tr><td>Relation</td><td></td><td></td></tr><tr><td>Rollup</td><td></td><td>See Notes on Rollups below.</td></tr><tr><td>Create time</td><td></td><td></td></tr><tr><td>Created by</td><td></td><td></td></tr><tr><td>Last edited time</td><td></td><td></td></tr><tr><td>Last edited by</td><td></td><td></td></tr></tbody></table>

## Notes on Rollups

{% hint style="info" %}
Learn more about Rollups in my [complete guide to Notion databases](https://thomasjfrank.com/notion-databases-the-ultimate-beginners-guide/#rollups).
{% endhint %}

The [data type](data-types/) of a Rollup referenced in a formula depends on both:

* The data type of the property the Rollup is referencing
* The Rollup's **Calculate** setting

When a Rollup's Calculate setting is set to **Show Original,** it will always output a string value.&#x20;

This is due to the fact that a Rollup can show the property values for multiple database rows – e.g. a Rollup targeting a number property may show a value of `4, 6, 2` if the current row is related to three other rows.&#x20;

When **Show Original** is set:

* A Rollup targeting a number-type property will output a numeric character (e.g. `4`), but it's still a string. (Use [toNumber](../formula-components/functions/tonumber.md) in your formulas to convert it)
* A Rollup targeting a Boolean-type property will output a string value of `Yes` or `No` (use [if](../formula-components/operators/if.md) to perform Boolean comparisons on these)

When a Calculate setting other than **Show Original** is chosen, the Rollup will output a different data type:

* If the Rollup is targeting a number or Boolean-type property, all Calculate settings (other than Show Original) will output a number.
* If the Rollup is targeting a date-type property, the **Earliest date, Latest date,** and **Date range** settings will output a date. **Date range** outputs a date object with both a start and end date, allowing you to access either using the [start](../formula-components/functions/start.md) and [end](../formula-components/functions/end.md) functions.&#x20;

Note that a Rollup cannot access the **End Date** of a date property, even if one is set. If you need to pull the end date of a date property through a Rollup, you'll need to first create a formula property that uses the [end](../formula-components/functions/end.md) function to output that end date, then configure your Rollup to target that formula property.

### Example Database

Duplicate this example database into your own workspace and try reconfiguring the **Rollup** property.&#x20;

Note that changing the settings may require you to click into the **Formula** property and hit **Enter** to get it to output data again - even if the Rollup configuration change didn't cause a Type Mismatch error in your formula.

![](<../.gitbook/assets/Rollups in Formulas.png>)

#### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/Rollups-in-Formulas-bff66df573934789a21842f86db4e57f" %}

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
