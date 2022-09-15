---
description: Learn how to use the test function in Notion formulas.
---

# test

The `test()` function allows you to test whether a [string](../../formula-basics/data-types/string.md) contains a substring, the latter of which can be a [regular expression](../../reference/regular-expressions-in-notion-formulas.md). If it does, the function returns [true](../constants/true.md).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
test(string, string [regex supported])
```
{% endcode %}

`test()` accepts two string arguments and outputs a [Boolean](../../formula-basics/data-types/boolean-checkbox.md) result.

{% hint style="info" %}
**Good to know:** `test()`, [replace](replace.md), and [replaceAll](replaceall.md) are able to automatically convert [numbers](../../formula-basics/data-types/number.md) and [Booleans](../../formula-basics/data-types/boolean-checkbox.md) (but not [dates](../../formula-basics/data-types/date-data-type.md)) to strings. Manual [type conversion](../../reference/converting-data-types.md) is not needed.
{% endhint %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
test("Monkey D. Luffy", "Luffy") // Output: true

// test() is case-sensitive
test("Monkey D. Luffy", "luffy") // Output: false

// You can use brackets [] to create a set of characters,
// any of which will be matched
test("Monkey D. luffy", "[Ll]uffy") // Output: true

// You can also create a group with () and then use the | (OR) operator
test("Monkey D. luffy", "(L|l)uffy") // Output: true
```
{% endcode %}

{% hint style="info" %}
Check out the [regular expressions](../../reference/regular-expressions-in-notion-formulas.md) page to see a **lot** more that you can accomplish using them!
{% endhint %}

## Example Database

This example database contains some file attachments. The Meta formula property displays information about each file, including its media type and hosting location (within Notion or hosted externally).

{% hint style="info" %}
**Good to know:** This exact example is also used for the [contains](contains.md) function. I recommend checking them both out to see how `test()` is a much more flexible tool.,
{% endhint %}

![](<../../.gitbook/assets/Test Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/test-3d50bd33ca0c48f2af86adb51b1f538b" %}

### “Meta” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
if(test(prop("File"),"([jJ][pP][eE]?[gG]|[gG][iI][fF]|[pP][nN][gG])"),"🌅 Image",if(test(prop("File"),"([mM][pP]3|[wW][aA][vV]|[aA][iI][fF]{2})"),"🎧 Audio","📝 Text")) + "\n" + if(test(prop("File"),"secure.notion-static.com"),"✅ Internal","⛔️ Externally Hosted")

// Expanded
if(
    test(
        prop("File"),
        "([jJ][pP][eE]?[gG]|[gG][iI][fF]|[pP][nN][gG])"
    ),
    "🌅 Image",
    if(
        test(
            prop("File"),
            "([mM][pP]3|[wW][aA][vV]|[aA][iI][fF]{2})"
        ),
        "🎧 Audio",
        "📝 Text"
    )
) + 
"\n" + 
if(
    test(
        prop("File"),
        "secure.notion-static.com"
    ),
    "✅ Internal",
    "⛔️ Externally Hosted"
)
```
{% endcode %}

`test()` is essentially the same as the [contains](contains.md) function, except it allows for the use of [regular expressions](../../reference/regular-expressions-in-notion-formulas.md).

This makes it far more powerful, and allows you to do things like **case-insensitive matching**. You can also include **optional characters** that don’t _have_ to be included in the match.

{% hint style="info" %}
**Good to know:** Regular expressions are incredibly powerful, but have a steep learning curve. Check out the [regular expressions](../../reference/regular-expressions-in-notion-formulas.md) page for a primer on how to use them in Notion formulas, as well as resources for learning them more deeply.
{% endhint %}

This formula replicates the functionality of the example formula in the [contains() function example database](contains.md#example-database), but it uses `test()`'s regular expression capability to reduce the size of the formula and add case-insensitivity.

If you want to understand this formula fully, you should read the [regular expressions](../../reference/regular-expressions-in-notion-formulas.md) page as well as the page on [if statements](../operators/if.md).

But let’s break apart this small chunk of the formula here:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
test(
    prop("File"),
    "([jJ][pP][eE]?[gG]|[gG][iI][fF]|[pP][nN][gG])"
)
```
{% endcode %}

`test()` returns true if the first string argument contains the substring specified in the second argument.

Here, our second argument is a regular expression. It is essentially saying:

> Match “jpg”, “jpeg”, “gif”, or “png” - regardless of character case.

How is it doing that? Let’s break it down.

* The parentheses `()` form what’s called a **capture group.**
* The pipe symbols `|` act as Boolean OR operators
* The brackets `[]` essentially say, “Match any single character that is included here”.

To make all of this easier to understand, let's start with the simplest version of a regular expression – a normal string.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
"jpg"
```
{% endcode %}

Here, `test()` would only return true if the first argument’s string contains “jpg”.

But what if we want to match one of several options? We'll need to use the OR operators `|` for that, and they only work inside of a capture group created with parentheses `()`.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
"(jpg|gif|png)"
```
{% endcode %}

Now, our `test()` function would return true if the first argument contains _any_ of the following:

* jpg
* gif
* png

However, currently this would only happen if the substring was all lower-case. The substring “JPG” would not cause `test()` to return true.

To make our regular expression case-insensitive, we’ll define a **character class** using brackets `[]`.

Here’s a very simple class:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
"[Jj]"
```
{% endcode %}

This will create a **match** if the first argument’s string contains “j” or “J”.

To make our entire set of potential file extensions case-insensitive, we simply need to define a similar character class for each letter:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
"[Jj][Pp][Gg]|[Gg][Ii][Ff]|[Pp][Nn][Gg]"
```
{% endcode %}

This regular expression will create a match for any of our three file extensions, regardless of the case (upper or lower) of any letter.

{% hint style="info" %}
**Good to know:** Many programming languages and regex engines ([such as JavaScript's](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular\_Expressions#advanced\_searching\_with\_flags)) support **flags** that you can set to more easily do things like marking your search as case-insensitive.

Unfortunately, in our testing we've found that Notion seems to support none of these flags. This is why we have to do things "the hard way" and define a character class for every letter that we want to be case-insensitive.
{% endhint %}

Finally, let’s deal with the fact that “jpg” is sometimes spelled “jpeg”. We could simply add another “or” case to our regular expression, but there’s a more efficient way to do it.

By adding a `?` character after another character (or character class), we can tell the regular expression engine (or “regex engine”) that character is optional. In other words, we’ll get a match if it shows up **zero or one times.**

To keep things simple, here’s how we’d match for `jpg` or `jpeg`, with case-sensitivity:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
"jpe?g"
```
{% endcode %}

{% hint style="info" %}
**Good to know:** Since `?` is a special character, you need to “escape” it with a `\` if you actually want to match for a question mark – e.g. `\?`.
{% endhint %}

Now that you have that down, let’s add our `?` to the original regular expression:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
"[Jj][Pp][Ee]?[Gg]|[Gg][Ii][Ff]|[Pp][Nn][Gg]"
```
{% endcode %}

With `[Ee]?` included, we’ll now match any version of “jpg” or “jpeg” regardless of any character’s case.

#### Making This Example Work in the Real World

This example deliberately keeps things simple in order to make the functionality of `test()` easy to understand.

If you actually wanted to determine the media type of a file attachment, you’d first want to extract the file extension from its URL (otherwise, any other instance of letters such as “jpg” or “mov” might cause your formula to mis-identify the file type).

In the example database above, I’ve also included a **File Extension** property with the following formula:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace(prop("File"), ".*\\.(\\w+)$", "$1")
```
{% endcode %}

This uses the replace function along with another regular expression to replace the entire file URL with its file extension.

{% hint style="info" %}
Want to understand how this regular expression works? Check out the [replace function's example database](replace.md#example-database); I've explained it there.
{% endhint %}

To make this example error-free, you’d ultimately want to have the **Meta** property target the output of **File Extension,** rather than the file’s URL directly. Alternatively, you could combine these two formulas. I’ll leave that as an exercise for the reader.

#### Other formula components used in this example:

{% content-ref url="../operators/if.md" %}
[if.md](../operators/if.md)
{% endcontent-ref %}

{% content-ref url="../operators/add.md" %}
[add.md](../operators/add.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
