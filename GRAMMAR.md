# `<lang>` Grammar

`<lang>` is largely focused on a sensible and readable grammar that puts developers first.
As such, the language was designed with mnemonics in mind which largely influenced various
parts of the language (i.e. keywords, constructs, etc.).

## Character Encoding

`<lang>` code can include any UTF-8 character with the following exceptions:
- [TODO]

## Comments
> Comments are **not** ignored during parsing and are available to compilation layers for use.
> 
> Unlike other languages, comments are not purely documentation. They serve to inform both
> the developer and the compiler on aspects of the program that may not be obvious. In order
> to warrant compiler hinting, hinting comments are equivalent to single line comments but
> are prefixed with `//!` instead. See [Compiler Hints]() below for more information on their
> usage. 

Two variants of comments are offered:
- Single-line comments are prefixed with `//` and include all contents until a newline.
```
// This is a single-line comment.
let _: u8 = 17; // It can follow any line. 
```
- Multi-line comments are delimited by `/*` and `*/`.
```
/* This seems counter-productive. */
let _: /* Ohhh, nevermind! */ u1 = 2; /*
    This is pretty cool.
*/
```

## Identifiers

Identifiers may be any non-interrupted string of `[a-zA-Z0-9_$]*` but it may not start with
a digit. Additionally, the `_` and `$` are reserved as temporary variables that cannot retain
their values after assignment. If an identifier requires other characters, it may be
delimited with backticks (`` ` ``).
```
let a: u1 = 1;
let hotdog: u2 = 2;
let _: u3 = 7; // Not retained.
let $_: u4 = 15;
let `hello world`: u5 = 31;
```

## Values

`<lang>` has two data-types, **integers** and **floats**. All others (booleans, strings, etc.) are derived from them.

### Integers

Integers may be any positive bit-width and signed/unsigned. Signed integers are prefixed
with an `i` followed by it's bit-width (i.e. `i32`), unsigned integers follow a similar
format, using a `u` instead (i.e. `u32`).
```
let x: i2 = 1;
let y: u10 = 123;
let z: i100 = -123456;
```

Integer literals may be in the following formats:
- Binary - Prefixed with `0b`.
- Octal - Prefixed with `0o`.
- Hexadecimal - Prefixed with `0x`.
- Decimal - No prefix.
- Scientific - Implicit.
```
let bin: u1 = 0b1;
let oct: u16 = 0xff;
let hex: u8 = 0o7;
let dec: u12 = 452;
let sci: u48 = 1e9;
```

### Floats

[TODO]

### Tuples and Arrays

Tuples are fixed-size collections of elements. Furthermore, Arrays are a subset of tuples
where all of the elements are the same type. Tuples are initialized with the elements
being separated by commas (i.e. `1, 2, 3`).
```
let tuple: [i2, u2, i3] = -1, 3, 8;
let array: [i3; 3] = 1, 1, 1;
```

## Operators

> Any operation that over/under-flows the resultant datatype, while not UB, will be
> reported as a warning unless specifically allowed via compiler hints. 

### Basic

- `+` - Adds two integers of the same bit-width and sign or two floats of the same bit-width.
```
let _: u2 = 1 + 2; // = 3
```
- `-` - Subtracts two integers of the same bit-width and sign or two floats of the same bit-width.
```
let _: i2 = 1 - 2; // = -1
```
- `*` - Multiplies two integers of the same bit-width and sign or two floats of the same bit-width.
```
let _: u3 = 2 * 2; // = 4
```
- `/` - Divides two integers of the same bit-width and sign or two floats of the same bit-width.
  - Integer division truncates the result.
```
let _: u8 = 16 / 4; // = 4
let _: u8 = 16 / 3; // = 5
```
- `%` - Returns the remained of division between two integers of the same bit-width and sign.
```
let _: u2 = 15 % 4; // = 3
```

### Bitwise

- `~` - Performs a bitwise `NOT` on an integer.
```
let _: u1 = ~1; // = 0
let _: u2 = ~0b10; // = 0b01
```
- `or` - Performs a bitwise `OR` on two integers of the same bit-width and sign.
```
let _: u2 = 0b10 or 0b01; // = 0b11
```
- `and` - Performs a bitwise `AND` on two integers of the same bit-width and sign.
```
let _: u2 = 0b10 and 0b01; // = 0
```
- `^` - Performs a bitwise `XOR` on two integers of the same bit-width and sign.
```
let _: u1 = 0b111 ^ 0b010; // = 0b101
```

### Comparison

- `>` - Greater than.
- `>=` - Greater than or equal to.
- `<` - Less than.
- `<=` - Less than or equal to.
- `==` - Equal to.

### Chaining

- `|` - Applies the value on the right side to the function on the left-side.

### Assignment

- `=` - expects an identifier on the left-hand side and binds the value of the right-hand
    side to it.

### Operator Precedence

## Keywords

`<lang>` is comprised of the following ## keywords:
- `let` - Defines a binding between a subsequent identifier and datatype.
- `import` - Includes the contents of another `<lang>` file at compilation.
- 