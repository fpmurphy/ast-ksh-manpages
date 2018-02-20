# NAME

continue - continue execution at top of the loop

# SYNOPSIS

`continue` \[ `options` \] \[n\]

# DESCRIPTION

`continue` is a shell special built-in that continues execution at the
top of smallest enclosing enclosing `for`, `select`, `while` , or
`until` loop, if any; or the top of the `n`-th enclosing loop if `n`
is specified.

If `n` is given, it must be a positive integer &gt;= 1. If `n` is larger
than the number of enclosing loops, the last enclosing loop will be
used.

# SEE ALSO

[`break`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/break.html)(1)

# IMPLEMENTATION

`version`
: continue (AT&T Research) 1999-04-07

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030240/http://www.opensource.org/licenses/cpl1.0.txt)


