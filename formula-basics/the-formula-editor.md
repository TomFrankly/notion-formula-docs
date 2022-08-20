---
description: Learn how to write formulas within Notion's formula editor window.
---

# The Formula Editor

When you click inside the content area of a formula property, you'll be presented with Notion's formula editor.

The editor is split into three parts:

* The editor field. Formulas written here must be written in a single, unbroken line without line breaks or indentation.
* A scrollable list of all available properties, [constants](../formula-components/constants/), [operators](../formula-components/operators/), and [functions](../formula-components/functions/). Clicking one will add it to your formula at the cursor's current location.
* A context window the provides a description of the currently selected/hovered formula component. Also includes a syntax reference and one or more examples.

![](<../.gitbook/assets/Notion Formula Editor.png>)

In addition to clicking formula components (constants, functions, etc), you can also start typing to automatically filter them. Hit enter when the one you want becomes highlighted.

When you've finished writing your formula, hit `Ctrl/⌘ + Enter` to exit the formula editor.

## Errors in Notion Formulas

If your formula contains an error, you won't be able to save the changes you've made to it.&#x20;

**Clicking away from the formula editor will result in your changes being lost, so make sure you copy your formula to your clipboard before doing so.**

When there is an error in your formula, you'll see a description of it at the bottom of the formula editor.

![](<../.gitbook/assets/Error in Notion Formula.png>)

Learn how to debug your formulas and fix errors:

{% content-ref url="../reference/debugging-formulas.md" %}
[debugging-formulas.md](../reference/debugging-formulas.md)
{% endcontent-ref %}

## Writing Complex Formulas in VS Code

When you need to write a formula that's more than a couple lines long, I highly recommend writing it first in a proper text editor such as Visual Studio Code first.

{% embed url="https://code.visualstudio.com/" %}

Writing your formulas in a true text editor will allow you to add indentation, comments, and other quality-of-life features that make you formulas easier to read and debug.

Notion formulas don't have a specific syntax, so I recommend saving your formula files as JavaScript files with the `.js` extension.

![](<../.gitbook/assets/Editing Notion Formulas in VS Code.png>)

Note how I comment specific sections of my formula:

{% code overflow="wrap" lineNumbers="true" %}
```
// First half of main else case - deal with opening hours
```
{% endcode %}

Notion formulas often require multiple levels of [nested if statements](../formula-components/operators/if.md#nested-if-then-statements), and these can get confusing and hard to keep track of. Adding comments above the function I'm calling helps me to understand my own formula code.

### Re-Formatting Formulas for Notion

Notion's formula editor doesn't support newlines or comments, so you can't simply paste your formula from VS Code to Notion. If you try, your formula won't work.

For this reason, we need to **re-format** formulas before they can be pasted into Notion:

* New lines must be removed
* Comments must be removed

Fortunately, you don't have to do this manually! Instead, you can do a **find and replace** operation using a regular expression that removes all of these elements for you.

Here's the expression (refer to the [regular expressions guide](../reference/regular-expressions-in-notion-formulas.md) if you want to understand how this works):

{% code overflow="wrap" lineNumbers="true" %}
```regex
(\n[ ]{2,}|\n|[/]{2}[^\n]*)
```
{% endcode %}

{% hint style="info" %}
Good to know: You can use text-snippet apps like [TextExpander](https://textexpander.com/), [Alfred](https://www.alfredapp.com/help/features/snippets/) (macOS), or [Espanso](https://espanso.org/install/) to find this expression to an easy-to-type keyword. I use `nminify`.
{% endhint %}

![](<../.gitbook/assets/Reformatting Notion Formula.png>)

1. Copy and paste your formula. We'll compress one of the copies, leaving the other as an easy-to-read reference.
2. Open the find and replace window with `Ctrl/⌘ + F` and paste the expression into the find field.
3. Paste in the expression above.
4. Click the **Use Regular Expression** button.
5. Select the entirety of your formula (just one of the copies)
6. Click the **Find in Selection** button.
7. Ensure the **Replace** field is blank.
8. Click the **Replace All** button.

Once done, your selected formula will be compressed and ready to paste into Notion:

![](<../.gitbook/assets/Fully Compressed Notion Formula.png>)

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
