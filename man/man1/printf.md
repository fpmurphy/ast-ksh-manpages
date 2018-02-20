# NAME

printf - write formatted output

# SYNOPSIS

`printf` \[ `options` \] format \[string ...\]

# DESCRIPTION

`printf` writes each `string` operand to standard output using
`format` to control the output format.

The `format` operands supports the full range of ANSI C formatting
specifiers plus the following additional specifiers:

`%b`
: Each character in the `string` operand is processed specially as
    follows:

    [`\\a`]()
    : Alert character.

    [`\\b`]()
    : Backspace character.

    [`\\c`]()
    : Terminate output without appending newline. The remaining
        `string` operands are ignored.

    [`\\f`]()
    : Formfeed character.

    [`\\n`]()
    : Newline character.

    [`\\t`]()
    : Tab character.

    [`\\v`]()
    : Vertical tab character.

    [`\\\\`]()
    : Backslash character.

    [`\\E`]()
    : Escape character (ASCII octal 033).

    [`\\0``x`]()
    : The 8-bit character whose ASCII code is the 1-, 2-, or 3-digit
        octal number `x`.

[`%q`]()

Output `string` quoted in a manner that it can be read in by the shell
to get back the same string. However, empty strings resulting from
missing `string` operands will not be quoted.

[`%B`]()

Treat the argument as a variable name and output the value without
converting it to a string. This is most useful for variables of type
`-b`.

[`%H`]()

Output `string` with characters `&lt;`, `&`, `&gt;`, `"`, and
non-printable characters properly escaped for use in HTML and XML
documents.

[`%P`]()

Treat `string` as an extended regular expression and convert it to a
shell pattern.

[`%R`]()

Treat `string` as an shell pattern expression and convert it to an
extended regular expression.

[`%T`]()

Treat `string` as a date/time string and format it. The `T` can be
preceded by `(``dformat``)` , where `dformat` is a date format as
defined by the `date` command.

[`%Z`]()

Output a byte whose value is `0`.

When performing conversions of `string` to satisfy a numeric format
specifier, if the first character of `string` is `"` or `'` , then
the value will be the numeric value in the underlying code set of the
character following the `"` or `'`. Otherwise, `string` is treated
like a shell arithmetic expression and evaluated.

If a `string` operand cannot be completely converted into a value
appropriate for that format specifier, an error will occur, but
remaining `string` operands will continue to be processed.

In addition to the format specifier extensions, the following extensions
of ANSI-C are permitted in format specifiers:

`-`
: The escape sequences `\\E` and `\\e` expand to the escape
    character which is octal `033` in ASCII.

`-`
: The escape sequence `\\c``x` expands to Control-`x`.

`-`
: The escape sequence `\\C\[.``name``.\]` expands to the collating
    element `name`.

`-`
: The escape sequence `\\x{``hex``}` expands to the character
    corresponding to the hexidecimal value `hex` .

`-`
: The format modifier flag `=` can be used to center a field to a
    specified width.

`-`
: The format modifier flag `L` can be used with the `c` and `s`
    formats to treat precision as character width instead of byte count.

`-`
: Each of the integral format specifiers can have a third modifier
    after width and precision that specifies the base of the conversion
    from 2 to 64. In this case the `\#` modifier will cause
    `base``\#` to be prepended to the value.

`-`
: The `\#` modifier can be used with the `d` specifier when no
    base is specified cause the output to be written in units of
    `1000` with a suffix of one of `k M G T P E`.

`-`
: The `\#` modifier can be used with the `i` specifier to cause
    the output to be written in units of `1024` with a suffix of one
    of `Ki Mi Gi Ti Pi Ei`.

If there are more `string` operands than format specifiers, the `format`
string is reprocessed from the beginning. If there are fewer `string`
operands than format specifiers, then string specifiers will be treated
as if empty strings were supplied, numeric conversions will be treated
as if 0 were supplied, and time conversions will be treated as if
`now` were supplied.

`printf` is equivalent to `print -f` which allows additional options
to be specified.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
: An error occurred.

# SEE ALSO

[`date`](/web/20150717202313/http://www2.research.att.com/~astopen/man/man1/date.html)(1),
[`print`](/web/20150717202313/http://www2.research.att.com/~astopen/man/man1/print.html)(1),
[`read`](/web/20150717202313/http://www2.research.att.com/~astopen/man/man1/read.html)(1)

# IMPLEMENTATION

`version`
: printf (AT&T Research) 2009-02-02

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20150717202313/http://www.opensource.org/licenses/cpl1.0.txt)


