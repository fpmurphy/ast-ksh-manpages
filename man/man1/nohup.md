# NAME

whence - locate a command and describe its type

# SYNOPSIS

`whence` \[ `options` \] name ...

# DESCRIPTION

Without `-v`, `whence` writes on standard output an absolute
pathname, if any, corresponding to `name` based on the complete search
order that the shell uses. If `name` is not found, then no output is
produced.

If `-v` is specified, the output will also contain information that
indicates how the given `name` would be interpreted by the shell in the
current execution environment.

# OPTIONS

-`a`

Displays all uses for each `name` rather than the first.

-`f`

Do not check for functions.

-`p`

Do not check to see if `name` is a reserved word, a built-in, an alias,
or a function. This turns off the `-v` option.

-`q`

Quiet mode. Returns 0 if all arguments are built-ins, functions, or are
programs found on the path.

-`v`

For each name you specify, the shell displays a line that indicates if
that name is one of the following:

Reserved word

Alias

Built-in

Undefined function

Function

Tracked alias

Program

# EXIT STATUS

`0`
: Each `name` was found by the shell.

`1`
: One or more `name`s were not found by the shell.

`&gt;1`
: An error occurred.

# SEE ALSO

[`command`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/command.html)(1)

# IMPLEMENTATION

`version`
: whence (AT&T Research) 2007-04-24

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030247/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030247/http://www.opensource.org/licenses/cpl1.0.txt)

nohup: line 23: --html: not found
