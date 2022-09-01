# Count Multi-Select Tags

Here’s a database that contains a multi-select property called **Members.** How can we get the **number** of members that have been added to each row?

We can accomplish this by using the [replaceAll](../formula-components/functions/replaceall.md) function, as shown in the **Shares** formula:

![](<../.gitbook/assets/Split Counter.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/Count-multi-select-tags-8438a2a8c6e54e028e16ef595222a5c5" %}

## "Shares" Property Formula

Compressed:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
length(replaceAll(prop("Members"), "[^,]", "")) + 1
```
{% endcode %}

Expanded:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
/* Get the length of the string */

length(

	/* Convert the list of Members into a string of commas, 
	removing all other characters. */

  replaceAll(
    prop("Members"),
    "[^,]", // [^,] = every character EXCEPT `,`
    ""
  )
) + 1 // Add 1, since the last item in the Members string has no comma
```
{% endcode %}

The **Shares** formula counts the number of members listed in the **Members** multi-select property for each heist.

Notion doesn’t provide a default way to get this count (unless you use a Rollup), so we have to use the [replaceAll](../formula-components/functions/replaceall.md) function with a _regular expression._

<details>

<summary>What’s a regular expression?</summary>

Regular expressions are essentially combinations of characters that match patterns in a string of text.

These can be very complex, and it can take a while to learn how to use regular expressions comfortably. [RegexOne](https://regexone.com/) is a good resource for getting started.

</details>

Here’s how the formula works:

1. Pull the **Members** property into our formula. By default, multi-select property values are pulled in as a comma-separated string - e.g. `Danny, Rusty, Reuben, Linus`.
2. We call the [replaceAll](../formula-components/functions/replaceall.md) function, which finds a pattern in a string and replaces it with another pattern. We write our function as `replaceAll(prop("Members"), "[^,]", "")`:
   * The first argument - `prop("Members")` pulls in the Members property.
   * The second argument - `“[^,]”` - searches for _any character that isn’t `,`. This pattern is called an_ [_exclusion_](https://chortle.ccsu.edu/finiteautomata/Section07/sect07\_12.html)_**.**_
   * The third argument - `""` - replaces every found character with nothing, effectively removing them from the new string.
3. The `replaceAll` function returns a string of commas - e.g. `,,,,,,,,,,`.
4. We use the `length()` function to count the characters in our string of commas - e.g. `10`.
5. Since the last item in the original list of Members won’t have a comma in it, we add `1`.
6. The formula outputs the final Shares count as a number. For the **Bellagio Job,** that number is `11`.

## Splitting a Pool of Money

In the [divide](../formula-components/operators/divide.md) article, this **Heist Splitter** example was used to show how we could split a **Total** pool of money among the members who took part in each heist.

Here’s a new view of that database, which contains a new property called **Split (Full).** This formula efficiently combines the counting function we built above with the division operation, returning the share each heist member should get.

![](<../.gitbook/assets/Split Full.png>)

### View and Duplicate Database

{% embed url="https://thomasfrank.notion.site/Count-multi-select-tags-8438a2a8c6e54e028e16ef595222a5c5" %}

Here’s the code:

{% code overflow="wrap" lineNumbers="true" %}
```jsx
// Compressed
prop("Total") / (length(replaceAll(prop("Members"), "[^,]", "")) + 1)

// Expanded
prop("Total") / (  
	length(
    replaceAll(
      prop("Members"),
      "[^,]",
      ""
    )
  ) + 1 
)
```
{% endcode %}

#### About the Author

<img src="../.gitbook/assets/Notion Fundamentals with Thomas Frank - Avatar 2021 compressed (1).png" alt="" data-size="line"> My name is Thomas Frank, and I'm a [Notion-certified](https://www.credly.com/badges/95fae13a-17bf-4b4a-a3d2-d58c8a3e6a2a/public\_url) writer, YouTuber, and template creator. I've been using Notion since 2018 to organize my personal life and to run my business and YouTube channel. In addition to this formula reference, I've created a [free Notion course for beginners](https://thomasjfrank.com/fundamentals/) and several [productivity-focused Notion templates](https://thomasjfrank.com/templates/). If you'd like to connect, [follow me on Twitter](https://twitter.com/TomFrankly).
