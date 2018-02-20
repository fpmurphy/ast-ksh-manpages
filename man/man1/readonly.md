# NAME

readonly - set readonly attribute on variables

# SYNOPSIS

`readonly` \[ `options` \] \[name\[=value\]...\]

# DESCRIPTION

`readonly` sets the readonly attribute on each of the variables
specified by `name` which prevents their values from being changed. If
`=``value` is specified, the variable `name` is set to `value` before
the variable is made readonly.

Within a type definition, if the value is not specified, then a value
must be specified when creating each instance of the type and the value
is readonly for each instance.

If no `name`s are specified then the names and values of all readonly
variables are written to standard output.

`readonly` is built-in to the shell as a declaration command so that
field splitting and pathname expansion are not performed on the
arguments. Tilde expansion occurs on `value`.

# OPTIONS

-`p`
: Causes the output to be in a form of `readonly` commands that can
    be used as input to the shell to recreate the current set of
    readonly variables.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
: An error occurred.

# SEE ALSO

[`sh`](/web/20150816234724/http://www2.research.att.com:80/~astopen/man/man1/sh.html)(1),
[`typeset`](/web/20150816234724/http://www2.research.att.com:80/~astopen/man/man1/typeset.html)(1)

# IMPLEMENTATION

`version`
: readonly (AT&T Research) 2008-06-16

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20150816234724/http://www.opensource.org/licenses/cpl1.0.txt)


