---
description: Learn how to fix and debug errors within Notion formulas.
---

# Fixing Notion Formula Errors

If you write or paste a Notion formula that contains an error, you'll see a red error message at the bottom of the formula editor.

<figure><img src="../.gitbook/assets/Error in Notion Formula Editor.png" alt=""><figcaption></figcaption></figure>

The table below contains the most common errors you'll see, as well as the likely fix.

{% hint style="info" %}
**Good to know:** If you click away from the formula editor while your formula contains an error, the entire formula (or your changes to an existing formula) will be lost. Be sure to copy the formula to your clipboard in order to avoid losing it!
{% endhint %}

| Error                                   | Reason                                                                                                                                                                                                                                                                 |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Property not found                      | `prop("Property Name")` is referencing a property that doesn't exist, or contains a typo.                                                                                                                                                                              |
| Too few arguments...                    | Function requires more arguments than have been specified. Example: `dateBetween()` requires three arguments. See the [function references](../formula-components/functions/) for details on all functions and required arguments.                                     |
| Type mismatch                           | Operands of different types are being used on either side of an operator (e.g. `"1" == 1`), or an argument in a function has been provided data of the wrong type (e.g. `concat(1,2)` - [concat](../formula-components/functions/concat.md) requires string arguments) |
| Value expected                          | Typically indicates an errant comma - e.g. `add(1,)` - here, the add function is expecting another number argument due to the comma.                                                                                                                                   |
| Character expected                      | Indicates a missing character. The editor will specify the character. E.g. `concat("foo","bar)` returns `" expected (char 19)`                                                                                                                                         |
| Unexpected token in JSON                | Notion is reporting a JSON error. Typically happens if you try to escapse an invalid character, such as the `\e` in `concat("foo","\ebar")`.                                                                                                                           |
| Syntax error                            | A general syntax error. E.g `\e` in the formula editor will result in this error message: `Syntax error in part "\e" (char 1)`.                                                                                                                                        |
| Undefined constant                      | Likely means you need to wrap a string in quotation marks. E.g. typing `hello` in the formula editor returns `undefined constant: hello`.                                                                                                                              |
| Invalid syntax                          | Triggers when using syntax that Notion has explicitly defined as invalid, such as `[]`                                                                                                                                                                                 |
| Unexpected end of expression            | Triggers on an open parenthesis`(`, or a single `-` or `+`                                                                                                                                                                                                             |
| Symbol or string expected as object key | _Reason currently unknown; triggers on_ `{`                                                                                                                                                                                                                            |

The Notion formula editor does _not_ make debugging easy. Formulas are displayed in one long line, and errors are not highlighted in the formula.

Therefore, I recommend writing longer formulas in a programmer-focused text editor such as [VS Code](https://code.visualstudio.com/). There, you'll be able to use multiple lines and indentation, which makes debugging much easier.&#x20;

See my guide on [Writing Complex Formulas](../formula-basics/the-formula-editor.md#writing-complex-formulas-in-vs-code) to learn how to compress formulas for easy pasting into Notion's formula editor.

<figure><img src="../.gitbook/assets/Editing Notion Formulas in VS Code.png" alt=""><figcaption></figcaption></figure>

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
