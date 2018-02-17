# NAME

unset - unset values and attributes of variables and functions

# SYNOPSIS

`unset` \[ `options` \] name...

# DESCRIPTION

For each `name` specified, `unset` unsets the variable, or function if
`-f` is specified, from the current shell execution environment.
Readonly variables cannot be unset.

# OPTIONS

-`n`
: If `name` refers to variable that is a reference, the variable
    `name` will be unset rather than the variable it references.
    Otherwise, is is equivalent to `-v`.

-`f`
: `name` refers to a function name and the shell will unset the
    function definition.

-`v`
: `name` refers to a variable name and the shell will unset it and
    remove it from the environment. This is the default behavior.

# EXIT STATUS

`0`
: All `name`s were successfully unset.

`&gt;0`
: One or more `name` operands could not be unset or an error occurred.

# SEE ALSO

[`typeset`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/typeset.html)(1)

# IMPLEMENTATION

`version`
: unset (AT&T Research) 1999-07-07

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030253/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030253/http://www.opensource.org/licenses/cpl1.0.txt)


