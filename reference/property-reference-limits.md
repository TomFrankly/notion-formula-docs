---
description: Learn about Notion's reference chain limit.
---

# Property Reference Limits

Notion formulas will only allow you to create a **reference chain** that is seven properties long.

Take a look at this database:

<figure><img src="../.gitbook/assets/Reference Chain Limit in Notion Formulas.png" alt=""><figcaption></figcaption></figure>

_Click the view/duplicate all examples shown on this page:_

{% embed url="https://thomasfrank.notion.site/Reference-Chain-Limits-5fba0f9a3223417ba134699fe1084e69" %}

Each property pulls in the value of the previous property and then adds 1.

Note how properties **8** and **9** actually have a _lower_ value than property **7.** Property 8 _should_ output 9, and Property 9 _should_ output 10 - but they don't. What's going on here?

This is an example of Notion's reference chain limit.

Property 9 contains the following formula:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
prop("8") + 1
```
{% endcode %}

But in order to output a value, Property 9's formula code "underneath the hood" must first execute the formula code of Property 8, which contains:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
prop("7") + 1
```
{% endcode %}

...meaning that the Property 8 formula must execute the code in Property 7, and so on.

This is what we mean by a **property reference chain.**&#x20;

From the perspective of Property 9, which contains `prop("8")`, Property 8 does not contain a static value. Instead, it contains another formula which must be executed.

To prevent slowdowns and other problems, Notion's developers implemented a reference chain limit of seven properties.

Here's another example. Each formula property takes the string from the last and adds on the next word. Note how Property 8 loses the first word "Monkey":

<figure><img src="../.gitbook/assets/String Example of Reference Chain Limit in Notion Formulas.png" alt=""><figcaption></figcaption></figure>

The reference chain limit also applies if you send values from one row (or database) to another using rollups.

The **String** property in the "Rollup Cascade" example below contains the following formula:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
if(not empty(prop("Rollup")), prop("Rollup") + 1, 1)
```
{% endcode %}

<figure><img src="../.gitbook/assets/Rollup Cascade Example of Reference Chain Limit in Notion Formulas.png" alt=""><figcaption></figcaption></figure>

As you can likely tell, the **Rollup** property is configured to display the value of property **2** from the row set in the **Relation** property.&#x20;

Keep this limitation in mind when you're creating complex databases where one formula references another formula, which references another formula, which references another....

It's easy to unwittingly hit the limit (Notion won't alert you to it), and then be confused as to why the formula you're building isn't outputting all the data that it should.

{% hint style="info" %}
**Good to know:** This does _not_ mean you can only reference seven properties in a single formula. You can reference many, many more if you want.
{% endhint %}

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
