# NAME

print - write arguments to standard output

# SYNOPSIS

`print` \[ `options` \] \[string ...\]

# DESCRIPTION

By default, `print` writes each `string` operand to standard output
and appends a newline character.

Unless, the `-r` or `-f` option is specified, each `\\` character
in each `string` operand is processed specially as follows:

`\\a`
: Alert character.

`\\b`
: Backspace character.

`\\c`
: Terminate output without appending newline. The remaining `string`
    operands are ignored.

`\\f`
: Formfeed character.

`\\n`
: Newline character.

`\\t`
: Tab character.

`\\v`
: Vertical tab character.

`\\\\`
: Backslash character.

`\\E`
: Escape character (ASCII octal 033).

`\\0``x`
: The 8-bit character whose ASCII code is the 1-, 2-, or 3-digit octal
    number `x`.

If both `-e` and `-r` are specified, the last one specified is the
one that is used.

When the `-f` option is specified and there are more `string` operands
than format specifiers, the format string is reprocessed from the
beginning. If there are fewer `string` operands than format specifiers,
then outputting will end at the first unneeded format specifier.

# OPTIONS

-`e`
: Unless `-f` is specified, process `\\` sequences in each
    `string` operand as described above. This is the default behavior.

-`n`
: Do not append a new-line character to the output.

-`f` `format`
: Write the `string` arguments using the format string `format` and do
    not append a new-line. See `printf` for details on how to specify
    `format`.

-`p`
: Write to the current co-process instead of standard output.

-`r`
: Do not process `\\` sequences in each `string` operand as
    described above.

-`s`
: Write the output as an entry in the shell history file instead of
    standard output.

-`u` `fd`
: Write to file descriptor number `fd` instead of standard output. The
    default value is `1`.

-`v`
: Treat each `string` as a variable name and write the value in
    `%B` format. Cannot be used with `-f`.

-`C`
: Treat each `string` as a variable name and write the value in
    `%\#B` format. Cannot be used with `-f`.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
: An error occurred.

# SEE ALSO

[`echo`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/echo.html)(1),
[`printf`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/printf.html)(1),
[`read`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/read.html)(1)

# IMPLEMENTATION

`version`
: print (AT&T Research) 2008-11-26

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030248/http://www.opensource.org/licenses/cpl1.0.txt)


