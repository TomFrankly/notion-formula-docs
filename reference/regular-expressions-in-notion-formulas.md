---
description: >-
  Learn how to use regular expressions in Notion's test(), replace(), and
  replaceAll() functions.
---

# Regular Expressions in Notion Formulas

Notion supports the use of regular expressions in three functions:

* [test](../formula-components/functions/test.md) - tests whether a string contains a regular expression. Outputs a [Boolean](../formula-basics/data-types/boolean-checkbox.md) true or false value.
* [replace](../formula-components/functions/replace.md) - matches a single instance of a regular expression within a string and replaces it with a specified replacement string.
* [replaceAll](../formula-components/functions/replaceall.md) - matches **all** instances of a regular expression and replaces them with a specified replacement string.

By using regular expressions within these functions, it is possible to do many kinds of string manipulation within Notion formulas.

## What is a Regular Expression?

A **regular expression** (often called a _regex_) is simply a set of instructions that tells a regular expression engine how to search through an **input string** in order to find one or more **matches.**

Regular expressions can often look very complex:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Bruce Thomas Wayne", "^[-\\w]+\\b\\s?(.*)\\b\\s[-\\w]+$", "$1")
// Output: Thomas
```
{% endcode %}

However, they can also be very simple. This is also a regular expression:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("My cat is cute", "cat", "dog")
// Output: My dog is cute
```
{% endcode %}

This expression would tell the regex engine to search the input string for a sub-string that matches “cat". The [replace](../formula-components/functions/replace.md) function then replaces it with "dog".

A simple match like this could also be found using the [contains](../formula-components/functions/contains.md) function:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
contains("My cat is cute","cat")
// Output: true
```
{% endcode %}

But what if you need to be more flexible with your search criteria?

Take this problem, for instance: Which of these strings contains the word “cat”?

* I have six cats.
* My dog catches fish.
* Cat food is expensive.

Here, `contains()` runs into trouble ([see this in an example database](https://thomasfrank.notion.site/Cats-f93c5656154240c8a9793d072a56b477)):

{% code overflow="wrap" lineNumbers="true" %}
```jsx
contains("I have six cats.","cat") // true

contains("My dog catches fish.","cat") // true, should be false

contains("Cat food is expensive","cat") // false, should be true
```
{% endcode %}

`contains()` gets the first one right, but fails on the other two.

On the second string, it sees “cat” inside the word “catches”. On the third string, it fails to see “Cats” because `contains()` is case-sensitive.

This is where a regular expression can help us!&#x20;

Regular expressions let us define **character groups,** make characters **optional,** check for **word boundaries,** and so much more.

Here’s how you could check all three of these strings correctly using the test function:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
test("I have six cats.", "\\b[Cc]ats?\\b") // true

test("My dog catches fish.", "\\b[Cc]ats?\\b") // false

test("Cat food is expensive", "\\b[Cc]ats?\\b") // true
```
{% endcode %}

The regular expression we’re checking for here is `\\b[Cc]ats?\\b`. Let’s break it down:

* `\\b` is a special character that translates to “word boundary”. It’s not a space character; it’s the boundary between a **word character** and a **non-word character.** In Notion, word characters include `A-z`, `0-9`, and `_`.
* `[Cc]` is a **character class.** The brackets `[]` define a group of characters (`C` and `c`), and the regex engine will try to match any one of them. This allows us to check for both “Cat” and “cat”.
* `?` denotes that the preceding character is optional. It can appear **zero or one times** in the match. Since the `s` precedes it, this allows us to include the plural “cats” as well as the singular “cat”.

Breaking all this down to plain English, our regular expression is essentially saying:

> Match any of the words “Cat, cat, Cats, or cats”.

Doing this with `contains()` would be really inefficient. You’d need to string together many, many `contains()` instances using [or](../formula-components/operators/or.md) clauses in order to account for the many variables – not just plurality and capitalization, but word boundaries as well!

By giving us special characters to work with, regular expressions essentially give us a new language that we can use to define _exactly_ what we’re looking for in the input string.

Once we’ve got our match (or matches), we can use Notion’s [test](../formula-components/functions/test.md), [replace](../formula-components/functions/replace.md), and [replaceAll](../formula-components/functions/replaceall.md) functions to do incredibly useful things with them.

## Learn Regular Expressions

This page isn’t intended to be a full tutorial on writing regular expressions. It’s a reference on how to use them in Notion formulas, and on what particular regex characters are supported in Notion.

If you’re interested in learning regular expressions, here are a few resources I recommend:

* [RegexOne](https://regexone.com/) - start here. This is the best beginner tutorial you’ll find.
* [Regular-Expressions.info](https://www.regular-expressions.info/quickstart.html) - a gold mine of regular expression tutorials and explanations
* [RexEgg](https://www.rexegg.com/) - another fantastic general resource for learning regex
* [.NET Regular Expressions Quick Reference](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference) - intended for .NET developers, but still quite handy as a general resource.
* [Regex101](https://regex101.com/) - a tool for building and testing regular expressions.

{% hint style="info" %}
When using Regex101, note that Notion requires double backslashes `\\` to escape characters, while Regex101 (and most regex engines) only require a single backslash `\`. The expression at [https://regex101.com/r/WffTEp/1](https://regex101.com/r/WffTEp/1) would need to be written as `^[-\\w]+\\b\\s?(.*)\\b\\s[-\\w]+$` in Notion.
{% endhint %}

## Supported Regular Expression Characters

This section includes one or more examples for every regular expression feature supported within Notion’s formula editor.

See working examples for all of these features here:

{% embed url="https://thomasfrank.notion.site/Supported-Regular-Expression-Characters-in-Notion-Formulas-d49f419410c14ce8b3cf7c90a08ceab5" %}

### Character Escapes

Working examples:

{% embed url="https://thomasfrank.notion.site/Character-Escapes-b0401a4a68194fe5b899dd2cb125c795" %}

#### `\\u0000` - **escaped Unicode reference**

**Note:** Only works in the regular expression argument. Unicode characters can be typed elsewhere with a single backslash `\` (e.g. `\u0041`), but they will be automatically converted to their corresponding character in the formula editor upon exiting it.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
test("A","\\u0041") // Output: True
```
{% endcode %}

#### `\\000` - octal character reference

**Note:** Only works in the regular expression argument. Doesn’t work in the input string or replacement string arguments.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
test("A","\\101") // Output: True
```
{% endcode %}

#### `\\x00` - hexadecimal character reference

**Note:** Only works in the regular expression argument. Doesn’t work in the input string or replacement string arguments.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
test("A","\\x41") // Output: True
```
{% endcode %}

You can find a list of all Unicode, octal, and hexadecimal reference codes here:

{% embed url="https://www.techonthenet.com/unicode/chart.php" %}

#### `\\n` - new line

Note that `\n` is used in the input string and replacement arguments, but `\\n` must be used in the regular expression.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("Apple\nBanana\nOrange", "\\n", "\n\n")
/* Output:
Apple

Banana

Orange
```
{% endcode %}

There are also several characters that must escaped with double backslashes (`\\`) in order to be represented normally. These characters are used as special characters within regular expressions if they are not escaped.

| Character               | Escape |
| ----------------------- | ------ |
| Period - `.`            | `\\.`  |
| Question mark - `?`     | `\\?`  |
| Dollar sign - `$`       | `\\$`  |
| Asterisk - `*`          | `\\*`  |
| Plus sign - `+`         | `\\+`  |
| Caret - `^`             | `\\^`  |
| Left parenthesis - `(`  | `\\(`  |
| Right parenthesis - `)` | `\\)`  |
| Left bracket - `[`      | `\\[`  |
| Right bracket - `]`     | `\\]`  |
| Left curly brace - `{`  | `\\{`  |
| Right curly brace - `}` | `\\}`  |
| Pipe - `\|`             | `\\\|` |
| Forward slash - `/`     | `\\/`  |
| Backslash `\`           | `\\\\` |

Single quotations (`'`) and double quotations (`"`) must also be escaped, but they can only be escaped by escaping their unicode number. See the section below on [Escaping Unicode Numbers](regular-expressions-in-notion-formulas.md#unicode-numbers-in-regular-expressions).

### Character Classes

Learn about character classes:

{% embed url="https://www.regular-expressions.info/shorthand.html" %}

Working examples:

{% embed url="https://thomasfrank.notion.site/Character-Classes-804da8d12639435bbe6e448aa61807a1" %}

#### `\\w` - alphanumeric character

{% hint style="info" %}
Notion considers [non-spacing marks](https://www.fileformat.info/info/unicode/category/Mn/list.htm) to be non-alphanumeric characters. Other regex engines (.NET, for example) do the opposite.
{% endhint %}

| Lowercase letters              | `a-z`                    |
| ------------------------------ | ------------------------ |
| Uppercase letters              | `A-Z`                    |
| Numbers                        | `0-9`                    |
| Punctuation, Connector symbols | Notion only supports `_` |

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("CAPS_nocap 12345", "\\w", "*")
// Output: ********** *****
```
{% endcode %}

#### `\\W` - non-alphanumeric character

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("correct horse battery staple", "\\W", "")
// Output: correcthorsebatterystaple
```
{% endcode %}

#### `\\d` - digit character (0-9)

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll(id(), "\\d", "")
// Output: ccadaecddeabaeeb (where ID is ccad6aec4dd34e5a942334bae3e9b728)
```
{% endcode %}

#### `\\D` - non-digit character

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll(id(), "\\D", "")
// Output: 6434594233439728 (where ID is ccad6aec4dd34e5a942334bae3e9b728)
```
{% endcode %}

#### `\\s` - whitespace character

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("charmander man bun", "\\sman\\s", " ")
// Output: charmander bun
```
{% endcode %}

#### `\\S` - non-whitespace character

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("charmander man bun", "\\Sman\\S", "ndl")
// Output: chandler man bun
```
{% endcode %}

#### `.` - wildcard; matches any single character _except_ newline (\\\n)

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("And blimey, if it ain't mutton again today!", ".", "😡")
// Output: 😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡

// Include newlines using (.|\\n)
// Assume prop "TwoLines" contains:
    // And blimey,
    // if it ain't
    // mutton again today!
replaceAll(prop("TwoLines"),"(.|\\n)","😡")
// Output: 😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡😡
```
{% endcode %}

#### `[]` - character class (matches any single character included in the group)

Character classes support ranges such as `A-Z` (all uppercase character), `A-z` (all upper and lowercase characters), and `0-9` (all digits).&#x20;

Commas may also be used to visually separate ranges and characters in your expression, but they are not needed.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("gold fold bold","[gfb]","t")
// Output: told told told

replaceAll("27 dresses","[a-z]","👗")
// Output: 27 👗👗👗👗👗👗👗

replaceAll("abcdefghijklmnopqrstuvwxyz123456789", "[a-ev-z1357-9]", "🙄")
// With commas:
replaceAll("abcdefghijklmnopqrstuvwxyz123456789", "[a-e,v-z,1,3,5,7-9]", "🙄")
// Output: 🙄🙄🙄🙄🙄fghijklmnopqrstu🙄🙄🙄🙄🙄🙄2🙄4🙄6🙄🙄🙄
```
{% endcode %}

Character class subtraction is not supported.

#### `[^]` - negated character class (matches any single character not included in the group)

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("123456789abcdefghijklmnopqrstuvwxyz", "[^a-z]", "")
// Output: abcdefghijklmnopqrstuvwxyz

replaceAll("abcdefghijklmnopqrstuvwxyz123456789", "[^cow]", "")
// Output: cow ("c","o","w" are in alphabetical order naturally. The character class doesn't specificy order.)
```
{% endcode %}

### Quantifiers

Learn about quantifiers:

{% embed url="https://www.regular-expressions.info/repeat.html" %}

Working examples:

{% embed url="https://thomasfrank.notion.site/Quantifiers-823f68c07be14f069437761828d831eb" %}

#### `*` - match zero or more of the preceding element

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("Trs Tres Trees Treeeeees", "Tre*s", "🌳")
// Output: 🌳 🌳 🌳 🌳

replaceAll("Trs Tres Trees Treees Treeees", "Tr(ee)*s", "🌳")
// Output: 🌳 Tres 🌳 Treees 🌳
```
{% endcode %}

#### `+` - match one or more of the preceding element

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("Trs Tres Trees Treeeeees", "Tre+s", "🌳")
// Output: Trs 🌳 🌳 🌳

replaceAll("Trs Tres Trees Treees Treeees", "Tr(ee)+s", "🌳")
// Output: Trs Tres 🌳 Treees 🌳
```
{% endcode %}

#### `?` - preceding element is optional; match it zero or one times

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("Trs Tres Trees Treeeeees", "Tre?s", "🌳")
// Output: 🌳 🌳 Trees Treeeeees

replaceAll("Trs Tres Trees Treees Treeees","Tr(ee)?s","🌳")
// Output: 🌳 Tres 🌳 Treees Treeees
```
{% endcode %}

#### `??` - match preceding element zero or one times (as few times as possible)

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("Trs Tres Trees Treees Treeees", "Tre??s", "🌳")
// Output: 🌳 🌳 Trees Treees Treeees

replaceAll("Trs Tres Trees Treees Treeees", "Tr(ee)??s", "🌳")
// Output: 🌳 Tres 🌳 Treees Treeees
```
{% endcode %}

#### `+?` - match preceding element one or more times (as few times as possible)

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Tree", "Tre+?", "🌳")
// Output: 🌳e
```
{% endcode %}

#### `*?` - match preceding element zero or more times (as few times as possible)

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Heeeeeeelp", "H.*?", "*")
// Output: *eeeeeeelp

replace("Heeeeeeelp", "H.*?l", "*")
// Output: *p
```
{% endcode %}

#### `{n}` - match the preceding element _n_ times

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Heeeeeeelp", "e{7}", "*")
// Output: H*lp
```
{% endcode %}

#### `{n,}` - match the preceding element _n_ or more times

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Heeeeeeelp", "e{1,}", "*")
// Output: H*lp
```
{% endcode %}

#### `{n,m}` - match the preceding element between _n_ and _m_ times (inclusive)

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Heeeeeeelp", "e{1,6}", "*")
// Output: H*elp
```
{% endcode %}

#### `{n}?` - match the preceding element _n_ times (no difference from `{n}`

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Heeeeeeelp", "e{7}?", "*")
// Output: H*lp
```
{% endcode %}

#### `{n,}?` - match the preceding element at least _n_ times, but as few times as possible

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Heeeeeeelp", "e{1,}?", "*")
// Output: H*eeeeeelp
```
{% endcode %}

#### `{n,m}?` - match the preceding element at least _n_ times, no more than _m_ times, and as few times as possible

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Heeeeeeelp", "e{1,6}?", "*")
// Output: H*eeeeeelp
```
{% endcode %}

### Anchors

Learn about anchors:

{% embed url="https://www.regular-expressions.info/anchors.html" %}

Working examples:

{% embed url="https://thomasfrank.notion.site/Anchors-9a740d5f333544ee97384c5cc8dc1ac9" %}

#### `^` - start of line

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("dogs dogs dogs", "^dogs", "cats")
// Output: cats dogs dogs
```
{% endcode %}

#### `$` - end of line

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("dogs dogs dogs", "dogs$", "cats")
// Output: dogs dogs cats
```
{% endcode %}

#### `\\b` - word boundary

This is **not** a space (that’s `\\s`). This is the boundary _between_ a word character and a non-word character (including punctuation such as `,`, `.`, `;`, etc.). It is a [zero-length match](https://www.regular-expressions.info/zerolength.html).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("martini art artist", "\\bart", "!!!")
// Output: martini !!! !!!ist

replaceAll("martini art artist", "\\bart\\b", "!!!")
// Output: martini !!! artist
```
{% endcode %}

#### `\\B` - not on a word boundary

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("martini art artist", "\\Bart", "!!!")
// Output: m!!!ini art artist
```
{% endcode %}

### Character Grouping

Learn about character grouping and capturing:

{% embed url="https://www.regular-expressions.info/brackets.html" %}

Working examples:

{% embed url="https://thomasfrank.notion.site/Character-Grouping-352c8e800d524c48912f08f8e8e3b74e" %}

#### `()` - capture group (is automatically assigned a sequential reference number)

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Dog Blog", "(Dog) Blog", "$1")
// Output: Dog

replace("Dog Blog", "(Dog) (Blog)", "$2")
// Output: Blog

replaceAll("Jack Sparrow", "^(\\w+)\\b.*", "$1")
// Output: Jack
```
{% endcode %}

#### `(?<name>expression)` - named capture group

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Jack plays poker", "(?<sup>J).*(oker)", "$<sup>$2")
// Output: Joker

// Named capture groups are still assigned their sequential number
// Note the output when I reference "$<sup>$1" instead of "$<sup>$2"
replace("Jack plays poker", "(?<sup>J).*(oker)", "$<sup>$1")
// Output: JJ
```
{% endcode %}

#### `(?:)` - non-capturing group

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Jack", "(?:Jack)", "$1")
// Output: $1

replace("123", "(\\w)(?:\\w)(\\w)", "$2")
// Output: 3
```
{% endcode %}

### Substitutions

Learn about substitutions:

{% embed url="https://www.regular-expressions.info/replacebackref.html" %}

Working examples:

{% embed url="https://thomasfrank.notion.site/Substitutions-dd1586a80d1c41148bbb511aa2418973" %}

#### `$n` - capture group numbers

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Dog Blog", "(Dog) Blog", "$1")
// Output: Dog

replace("Dog Blog", "(Dog) (Blog)", "$2")
// Output: Blog
```
{% endcode %}

#### `$&` - copy of the whole match

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("Hello", ".*", "$& $& $&")
// Output: Hello Hello Hello

replaceAll("I sell pan and pan accessories", "pan", "pro$&e")
// Output: I sell propane and propane accessories
```
{% endcode %}

#### `` $` `` - copy of the entire input string before the match

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("badboy","boy","$`")
// Output: badbad
```
{% endcode %}

#### `$'` - copy of the entire input string after the match

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("badboy", "bad", "$'")
// Output: boyboy
```
{% endcode %}

### Backreferences

Learn about backreferences:

{% embed url="https://www.regular-expressions.info/backref.html" %}

Working examples:

{% embed url="https://thomasfrank.notion.site/Backreferences-b5358a96949a432eb16320d1a493b836" %}

#### `\\n` - e.g. `\\1` - backreference. Must match an existing capture group

Note that the backreference looks for matches of the _content_ of its capture group. It is not an alias for the expression within the capture group.

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("12-12-12", "([0-9]+)-\\1-\\1", "Success")
// Output: Success

replace("12-34-56", "([0-9]+)-\\1-\\1", "Success")
// Output: 12-34-56

replace("I have 56 apples, 35 bananas, and 35 grapes.", ".*(56).*(35).*\\2.*", "Success")
// Output: Success
```
{% endcode %}

#### `(?<name>\\w) \\k<name>` - named backreference

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("I have 56 apples, 35 bananas, and 35 grapes.", ".*(56).*(?<two>35).*\\k<two>.*", "Success")
// Output: Success

// Named backreferences can still be called with their sequential number
replace("I have 56 apples, 35 bananas, and 35 grapes.", ".*(56).*(?<two>35).*\\2.*", "Success")
// Output: Success
```
{% endcode %}

### Alternation

Learn about alternations:

{% embed url="https://www.regular-expressions.info/alternation.html" %}

Working examples:

{% embed url="https://thomasfrank.notion.site/Alternation-f1546e6762304412868f48669735f5d9" %}

#### `|` - either/or

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replaceAll("jpg, jpeg, png, gif, wav", "jpg|jpeg|png|gif", "picture")
// Output: picture, picture, picture, picture, wav

// Order matters!

replace("mould", "ou|o", "😀")
// Output: m😀ld

replace("mould", "o|ou", "😀")
// Output: m😀uld

// Alternation can also be done inside groups:

replaceAll("My name is Bruce Wayne", "(Bruce|Wayne)", "*****")
// Output: My name is ***** *****
```
{% endcode %}

### Unsupported Features

The following features are currently not supported in Notion's flavor of regex:

* `\\A`
* `\\z`
* `\\Z`
* `\\p{name}`
* `\\P{name}`
* `$+`
* `$_`
* `(?>*subexpression*)`
* `(?(expression) yes | no)`
* Lookarounds are not fully supported due to [lack of support in all variants of Safari](https://caniuse.com/js-regexp-lookbehind). Not recommended to use them in your formulas.
* [Flags/modifiers](https://www.regular-expressions.info/modifiers.html) are not supported in Notion at all (which often makes case-insensitive matching very tedious)

## Unicode Numbers in Regular Expressions

When writing regular expressions in Notion formulas, it is possible to “hard code” Unicode numbers into your expression. The regex engine will then parse these as their actual Unicode characters. (Thanks to [Ben Borowski](https://twitter.com/typeoneerror) for pointing this out to me).

To do so, use double-backslashes `\\` to escape the Unicode reference:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// \\u0027 escapes apostrophes. 
// \\u2018 and \\u2019 handle left and right single quotes.
replaceAll("Mike 'Iron Mike' Tyson", "[\\u0027\\u2018\\u2019]","🥊")
// Output: Mike 🥊Iron Mike🥊 Tyson
```
{% endcode %}

See a working example of this:

{% embed url="https://thomasfrank.notion.site/Unicode-Numbers-in-Regular-Expressions-688f3bcc259f432da6b576066e1cd669" %}

It is also possible to use octal or hex codes here. For example:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
test("A", "\\x41") // Output: true

test("A", "\\101") // Output: true
```
{% endcode %}

These `\\` Unicode references don’t work in input string argument, nor the replacement argument within [replace](../formula-components/functions/replace.md) and [replaceAll](../formula-components/functions/replaceall.md). They’ll only be interpreted correctly within the regular expression argument.

If you type a Unicode character’s code anywhere within a Notion formula (besides a regular expression argument) using only a single backslash `\`, it’ll automatically be transformed into that character – within the formula itself (this does not work for hex and octal codes).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
"\u0041" is automatically turned into "A"
```
{% endcode %}

### Escaping Double Quotations

You can usually escape a double quotation `"` in a Notion formula using a single backslash `\`:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
"Mike \"Iron Mike\" Tyson" 
// Output: Mike "Iron Mike" Tyson
```
{% endcode %}

This also works in the input-string and replacement arguments within Notion’s regular expression functions:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Mike \"Iron Mike\" Tyson", "^(\\w+)\\b","\"$1\"") 
// Output: "Mike" "Iron Mike" Tyson
```
{% endcode %}

However, this _does not_ work inside of regular expressions – i.e., the second argument of the [test](../formula-components/functions/test.md), [replace](../formula-components/functions/replace.md), and [replaceAll](../formula-components/functions/replaceall.md) functions.

Fortunately, you can get around this by hard-coding their Unicode character codes into your expression:

* `\\u0022` for a normal quotation mark
* `\\u201c` for a left double quotation mark
* `\\u201d` for a right double quotation mark

For example, here’s how you could extract `"Iron Mike"` from `Mike "Iron Mike" Tyson`:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
replace("Mike \"Iron Mike\" Tyson", ".*([\\u0022\\u201c\\u201d][^\\u0022\\u201c\\u201d]+[\\u0022\\u201c\\u201d]).*", "$1")
// Output: "Iron Mike"
```
{% endcode %}

See a working example of this:

{% embed url="https://thomasfrank.notion.site/Unicode-Numbers-in-Regular-Expressions-688f3bcc259f432da6b576066e1cd669" %}

It’s best to ensure your character class includes all three common quotation marks: `[\\u0022\\u201c\\u201d]`

When you type a quotation mark directly into the formula editor, you’ll get a normal quotation mark `"` – however, when you type within text fields inside a Notion database, Notion intelligently uses left `“` and right `”` quotation marks to wrap your text.

In the example above, I hard-coded `Mike \"Iron Mike\" Tyson` within the formula editor. However, if that string had been pulled in via another property (e.g. `prop("Name")`), then it would likely be using left `“` and right `”` quotation marks.

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
