---
description: Learn how to use the id function in Notion formulas.
---

# id

The `id()` function returns the current row’s **page ID,** which is a unique [string](../../formula-basics/data-types/string.md). `id()` accepts no arguments.

The page ID can also be found at the end of a Notion page’s URL (before any query strings starting with `?`.

`id()` outputs a string that is guaranteed to be unique for each page in a database. It is possible for all other properties - including Name - to contain the same value in multiple rows.

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Page URL: <https://www.notion.so/thomasfrank/id-c5d67d15854744869cc4a062fb7b1377>
id() // Output: c5d67d15854744869cc4a062fb7b1377
```
{% endcode %}

## Example Database

This example database uses the `id()` function and string concatenation to return the URL of each page within the database.

<figure><img src="../../.gitbook/assets/Id Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/id-0770ebee438e48a6a8f59b0de0617ce8" %}

### "URL" Property Formula

```jsx
"https://www.notion.so/" + id()
```

This formula concatenates the [string](../../formula-basics/data-types/string.md) "https://www.notion.so/" with the output of the `id()` function using the [add](../operators/add.md) operator.

#### Other formula components used in this example:

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
