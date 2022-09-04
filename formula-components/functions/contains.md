---
description: Learn how to use the contains function in Notion formulas.
---

# contains

The `contains()` function tests whether the first argument contains the second argument. It only accepts [strings](../../formula-basics/data-types/string.md) (or nested functions that output strings).

`contains()` tests for the entire string passed via the second argument, is case-sensitive, and does not accept [regular expressions](../../reference/regular-expressions-in-notion-formulas.md).

{% hint style="info" %}
**Good to know:** The [test](test.md) function can do everything `contains()` does and much more, including accepting [regular expressions](../../reference/regular-expressions-in-notion-formulas.md) and testing non-string data types.
{% endhint %}

## Example Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
contains("Monkey D. Luffy", "Luffy") // Output: true

contains("Monkey D. Luffy", "keyLuf") // Output: false

// Invalid
contains(true, "true") // Error: Type mismatch true is not a Text.
```
{% endcode %}

## Example Database

This example database contains some file attachments. The Meta formula property displays information about each file, including its media type and hosting location (within Notion or hosted externally).

![](<../../.gitbook/assets/Contains Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/contains-a41cbf79c85345c0bb9350846d2fa7c3" %}

### “Meta” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Compressed
if(contains(prop("File"),"jpg") or contains(prop("File"),"png") or contains(prop("File"),"gif") or contains(prop("File"),"jpeg"),"🌅 Image",if(contains(prop("File"),"mp3") or contains(prop("File"),"wav") or contains(prop("File"),"aiff"),"🎧 Audio","📝 Text")) + "\n" + if(contains(prop("File"),"secure.notion-static.com"),"✅ Internal","⛔️ Externally Hosted")

// Expanded
if(
    contains(
        prop("File"),
        "jpg"
    ) or contains(
        prop("File"),
        "png"
    ) or contains(
        prop("File"),
        "gif"
    ) or contains(
        prop("File"),
        "jpeg"
    ),
    "🌅 Image",
    if(
        contains(
            prop("File"),
            "mp3"
        ) or contains(
            prop("File"),
            "wav"
        ) or contains(
            prop("File"),
            "aiff"
        ),
        "🎧 Audio",
        "📝 Text"
    )
) + 
"\n" + 
if(
    contains(
        prop("File"),
        "secure.notion-static.com"
    ),
    "✅ Internal",
    "⛔️ Externally Hosted"
)
```
{% endcode %}

File & Media-type [properties](../../formulas-and-databases/reference-properties-in-formulas.md) return their file path as a [string](../../formula-basics/data-types/string.md) when referenced in Notion formulas.

This formula uses `contains()` to check each file’s path for the presence of several common file extensions, such as `jpg`, `gif`, `mp3`, etc.

It uses a [nested if statement](../operators/if.md#nested-if-then-statements) , as well as the [or](../operators/or.md) operator, to check for several different file extensions. It then outputs the file’s media type based on its match (or lack thereof).

Another if statement checks for the presence of the string `secure.notion-static.com`, which is always part of the URL for files that are uploaded directly to Notion’s Amazon AWS locker.

{% hint style="info" %}
**Note:** One major weakness of `contains()` is that it can’t do case-insensitive matching. In this formula, we’d have to add many more “or” clauses in order to test for every case variation of each file type. Check out the [test](test.md) function’s example database to see a much more efficient way to achieve this exact same goal.
{% endhint %}

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

{% content-ref url="../operators/or.md" %}
[or.md](../operators/or.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
