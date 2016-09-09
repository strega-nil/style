# Rust Style Guide

## Formatting Conventions

These formatting conventions are a work in progress, and may do anything they
like, up to and including eating your laundry.

### Function Definitions

In Rust, one finds functions by searching for `fn [function-name]`; It's
important that you style your code so that it's very searchable in this way.
The proper format, therefore, is:

```rust
[pub] [unsafe] [extern ["ABI"]] fn foo(arg1: i32, arg2: i32) -> i32 {
    ...
}
```

### Function Body

Prefer to use Rust's expression oriented nature where possible;

```rust
// use
let x = if y { 1 } else { 0 };
// not
let x;
if y {
    x = 1;
} else {
    x = 0;
}
```

### Closures

Don't put any extra spaces before the first `|`, but put a space between the
second `|` and the expression of the closure. Between the `|`s, you should use
function definition syntax, except excluding the types.

Use closures without the enclosing `{}`, if possible. Add the `{}` when you
have a return type, when there are statements before the final expression, or
when you need to split it into multiple lines.

Generally, don't use type hints for the parameter list; however, you may if
necessary.

### Indenting

Tabs *shall not* be used.

### Names

 * Types shall be `PascalCase`
 * Enum variants shall be `PascalCase`
 * Struct members shall be `snake_case`
 * Function and method names shall be `snake_case`
 * Local variables shall be `snake_case`
 * Macro names shall be `snake_case`
 * Constants shall be `SCREAMING_SNAKE_CASE`

### Expressions

DO NOT include a space between a unary op and its operand (i.e., `!x`, not
`! x`).

DO include spaces around binary ops (i.e., `x + 1`, not `x+1`) (note: this
includes `=`)

For comparison operators, because for `T op U`, `&T op &U` is also implemented:
if you have `t: &T`, and `u: U`, prefer `*t op u` to `t op &u`. In general,
within expressions, prefer dereferencing to taking references.

DO NOT include extraneous parentheses for `if` and `while` expressions.

```rust
// NO
if (true) {
}
```

DO include extraneous parentheses if it makes an arithmetic expression easier
to understand (`(x * 15) + (y * 20)` is fine)

### Function Calls

DO NOT put a space between the function name, and the open paren.

DO NOT put a space between an argument, and the comma which follows.

DO put a space between an argument, and the comma which precedes it.

#### Single-line Calls

DO NOT put a space between the parens, and the first and last arguments.

DO NOT put a comma after the last argument.

```rust
foo(x, y, z)
```

### Methods

Follow the function rules for calling.

#### Single-line

DO NOT put any spaces around the `.`.

```rust
x.foo().bar().baz();
```

### as

The same rules for methods, follow for `as`, except that you must put spaces
around it.

```rust
let cstr = "Hi\0" as *const str as *const [u8] as *const std::os::raw::c_char;
```

### Tuple structs

Write the type list as you would a parameter list to a function.

Build a tuple or tuple struct as you would call a function.

#### Single-line

```rust
struct Bar(Type1, Type2);
```

### Enums

DO put each variant on it's own line.

DO format each variant accordingly as either a `struct`, `tuple struct`, or
just simply as an ident, which doesn't require special formatting.

```rust
enum FooBar {
    First(u32),
    Second,
    Error {
        err: Box<Error>,
        line: u32,
    },
}
```

Build an enum as you would a namespaced struct, tuple struct, or constant.

### macro\_rules!

Use `{}` for the full definition of the macro.

DO NOT use spaces around the `:`.

### String literals

Raw string literals should be used for things like code blocks. There is no
style guide at all for the insides of raw string literals; they are translated
literally, so whatever you need to make the raw string literal correct.

### Doc comments

Only use inner doc comments (`//!` and `/*!`) to write module level
documentation.

### Attributes

Put each attribute on it's own line, indented to the indentation of its item.
In the case of inner attributes (`#!`), indent it to the inner indentation (the
indentation of the item + 1).

```rust
#[repr(C)]
struct CRepr {
    x: f32,
    y: f32,
}
```

### Extern

`extern crate foo;`

There's no other real recommendations about this. You may prefer alphabetical
order.

Almost always, put your `extern crates` at top level (in `main.rs` or
`lib.rs`).

### Modules

`mod foo {`

`mod foo;`

Files for modules may either be in `./foo.rs` if there are no submodules that
require files, or `./foo/mod.rs` if there are. Do not use `#[path]` annotations.
