## Object Description Language Specificaton Version 1
This version is being written as of Friday 2024 April 24 18:12 UTC+3

This is the first and main specification of ODL. This documentation contains
every aspect and detail of how ODL works.

## 1. Introduction
ODL is a minimal but advanced, human-readable configuration and object
description language designed for structured data. It focused on simplicity,
using tables and arrays as the primary organization unit. It supports macros
and several procedure-like operations like null-coalescing.

## 2. Basic Syntax
Below is an example document you can inspect.
```odl
# my package definition or something idk
mypkg {
    name        = 'ODL'
    description = 'a configuration and object description language.'
    source      = 'git:github.com/glassthorn/odl-spec'

    version       = APPV ? 'github-release'
    versionString = '{{ name }}, Build {{ version }}'

    PI = 3.1415

    isItDryRun = true
    extraBuildStuff = nil # you can use null too btw
}
```

### 2.1 Comments
Comments can be added using multiple syntaxes like this:
```
# one line
// one line
#*
    multi line
*#
/*
    multi line
*/
```

### 2.2 Assignments
A key-value pair is assigned using `=`, `is`, or `as`. All three are
functionally identical tokens to allow for expressive flexibility.
```odl
table1 {
    myVar1 =   1.3
    myVar2 is 'hii :3'
    myVar3 as true
}
```

## 3. Data types
| Type    | Example                   | Description                                                |
|---------|---------------------------|------------------------------------------------------------|
| String  | `'hello'`, `"hi"`         | Supported in both double and single quotes.                |
| Number  | `10`, `-23`, `1.3`, `6e2` | All numbers, even floating-point and scientific notations. |
| Boolean | `true`, `false`           | Case-sensitive logical values.                             |
| Null    | `null`, `nil`             | Represents an empty or non-existent value.                 |
| Array   | `(1, 2.3, '4', nil)`      | Space-separated list enclosed in parentheses.              |

## 4. Expressions and logic
### 4.1 Variable Interpolation
Values can reference previously defined keys using the `{{identifier}}` syntax.
```odl
...
lorem2 = 'ipsum'
blabla = 'lorem {{ lorem2 }} dolor sit amet'
...
```

### 4.2 Null-Coalescing
The `?` operator provides a fallback if the first operand is `null` or `nil`.
```odl
test1  = nil
test2  = null
test3  = 'Hello World'
output = test1 ? test2 ? test3
# output is 'Hello World'
```

### 4.3 Macros
Macros are triggered by the `@` symbol. They can be atomic (single line) or
block-based.
- Atomic Macro: `@macroName ...args`
- Block Macro: Starts with `@macroName` and must be terminated with `@end`.

```odl
table1 {
    # This is an atomic macro
    @doSomething

    # This is a block macro
    @ifdef something
    something = nil
    @end
}
```

# License
Check the license at [./LICENSE](./LICENSE)