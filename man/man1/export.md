# NAME

export - set export attribute on variables

# SYNOPSIS

`export` \[ `options` \] \[name\[=value\]...\]

# DESCRIPTION

`export` sets the export attribute on each of the variables specified
by `name` which causes them to be in the environment of subsequently
executed commands. If `=``value` is specified, the variable `name` is
set to `value`.

If no `name`s are specified then the names and values of all exported
variables are written to standard output.

`export` is built-in to the shell as a declaration command so that
field splitting and pathname expansion are not performed on the
arguments. Tilde expansion occurs on `value`.

# OPTIONS

-`p`
: Causes the output to be in the form of `export` commands that can
    be used as input to the shell to recreate the current exports.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
: An error occurred.

# SEE ALSO

[`sh`](/web/20150816234719/http://www2.research.att.com:80/~astopen/man/man1/sh.html)(1),
[`typeset`](/web/20150816234719/http://www2.research.att.com:80/~astopen/man/man1/typeset.html)(1)

# IMPLEMENTATION

`version`
: export (AT&T Research) 1999-07-07

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20150816234719/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20150816234719/http://www.opensource.org/licenses/cpl1.0.txt)


