# NAME

exit - exit the current shell

# SYNOPSIS

`exit` \[ `options` \] \[n\]

# DESCRIPTION

`exit` is shell special built-in that causes the shell that invokes it
to exit. Before exiting the shell, if the `EXIT` trap is set it will
be invoked.

If `n` is given, it will be used to set the exit status.

# EXIT STATUS

If `n` is specified, the exit status is the least significant eight bits
of the value of `n`. Otherwise, the exit status is the exit status of
preceding command. When invoked inside a trap, the preceding command
means the command that invoked the trap.

# SEE ALSO

[`break`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/break.html)(1),
[`return`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/return.html)(1)

# IMPLEMENTATION

`version`
: exit (AT&T Research) 1999-07-07

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030243/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030243/http://www.opensource.org/licenses/cpl1.0.txt)


