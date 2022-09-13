---
description: Learn how to use the replace function in Notion formulas.
---

# replace

The `replace()` function searches a [string](../../formula-basics/data-types/string.md) for a pattern (which can be a [regular expression](../../reference/regular-expressions-in-notion-formulas.md)), and replaces the **first** match it finds with another string.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace(string, string [regex supported], string [regex supported])
```
{% endcode %}

Since they can search for pattern matches using regular expressions, `replace()`,its counterpart, [replaceAll](replaceall.md), and the related [test](test.md) function are three of the most versatile and powerful functions you can use in your Notion formulas.

{% hint style="info" %}
**Good to know:** `replace()`, [replaceAll](replaceall.md), and [test](test.md) are able to automatically convert [numbers](../../formula-basics/data-types/number.md) and [Booleans](../../formula-basics/data-types/boolean-checkbox.md) (but not [dates](../../formula-basics/data-types/date-data-type.md)) to strings. Manual [type conversion](../../reference/converting-data-types.md) is not needed.
{% endhint %}

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Pogo","Po","Dog") // Output: Doggo

// Matches the first occurrance, unless otherwise specified
replace("Dogs Dogs Dogs","Dogs","Cats") // Output: Cats Dogs Dogs

// $ tells the regex engine "start from end of line and work backwards"
replace("Dogs Dogs Dogs","Dogs$","Cats") // Output: Dogs Dogs Cats

// Matches are case-sensitive
replace("thomas","t","T") // Output: Thomas

// You can use brackets [] to create a set of characters,
// any of which will be matched
replaceAll("thomas", "[Tt]homas", "Megatron") // Output: Megatron

// You can also create a group with () and then use the | (OR) operator
replaceAll("thomas", "(T|t)homas", "Megatron") // Megatron

// Accepts regex metacharacters, such as "\\b" which denotes "word boundary".
// Without \\b, this would output "Thwas is Sparta"
replace("This is Sparta","\\bis\\b","was") // Output: This was Sparta
```
{% endcode %}

{% hint style="info" %}
Check out the [regular expressions](../../reference/regular-expressions-in-notion-formulas.md) page to see a **lot** more that you can accomplish using them!
{% endhint %}

## Example Database: File Extensions

The example database below contains several media attachments. The **File Extension** property uses `replace()` and a regular expression to replace each file’s full URL with its file extension.

![](<../../.gitbook/assets/Replace Function - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/replace-955e8dfdd25e4491b11292634ae6340a" %}

### “File Extension” Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace(prop("File"), ".*\\.(\\w+)$", "$1")
```
{% endcode %}

To extract the file extension from the media attachment's full URL, we use a regular expression that essentially translates to:

> Start from the end of the string and capture all characters until the first period `.` – then replace the entire URL with those captured characters.

Let's break down exactly how our regular expression – `.*\\.(\\w+)$` – does this:

* `.` is a wildcard, meaning it'll match _any_ character.
* `*` is a [quantifier](../../reference/regular-expressions-in-notion-formulas.md#quantifiers). It tells the regex engine to match _zero or more_ of the preceding character. So `.*` means, "match any number of any character.
* `\\.` translates to an actual period `.` character. It must be "escaped" with `\\` because `.` is a special wildcard character in regular expressions (as mentioned above).
* `(\\w+)` is our **capture group.** We're "[capturing](../../reference/regular-expressions-in-notion-formulas.md#character-grouping)" any match defined within the parentheses `()`, allowing us to reference the capture later (which we do with the `$1`). `\\w` is another special character that translates to "any word character", and `+` is a quantifier that translates to _one or more._
* `$` is an [anchor](../../reference/regular-expressions-in-notion-formulas.md#anchors) **** that tells the regex engine that the match must happen at the **end of the input string.** This essentially makes sure the match happens at the end of the URL.

Basically, we're telling the regular expression to match the _entire_ URL, but we're putting only the file extension (everything after the final period `.` character) into a capture group.

Then, we're replacing that entire matched URL with the contents of the capture group by referencing it with `$1`.

{% hint style="info" %}
**Good to know:** If you want to learn more about using regular expressions in Notion, check out my **** [complete regular expression reference](../../reference/regular-expressions-in-notion-formulas.md).&#x20;

Most truly worthwhile use cases for `replace()` in Notion will use special characters like the ones shown above, so it's worth getting familiar with them!
{% endhint %}

## Example Database: Temperature Conversion

The example database below shows how you can use `replace()` in conjunction with other functions to convert a temperature value from Fahrenheit to Celsius.

At first, the temperature is a [string](../../formula-basics/data-types/string.md) value that cannot be manipulated by arithmetic functions. `replace()` is used to extract the number from the full string.

![](<../../.gitbook/assets/Fahrenheit to Celcius Convertion - Replace Function with Regular Expressions - Notion Formulas.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/replace-955e8dfdd25e4491b11292634ae6340a" %}

### "Celsius Conversion" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
replace(replace(prop("Name"),"\\d+",format(round((toNumber(replace(prop("Name"), "\\D*(\\d+)\\D", "$1")) - 32) * 5 / 9))),"°F","°C")

// Expanded
replace(
    replace(
        prop("Name"),
        "\\d+",
        format(
            round(
                (
                    toNumber(
                        replace(
                            prop("Name"), 
                            "\\D*(\\d+)\\D", 
                            "$1"
                        )
                    ) - 32
                ) * 5 / 9
            )
        )
    ),
    "°F",
    "°C"
)
```
{% endcode %}

This formula is meant to demonstrate how you can use `replace()` in conjunction with other functions in order to do things that are otherwise impossible.

Here, the challenge is to convert the weather prediction from Fahrenheit to Celsius. However, the prediction starts out as a [string](../../formula-basics/data-types/string.md) value – i.e. "Today's high will be 78 °F".&#x20;

Since it's a string, we can't currently use arithmetic functions on it. We also can't currently use [toNumber](tonumber.md) to convert it to a [number](../../formula-basics/data-types/number.md), since it contains non-numeric characters.

The [slice](slice.md) function isn't an option, either. The numeric temperature shows up at different positions based on the text that comes before it.

Fortunately, the `replace()` function allows us to solve this problem using a few simple regular expressions.&#x20;

Here's a quick breakdown of this formula's process:

1. Extract the temperature number using `\\D*(\\d+).\\D`, which captures any numeric digits and replaces the entire string with just those digits. See the [first example](replace.md#example-database-file-extensions) on this page to understand how that works. (`\\D` means "any non-digit character", and `\\d` mean "any digit character".)
2. Convert the digits from a string to a number using [toNumber](tonumber.md).
3. Apply the [Fahrenheit-to-Celsius conversion formula](https://www.almanac.com/temperature-conversion-celsius-fahrenheit): `(Fahrenheit temp - 32) * 5 / 9`.
4. Round to the nearest integer using [round](round.md).
5. Convert the result to a string using [format](format.md).
6. Use `replace()` a second time to replace the original weather predictions Fahrenheit number with out new Celsius number.
7. Use `replace()` a final time to replace `°F` with `°C`.

#### Other formula components used in this example:

{% content-ref url="tonumber.md" %}
[tonumber.md](tonumber.md)
{% endcontent-ref %}

{% content-ref url="round.md" %}
[round.md](round.md)
{% endcontent-ref %}

{% content-ref url="format.md" %}
[format.md](format.md)
{% endcontent-ref %}

{% content-ref url="../operators/subtract.md" %}
[subtract.md](../operators/subtract.md)
{% endcontent-ref %}

{% content-ref url="../operators/multiply.md" %}
[multiply.md](../operators/multiply.md)
{% endcontent-ref %}

{% content-ref url="../operators/divide.md" %}
[divide.md](../operators/divide.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
