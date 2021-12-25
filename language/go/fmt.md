### Printing verbs
- General:

    |verb|desc|
    |---|--|
    |`%v`| the value in a default format, when printing structs, the plus flag (`%+v`) adds field names|
    |`%#v`| a Go-syntax representation of the value |
    |`%T`| a Go-syntax representation of the type of the value|
    |`%%`| `%`｜
- Boolean
    |verb|desc|
    |---|--|
    |`%t`| the word `true` or `false` |
- Integer
     |verb|desc|
    |---|--|
    |`%b`| base 2 |
    |`%d`| base 10 |
    |`%o`| base 8 |
    |`%O`| base 8 with `0o` prefix
    |`%x`| base 16, lower-case letters for a-f
    |`%X`| base 16, upper-case letters for A-F
    |`%U`| Unicode format: U+1234; same as "U+%04X"
- Floating-point
    | verb| desc|
    |--|--|
    |`%e`| scientific notation, e.g. -1.23456e+78|
    |`%f`| decimal point but no exponent, e.g. 123.456|
    |`%f`|     default width, default precision
    |`%9f`|    width 9, default precision
    |`%.2f`|   default width, precision 2
    |`%9.2f`|  width 9, precision 2
    |`%9.f`|   width 9, precision 0
- String and slice of bytes
    | verb| desc|
    |`%s`| the uninterpreted bytes of string or slice
    |`%q`| a double-quoted string safely escaped with Go syntax
    |`%x`| base 16, lower-case, two characters per byte
    |`%X`| base 16, upper-case, two characters per byte
- slice
    |verb|desc|
    |--|--|
    |`%p`| address of 0th element in base16 notation, with leading 0x
- Pointer
    | verb|desc|
    |--|-|
    |`%p`| base 16 notation, with leading 0x
    |`%b`, `%d`, `%o`, `%x`| also work with pointers, formatting the value exactly as it were an integer.
- default format for `%v`

    |type|verb|
    |--|-|
    |bool|                    `%t`
    |int, int8 etc.|          `%d`
    |uint, uint8 etc.|        `%d`, `%#x` if printed with `%#v`
    |float32, complex64, etc| `%g`
    |string|                  `%s`
    |chan|                    `%p`
    |pointer|                 `%p`
    |struct|             `{field0 field1 ...}`
    |array, slice|       `[elem0 elem1 ...]`
    |maps|               `map[key1:value1 key2:value2 ...]`
    |pointer to above|   `&{}`, `&[]`, `&map[]`