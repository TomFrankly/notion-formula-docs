---
description: Learn how to use the sign function in Notion formulas.
---

# sign

The `sign()` function returns the sign of its argument. It indicates whether its argument is positive, negative, or zero.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
sign(number)
```
{% endcode %}

`sign()` accepts only [numbers](../../formula-basics/data-types/number.md); it will not auto-convert [Booleans](../../formula-basics/data-types/boolean-checkbox.md) or other [data types](../../formula-basics/data-types/).

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
sign(-5) // -1

sign(5) // 1

sign(0) // 0

sign(+"-1") // -1
```
{% endcode %}

## Example Database

The example database below lists bank account balances. The `sign()` function is used to determine the output of the Status property.

<figure><img src="../../.gitbook/assets/Sign Function - Notion Formulas.png" alt=""><figcaption></figcaption></figure>

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/sign-ae7ef4a2f236433cadf04a47b48774d1" %}

### "Balance" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
sign(prop("Balance")) == -1 ? "🔴 Negative Balance!" : sign(prop("Balance")) == 0 ? "🟡 $0 Balance" : "🟢 Balance OK"

// Expanded
sign(
    prop("Balance")
) == -1 ? 
"🔴 Negative Balance!" : 
sign(
    prop("Balance")
) == 0 ? 
"🟡 $0 Balance" : 
"🟢 Balance OK"
```
{% endcode %}

This simple formula uses a [nested if-statement](../operators/if.md#nested-if-then-statements) (written in the ternary operator syntax with `?` and `:`) to return one of three status messages.

The output is determined by the `sign()` function's output.

{% hint style="info" %}
Good to know: You can also use comparison operators such as [larger](../operators/larger.md) and [smaller](../operators/smaller.md) to accomplish the same thing.

E.g. `prop("Balance") < 0`.
{% endhint %}

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="../operators/equal.md" %}
[equal.md](../operators/equal.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
