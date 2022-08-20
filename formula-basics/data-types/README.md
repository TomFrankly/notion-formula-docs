# Data Types

Notion formulas can accept (and return) four different types of data:

| Data Type                                                  | Examples                 |   |
| ---------------------------------------------------------- | ------------------------ | - |
| [String](string.md)                                        | `"King of the Pirates"`  |   |
| [Number](number.md)                                        | `9001`                   |   |
| [Boolean](boolean-checkbox.md) (called Checkbox in Notion) | `true`, `false`          |   |
| [Date](date-data-type.md)                                  | `"2022-11-11T12:00:00Z"` |   |

When working with binary operators, you'll need to make sure that your operands share the same data type. Notion formulas do not do any kind of automatic type conversion.

{% hint style="info" %}
Good to know: Since Notion formulas don't do automatic type conversion, the equals (`==`) operator tests for **strict equality** (see the [JavaScript reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict\_equality) page on this)**.**&#x20;

E.g. `"1" == 1` will throw a Type Mismatch error in Notion. In JavaScript, it would return `true`.
{% endhint %}

Similarly, when working with functions, you'll need to ensure you're passing a supported data type for each argument. Fortunately, the Notion formula editor tells us which data types are supported/required for the arguments in each function.
