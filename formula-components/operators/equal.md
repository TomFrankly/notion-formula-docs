---
description: Learn how to use the Boolean "equal" (==) operator in Notion formulas.
---

# equal

The equality (`==`) operator returns [true](../constants/true.md) if its operands are equal. It accepts operands of all [data types](../../formula-basics/data-types/) - [strings](../../formula-basics/data-types/string.md), [numbers](../../formula-basics/data-types/number.md), [Booleans](../../formula-basics/data-types/boolean-checkbox.md), and [dates](../../formula-basics/data-types/date-data-type.md).

{% code overflow="wrap" lineNumbers="true" %}
```jsx
string == string
number == number
Boolean == Boolean
date == date

equal(string, string)
equal(number, number)
equal(Boolean, Boolean)
equal(date, date)
```
{% endcode %}

{% hint style="info" %}
**Good to know:** Notion does not allow for comparisons between different [data types](../../formula-basics/data-types/), so the strict equality operator `===` is not supported (_or rather, the equality operator (\`==\`) is already a strict equality operator)_. You must convert all data to a common type before making a comparison (e.g. by using [format()](../functions/format.md) to create a string value).
{% endhint %}

You can also use the function version, `equal()`.

## Example Formulas

{% code overflow="wrap" lineNumbers="true" %}
```jsx
1 == 1 // Output: True

equal(1,1) // Output: True

1 == 2 // Output: False

"1" == 1 // Type mismatch error

+"1" == 1 // Output: True (uses the unaryPlus operator to convert "1" to a number

2^2 == 4 // Output: True

length("Monkey D. Luffy") == 15 // Output: True
```
{% endcode %}

{% hint style="info" %}
**Good to know:** The equality (`==`) operator _cannot_ be chained in a Notion formula. A formula like `1 == 1 ==1` won't work. Use the [and](and.md) operator to get around this - e.g. `1 == 1 and 1 == 1`.
{% endhint %}

## Example Database

The example database below shows several rows with random dates. The **Last Weekday** property displays the last weekday in that date’s month, and then the **Day Name** property shows which day of the week it is.

![](<../../.gitbook/assets/Last Weekday of the Month.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/equal-461f9393ef0e401aad5e778055cd1539" %}

{% hint style="success" %}
**Want a simpler example?** Check out the one on the [inequality](unequal.md) (`!=`) operator's page. These operators are opposites, but their usage (and [operator precedence](../../reference/operator-precedence-and-associativity.md)) is the same.
{% endhint %}

### Last Weekday Explanation

To get the last weekday of the month in a Notion formula, we follow this process:

1. First, obtain the last day of the month:
   1. Add 1 month to the current date in the Date property, using [dateAdd()](../functions/dateadd.md).
   2. Subtract `x` days from the resulting date using [dateSubtract()](../functions/datesubtract.md), where `x` is that date's date index (E.g. `June 11` would have a date index of `11`)
   3. Since all months start on the 1st, this will always get you to the last day of the preceding month. (e.g. `June 11 - 11 == May 31`).
2. Next, check if the last day of the month is a Sunday using [date()](../functions/date.md). If so, subtract 2 days from it and output the resulting date, which will be a Friday.
3. If the last day of the month isn't a Sunday, check if it's a Saturday. If so, subtract 1 day from it and output the resulting date, which will be a Friday.
4. If the last day of the month isn't a Sunday or Saturday, simply output it.

To keep this example simple and easy to follow, I've created the **Last Day** property to act as a variable that we can call from the **Last Weekday** formula.

{% hint style="warning" %}
**Good to know:** You can't explicitly define variables in a Notion formula, so you'll need to use a separate property for each variable instead.
{% endhint %}

Finally, the **Day Name** property uses the [formatDate()](../functions/formatdate.md) function to display the actual day of the week that corresponds to **Last Weekday's** date.

### "Last Weekday" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Compressed
if(day(prop("Last Day")) == 0, dateSubtract(prop("Last Day"),2,"days"), if(day(prop("Last Day")) == 6, dateSubtract(prop("Last Day"),1,"days"),prop("Last Day")))

// Expanded and Commented
if(

    // Check if the day of the week index for Last Day
    // is 0 (Sunday).
    day(
        prop("Last Day")
    ) == 0, 
    
    // If it is 0, subtract 2 days from Last Day to arrive at the
    // nearest weekday (Friday).
    dateSubtract(
        prop("Last Day"), 2, "days"
    ),
    
    // If it isn't 0, next check if the day of the week index
    // for Last Day is 6 (Saturday).
    if(
        day(
            prop("Last Day")
        ) == 6, 
        
        // If it is 6, subtract 1 day from Last Day to arrive at
        // the nearest weekday (Friday).
        dateSubtract(
            prop("Last Day"), 1, "days"
        ),
        
        // If the day of the week index isn't 0 or 6, output the
        // Last Day property as-is.
        prop("Last Day")
    )
)
```
{% endcode %}

### "Last Day" Property Formula

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
dateSubtract(dateAdd(prop("Date"), 1, "months"), date(dateAdd(prop("Date"), 1, "months")), "days")

// Expanded and Commented

// Get the last day of the current month by adding 1 month to the current Date,
// then subtracting the number of days in that date's date() index.
dateSubtract(

    // Add 1 month to the current date.
	// E.g. - May 11 + 1 month == June 11
    dateAdd(
        prop("Date"), 1, "months"
    ),

    // Get the number of days to be subtracted using the date()
	// function. E.g. - June 11 == 11 
    date(
        dateAdd(
            prop("Date"), 1, "months"
        )
    ), 

    // Specify the date unit to be subtracted; in this case, "days"
    "days"
)
```
{% endcode %}

<details>

<summary>Combined Formula without Using "Last Day" Property</summary>

If you're curious, here's how you could create a single mega-formula that can find the last weekday of the month without the need for a **Last Day** variable property:

```javascript
// Compressed
if(day(dateSubtract(dateAdd(prop("Date"), 1, "months"), date(dateAdd(prop("Date"), 1, "months")), "days")) == 0, dateSubtract(dateSubtract(dateAdd(prop("Date"), 1, "months"), date(dateAdd(prop("Date"), 1, "months")), "days"),2,"days"), if(day(dateSubtract(dateAdd(prop("Date"), 1, "months"), date(dateAdd(prop("Date"), 1, "months")), "days")) == 6, dateSubtract(dateSubtract(dateAdd(prop("Date"), 1, "months"), date(dateAdd(prop("Date"), 1, "months")), "days"),1,"days"), dateSubtract(dateAdd(prop("Date"), 1, "months"), date(dateAdd(prop("Date"), 1, "months")), "days")))

// Expanded and Commented
if(
    
    // Get the day of the week index for the last day of Date's month,
    // and see if it equals 0 (Sunday)
    day(
        
        // Output the last day of Date's month, by first
        // adding one month to Date, then subtracting that date's
        // date() value. Example: 
            // May 11 + 1 month == June 11
            // June 11 - 11 == May 31
        dateSubtract(
            dateAdd(
                prop("Date"), 1, "months"
            ),
            date(
                dateAdd(
                prop("Date"),1,"months")
            ),
            "days"
        )
    ) == 0,
    
    // If the day of the week index does match 0 (Sunday), then
    // subtract 2 days to get to a weekday (Friday)
    dateSubtract(
        dateSubtract(
            dateAdd(
                prop("Date"), 1, "months"
            ),
            date(
                dateAdd(
                    prop("Date"), 1, "months"
                )
            ),
            "days"
        ),
        2,
        "days"
    ),
    
    // If the day of the week index does NOT match 0 (Sunday), next
    // check if it matches 6 (Saturday).
    if(
        day(
            dateSubtract(
                dateAdd(
                    prop("Date"), 1, "months"
                ),
                date(
                    dateAdd(
                        prop("Date"), 1, "months"
                    )
                ),
                "days"
            )
        ) == 6,
        
        // If the day of the week index does match 6 (Saturday),
        // subtract 1 day from that date to get to the nearest
        // weekday (Friday).
        dateSubtract(
            dateSubtract(
                dateAdd(
                    prop("Date"), 1, "months"
                ),
                date(
                    dateAdd(
                        prop("Date"), 1, "months"
                    )
                ),
                "days"
            ),
            1,
            "days"
        ),
        
        // If the day of the week index did not match 0 (Sunday) or
        // 6 (Saturday), then output the date as-is.
        dateSubtract(
            dateAdd(
                prop("Date"), 1, "months"
            ),
            date(
                dateAdd(
                    prop("Date"), 1, "months"
                )
            ),
            "days"
        )
    )
)
```

If you take the time to read the formula fully, you'll notice that we're just repeating the formula within the **Last Day** property multiple times - precisely, everythere I called `prop("Last Day")` in the simpler **Last Week** formula above.

This is the trade-off with Notion formulas; since you can't define variables in a formula, you can either create "helper" properties that hold variables, or you can create monster formulas that perform the same functions multiple times.

</details>

#### Other formula components used in this example:

{% content-ref url="if.md" %}
[if.md](if.md)
{% endcontent-ref %}

{% content-ref url="../functions/dateadd.md" %}
[dateadd.md](../functions/dateadd.md)
{% endcontent-ref %}

{% content-ref url="../functions/datesubtract.md" %}
[datesubtract.md](../functions/datesubtract.md)
{% endcontent-ref %}

{% content-ref url="../functions/date.md" %}
[date.md](../functions/date.md)
{% endcontent-ref %}

{% content-ref url="../functions/day.md" %}
[day.md](../functions/day.md)
{% endcontent-ref %}

{% content-ref url="../functions/formatdate.md" %}
[formatdate.md](../functions/formatdate.md)
{% endcontent-ref %}

#### About the Author

<img src="../../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
