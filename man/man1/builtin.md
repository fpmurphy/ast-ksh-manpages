# NAME

builtin - add, delete, or display shell built-ins

# SYNOPSIS

`builtin` \[ `options` \] \[pathname ...\]

# DESCRIPTION

`builtin` can be used to add, delete, or display built-in commands in
the current shell environment. A built-in command executes in the
current shell process and can have side effects in the current shell. On
most systems, the invocation time for built-in commands is one or two
orders of magnitude less than commands that create a separate process.

For each `pathname` specified, the basename of the pathname determines
the name of the built-in. For each basename, the shell looks for a C
level function in the current shell whose name is determined by
prepending `b\_` to the built-in name. If `pathname` contains a `/`,
then the built-in is bound to this pathname. A built-in bound to a
pathname will only be executed if `pathname` is the first executable
found during a path search. Otherwise, built-ins are found prior to
performing the path search.

If no `pathname` operands are specified, then `builtin` displays the
current list of built-ins, or just the special built-ins if `-s` is
specified, on standard output. The full pathname for built-ins that are
bound to pathnames are displayed.

Libraries containing built-ins can be specified with the `-f` option.
If the library contains a function named `lib\_init`(), this function
will be invoked with argument `0` when the library is loaded. The
`lib\_init`() function can load built-ins by invoking an appropriate C
level function. In this case there is no restriction on the C level
function name.

The C level function will be invoked with three arguments. The first two
are the same as `main`() and the third one is a pointer.

`builtin` cannot be invoked from a restricted shell.

# OPTIONS

-`d`
: Deletes each of the specified built-ins. Special built-ins cannot
    be deleted.

-`f` `lib`
: On systems with dynamic linking, `lib` names a shared library to
    load and search for built-ins. Libraries are search for in
    `\$PATH` and system dependent library directories. The system
    dependent shared library prefix and/or suffix may be omitted. Once a
    library is loaded, its symbols become available for the current and
    subsequent invocations of `builtin`. Multiple libraries can be
    specified with separate invocations of `builtin`. Libraries are
    searched in the reverse order in which they are specified.

-`s`
: Display only the special built-ins.

# EXIT STATUS

`0`
: All `pathname` operands and `-f` options processed successfully.

`&gt;0`
: An error occurred.

# SEE ALSO

[`whence`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/whence.html)(1)

# IMPLEMENTATION

`version`
: builtin (AT&T Research) 1999-07-10

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030239/http://www.opensource.org/licenses/cpl1.0.txt)


