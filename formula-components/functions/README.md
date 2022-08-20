---
description: Learn how to use the built-in functions within Notion formulas.
---

# Functions

In programming, a **function** is a reusable bundle or "chunk" of code. Functions have names which, when _called_ elsewhere in the program, execute the function's code.

Functions can also take in outside data (these are called **arguments),** and return new data.

In Notion formulas, you cannot define your own functions. However, Notion has provided many built-in functions you can use.

For example, the [length](length.md) function takes in a [string](../../formula-basics/data-types/string.md) argument and outputs a [number](../../formula-basics/data-types/number.md) equal the number of characters in that string.

{% code overflow="wrap" lineNumbers="true" %}
```javascript
length("Monkey D. Luffy") // Output: 15
```
{% endcode %}

Here's a list of every function available for use in a Notion formula. Click a function to learn more about how it works and see more examples.

| Function                          | Data Output Type | Example                                       | Output                           |
| --------------------------------- | ---------------- | --------------------------------------------- | -------------------------------- |
| [concat](concat.md)               | String           | `concat("Roronoa "," Zoro")`                  | Roronoa Zoro                     |
| [join](join.md)                   | String           | `join(", ","Luffy ","Zoro","Nami","Chopper")` | Luffy, Zoro, Chopper             |
| [slice](slice.md)                 | String           | `slice("Dangerfield",0,6)`                    | Danger                           |
| [length](length.md)               | Number           | `length("Monkey D. Luffy")`                   | 15                               |
| [format](format.md)               | String           | `format(4)`                                   | 4 _(as a string)_                |
| [toNumber](tonumber.md)           | Number           | `toNumber("42")`                              | 42 _(as a number)_               |
| [contains](contains.md)           | Boolean          | `contains("Monkey D. Luffy", "Luffy")`        | True                             |
| [replace](replace.md)             | String           | `replace("Pogo","Po","Dog")`                  | Doggo                            |
| [replaceAll](replaceall.md)       | String           | `replaceAll("Dogs Dogs Dogs","Dogs","Cats")`  | Cats Cats Cats                   |
| [test](test.md)                   | Boolean          | `test("Monkey D. Luffy", "Luffy")`            | True                             |
| [empty](empty.md)                 | Boolean          | `empty("")`                                   | True                             |
| [abs](abs.md)                     | Number           | `abs(-42)`                                    | 42                               |
| [cbrt](cbrt.md)                   | Number           | `cbrt(64)`                                    | 4                                |
| [ceil](ceil.md)                   | Number           | `ceil(4.2)`                                   | 5                                |
| [exp](exp.md)                     | Number           | `exp(2)`                                      | 7.389056098931                   |
| [floor](floor.md)                 | Number           | `floor(4.2)`                                  | 4                                |
| [ln](ln.md)                       | Number           | `ln(20)`                                      | 2.995732273554                   |
| [log10](log10.md)                 | Number           | `log10(1000)`                                 | 3                                |
| [log2](log2.md)                   | Number           | `log2(64)`                                    | 6                                |
| [max](max.md)                     | Number           | `max(3,5,4)`                                  | 5                                |
| [min](min.md)                     | Number           | `min(4,1,9,-3)`                               | -3                               |
| [round](round.md)                 | Number           | `round(4.5)`                                  | 5                                |
| [sign](sign.md)                   | Number           | `sign(-5)`                                    | -1                               |
| [sqrt](sqrt.md)                   | Number           | `sqrt(16)`                                    | 4                                |
| [start](start.md)                 | Date             | `start(prop("Date"))`                         | August 18, 2022                  |
| [end](end.md)                     | Date             | `end(prop("Date"))`                           | August 25, 2022                  |
| [now](now.md)                     | Date             | `now()`                                       | August 18, 2022 2:10 PM          |
| [timestamp](timestamp.md)         | Number           | `timestamp(now())`                            | 1660853460000                    |
| [fromTimestamp](fromtimestamp.md) | Date             | `fromTimestamp(1656012840000)`                | June 23, 2022 1:34 PM            |
| [dateAdd](dateadd.md)             | Date             | `dateAdd(now(),3,"months")`                   | November 18, 2022 2:11 PM        |
| [dateSubtract](datesubtract.md)   | Date             | `dateSubtract(now(),3,"months")`              | May 18, 2022 2:11 PM             |
| [dateBetween](datebetween.md)     | Number           | `dateBetween(now(),prop("Date"),"days")`      | 9                                |
| [formatDate](formatdate.md)       | String           | `formatDate(now(), "MMMM DD YYYY")`           | August 18 2022                   |
| [minute](minute.md)               | Number           | `minute(now())`                               | 9                                |
| [hour](hour.md)                   | Number           | `hour(now())`                                 | 14                               |
| [day](day.md)                     | Number           | `day(now())`                                  | 4                                |
| [date](date.md)                   | Number           | `date(now())`                                 | 18                               |
| [month](month.md)                 | Number           | `month(now())`                                | 7                                |
| [year](year.md)                   | Number           | `year(now())`                                 | 2022                             |
| [id](id.md)                       | String           | `id()`                                        | c5d67d15854744869cc4a062fb7b1377 |

## Functions as Arguments

Functions can accept other functions as arguments, so long as the inner function outputs the [data type](../../formula-basics/data-types/) that the outer function requires.

Here are a couple examples:

{% code overflow="wrap" lineNumbers="true" %}
```javascript
slice(format(1932),0,2)
// Output: 19

// Expanded form
slice(
    format(1932),
    0,
    2
)

---

// Get the century name (e.g. "20th") from a year (expressed as a number)
concat(format(add(toNumber(slice(format(1932),0,2)),1)),"th") 
// Output: 20th

// Expanded form
concat(
    format(
        add(
            toNumber(
                slice(
                    format(1932),
                    0,
                    2
                )
            ),
            1
        )
        ),
    "th"
)
```
{% endcode %}

For more examples, see the **example databases** for most of the functions. The majority in this reference use other functions as arguments in order to do useful things. To start, I'll recommend checking out the [format](format.md) function's example database.

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
