# NAME

let - evaluate arithmetic expressions

# SYNOPSIS

`let` \[ `options` \] \[expr ...\]

# DESCRIPTION

`let` evaluates each `expr` in the current shell environment as an
arithmetic expression using ANSI C syntax. Variables names are shell
variables and they are recursively evaluated as arithmetic expressions
to get numerical values.

`let` has been made obsolete by the `((`...`))` syntax of
[`ksh`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
which does not require quoting of the operators to pass them as command
arguments.

# EXIT STATUS

`0`
: The last `expr` evaluates to a non-zero value.

`&gt;0`
: The last `expr` evaluates to `0` or an error occurred.

# SEE ALSO

[`expr`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/expr.html)(1),
[`test`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/test.html)(1),
[`ksh`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)

# IMPLEMENTATION

`version`
: let (AT&T Research) 2000-04-02

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030245/http://www.opensource.org/licenses/cpl1.0.txt)


