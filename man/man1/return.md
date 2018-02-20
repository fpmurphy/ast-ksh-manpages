# NAME

return - return from a function or dot script

# SYNOPSIS

`return` \[ `options` \] \[n\]

# DESCRIPTION

`return` is a shell special built-in that causes the function or dot
script that invokes it to exit. If `return` is invoked outside of a
function or dot script it is equivalent to `exit`.

If `return` is invoked inside a function defined with the `function`
reserved word syntax, then any `EXIT` trap set within the then
function will be invoked in the context of the caller before the
function returns.

If `n` is given, it will be used to set the exit status.

# EXIT STATUS

If `n` is specified, the exit status is the least significant eight bits
of the value of `n`. Otherwise, the exit status is the exit status of
preceding command.

# SEE ALSO

[`break`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/break.html)(1),
[`exit`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/exit.html)(1)

# IMPLEMENTATION

`version`
: return (AT&T Research) 1999-07-07

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030249/http://www.opensource.org/licenses/cpl1.0.txt)


