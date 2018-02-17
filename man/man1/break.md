# NAME

break - break out of loop

# SYNOPSIS

`break` \[ `options` \] \[n\]

# DESCRIPTION

`break` is a shell special built-in that exits the smallest enclosing
`for`, `select`, `while`, or `until` loop, or the `n`-th
enclosing loop if `n` is specified. Execution continues at the command
following the loop(s).

If `n` is given, it must be a positive integer &gt;= 1. If `n` is larger
than the number of enclosing loops, the last enclosing loop will be
exited.

# EXIT STATUS

0

# SEE ALSO

[`continue`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/continue.html)(1),
[`return`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/return.html)(1)

# IMPLEMENTATION

`version`
: break (AT&T Research) 1999-04-07

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030239/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030239/http://www.opensource.org/licenses/cpl1.0.txt)


