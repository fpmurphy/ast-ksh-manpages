# NAME

typeset - declare or display variables with attributes

# SYNOPSIS

`typeset` \[ `options` \] \[name\[=value\]...\]\

`typeset` \[ `options` \] -f \[name...\]

# DESCRIPTION

Without the `-f` option, `typeset` sets, unsets, or displays
attributes of variables as specified with the options. If the first
option is specified with a `-` then the attributes are set for each of
the given `name`s. If the first option is specified with a `+`, then
the specified attributes are unset. If `=``value` is specified value
is assigned before the attributes are set.

When `typeset` is called inside a function defined with the
`function` reserved word, and `name` does not contain a `.`, then a
local variable statically scoped to that function will be created.

Not all option combinations are possible. For example, the numeric
options `-i`, `-E`, and `-F` cannot be specified with the
justification options `-L`, `-R`, and `-Z`.

Note that the following preset aliases are set by the shell:

`compound`
: `typeset -C`.

`float`
: `typeset -lE`.

`functions`
: `typeset -f`.

`integer`
: `typeset -li`.

`nameref`
: `typeset -n`.

If no `name`s are specified then variables that have the specified
options are displayed. If the first option is specified with a leading
`-` then the name and value of each variable is written to standard
output. Otherwise, only the names are written. If no options are
specified or just `-p` is specified, then the names and attributes of
all variables that have attributes are written to standard output. When
`-f` is specified, the names displayed will be function names.

If `-f` is specified, then each `name` refers to a function and the
only valid options are `-u` and `-t`. In this case no `=``value`
can be specified.

`typeset` is built-in to the shell as a declaration command so that
field splitting and pathname expansion are not performed on the
arguments. Tilde expansion occurs on `value`.

# OPTIONS

-`a`\[`type`\]
: Indexed array. This is the default. If `\[``type``\]` is
    specified, each subscript is interpreted as a value of type `type`.
    The option value may be omitted.

-`b`
: Each `name` may contain binary data. Its value is the mime base64
    encoding of the data. It can be used with `-Z`, to specify fixed
    sized fields.

-`f`
: Each of the options and `name`s refers to a function.

-`i`\[`base`\]
: An integer. `base` represents the arithmetic base from 2 to 64. The
    option value may be omitted. The default value is `10`.

-`l`
: Convert uppercase character to lowercase. Unsets `-u` attribute.
    When used with `-i`, `-E`, or `-F` indicates long variant.

-`m`
: Move. The value is the name of a variable whose value will be moved
    to `name`. The orignal variable will be unset. Cannot be used with
    any other options.

-`n`
: Name reference. The value is the name of a variable that
    `name` references. `name` cannot contain a `.`. Cannot be use with
    any other options.

-`p`
: Causes the output to be in a format that can be used as input to the
    shell to recreate the attributes for variables.

-`r`
: Enables readonly. Once enabled it cannot be disabled. See
    [`readonly`](/web/20150816004223/http://www2.research.att.com:80/~astopen/man/man1/readonly.html)(1).

-`s`
: Used with `-i` to restrict integer size to short.

-`t`
: When used with `-f`, enables tracing for each of the
    specified functions. Otherwise, `-t` is a user defined attribute
    and has no meaning to the shell.

-`u`
: Without `-f` or `-i`, converts lowercase character to uppercase
    and unsets `-l`. With `-f` specifies that `name` is a function
    that hasn't been loaded yet. With `-i` specifies that the value
    will be displayed as an unsigned integer.

-`x`
: Puts each `name` on the export list. See
    [`export`](/web/20150816004223/http://www2.research.att.com:80/~astopen/man/man1/export.html)(1).
    `name` cannot contain a `.`.

-`A`
: Associative array. Each `name` will converted to an associate array.
    If a variable already exists, the current value will become index
    `0`.

-`C`
: Compound variable. Each `name` will be a compound variable. If
    `value` names a compound variable it will be copied to `name` .
    Otherwise if the variable already exists, it will first be unset.

-`E`\[`n`\]
: Floating point number represented in scientific notation. `n`
    specifies the number of significant figures when the value
    is expanded. The option value may be omitted. The default value is
    `10`.

-`F`\[`n`\]
: Floating point. `n` is the number of places after the decimal point
    when the value is expanded. The option value may be omitted. The
    default value is `10`.

-`H`
: Hostname mapping. Each `name` holds a native pathname. Assigning a
    UNIX format pathname will cause it to be converted to a pathname
    suitable for the current host. This has no effect when the native
    system is UNIX.

-`L`\[`n`\]
: Left justify. If `n` is given it represents the field width. If the
    `-Z` attribute is also specified, then leading zeros are stripped.
    The option value may be omitted.

-`R`\[`n`\]
: Right justify. If `n` is given it represents the field width. If the
    `-Z` attribute is also specified, then zeros will be used as the
    fill character. Otherwise, spaces are used. The option value may
    be omitted.

-`X`\[`n`\]
: Floating point number represented in hexadecimal notation. `n`
    specifies the number of significant figures when the value
    is expanded. The option value may be omitted. The default value is
    `2\`sizeof(long long)`.

-`h` `string`
: Used within a type definition to provide a help string for variable
    `name`. Otherwise, it is ignored.

-`S`
: Used with a type definition to indicate that the variable is shared
    by each instance of the type. When used inside a function defined
    with the `function` reserved word, the specified variables will
    have function static scope. Otherwise, the variable is unset prior
    to processing the assignment list.

-`T` `tname`
: `tname` is the name of a type name given to each `name`.

-`Z`\[`n`\]
: Zero fill. If `n` is given it represents the field width. The option
    value may be omitted.

# EXIT STATUS

`0`
: No errors occurred.

`&gt;0`
: An error occurred.

# SEE ALSO

[`readonly`](/web/20150816004223/http://www2.research.att.com:80/~astopen/man/man1/readonly.html)(1),
[`export`](/web/20150816004223/http://www2.research.att.com:80/~astopen/man/man1/export.html)(1)

# IMPLEMENTATION

`version`
: typeset (AT&T Research) 2008-08-04

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20150816004223/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20150816004223/http://www.opensource.org/licenses/cpl1.0.txt)


