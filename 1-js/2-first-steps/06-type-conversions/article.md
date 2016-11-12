# Type Conversions

Most of time, operators and functions automatically convert a value to the right type. That's called "type coercion".

For example, `alert` automatically converts any value to a string, to show it. Or mathematical operations convert values to numbers.

There are also cases when we need to explicitly convert a value to put things right.

[cut]

```smart header="Not covering objects yet"
In this chapter we don't cover objects yet. Here we study primitives first, and then we'll add objects in the chapter [todo].
```

[todo where we cover them? link?]

## ToString

The string conversion happens when we need a string form of a value.

For example, `alert` does it:

```js run
let a = true;

alert(a); // "true"
```

We can also use a call `String(value)` function for that:

```js run
let a = true;
alert(typeof a); // boolean

*!*
a = String(a); // now: a = "true"
alert(typeof a); // string
*/!*
```

The string conversion is mostly obvious. A `false` becomes `"false"`, `null` becomes `"null"` etc.

## ToNumber

Numeric conversion happens in mathematical functions and expressions automatically.

For example, when division '/' is applied to non-numbers:

```js run
alert( "6" / "2" ); // 3, strings are converted to numbers
```

We can use a `Number(value)` function to explicitly convert a `value`:

```js run
let str = "123";
alert(typeof str); // string

let n = Number(str); // becomes a number 123

alert(typeof n); // number
```

The explicit conversion is usually required when we read a value coming from a text form field or another string-based source, but we expect a number to be entered.

If the string is not a valid number, the result of such conversion is `NaN`, for instance:

```js run
let age = Number("an arbitrary string instead of a number");

alert(age); // NaN, conversion failed
```

The numeric conversion rules:

| Value |  Becomes... |
|-------|-------------|
|`undefined`|`NaN`|
|`null`|`0`|
|<code>true&nbsp;and&nbsp;false</code> | `1` and `0` |
| `string` | Whitespaces from the start and the end are removed. Then, if the remaining string is empty, the result is `0`, otherwise -- the number is "read" from the string. An error gives `NaN`. |

Examples:

```js run
alert( Number("   123   ") ); // 123
alert( Number("123z") );      // NaN (error reading a number at "z")
alert( Number(true) );        // 1
alert( Number(false) );       // 0
```

Please note that `null` and `undefined` behave differently here: `null` becomes a zero, while `undefined` becomes `NaN`.

````smart header="Addition '+' concatenates strings"
Almost all mathematical operations convert values to numbers. With a notable exception of the addition `+`. If one of the added values is a string, then another one is also converted to a string.

Then it concatenates (joins) them:

```js run
alert( 1 + '2' ); // '12' (string to the right)
alert( '1' + 2 ); // '12' (string to the left)

alert( 1 + 2 ); // 3, numbers (for the contrast)
```

That only happens when one of arguments is a string. Otherwise values are converted to numbers.
````

## ToBoolean

Boolean conversion is the simplest one.

It happens in logical operations (later we'll meet condition tests and other kinds of them), but also can be performed manually with the call of `Boolean(value)`.

The conversion rule:

- Values that are intuitively "empty", like `0`, an empty string, `null`, `undefined` and `NaN` become `false`.
- Other values become `true`.

For instance:

```js run
alert( Boolean(1) ); // true
alert( Boolean(0) ); // false

alert( Boolean("hello") ); // true
alert( Boolean("") ); // false
```

````warn header="Please note: the string with zero `\"0\"` is `true`"
Some languages (namely PHP) treat `"0"` as `false`. But in JavaScript a non-empty string is always `true`.

```js run
alert( Boolean("0") ); // true
alert( Boolean(" ") ); // also true (any non-empty string is true)
```
````


## Summary

There exist three most widely used type conversions: to string, to number and to boolean.

`ToString`
: Happens when we output something, can be performed with `String(value)`. The conversion to string is usually obvious for primitive values.

`ToNumber`
: Happens in math operations, can be performed with `Number(value)`.

    The conversion follows the rules:

    | Value |  Becomes... |
    |-------|-------------|
    |`undefined`|`NaN`|
    |`null`|`0`|
    |<code>true&nbsp;/&nbsp;false</code> | `1 / 0` |
    | `string` | The string is read "as is", whitespaces from both sides are ignored. An empty string is  `0`. An error gives `NaN`. |

ToBoolean
: Happens in logical operations, or can be performed with `Boolean(value)`.

    Follows the rules:

    | Value |  Becomes... |
    |-------|-------------|
    |`0`, `null`, `undefined`, `NaN`, `""` |`false`|
    |any other value| `true` |


Most of these rules are easy to understand and memorize. The notable exceptions where people usually make mistakes are:

- `undefined` is `NaN` as a number.
- `"0"` is true as a boolean.

Objects are not covered here, we'll return to them in the special chapter, devoted exclusively to objects.

[todo link?]