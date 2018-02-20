# NAME

umask - get or set the file creation mask

# SYNOPSIS

`umask` \[ `options` \] \[mask\]

# DESCRIPTION

`umask` sets the file creation mask of the current shell execution
environment to the value specified by the `mask` operand. This mask
affects the file permission bits of subsequently created files. `mask`
can either be an octal number or a symbolic value as described in
[`chmod`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1).
If a symbolic value is given, the new file creation mask is the
complement of the result of applying `mask` to the complement of the
current file creation mask.

If `mask` is not specified, `umask` writes the value of the file
creation mask for the current process to standard output.

# OPTIONS

-`S`
: Causes the file creation mask to be written or treated as a symbolic
    value rather than an octal number.

# EXIT STATUS

`0`
: The file creation mask was successfully changed, or no `mask`
    operand was supplied.

`&gt;0`
: An error occurred.

# SEE ALSO

[`chmod`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1)

# IMPLEMENTATION

`version`
: umask (AT&T Research) 1999-04-07

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030252/http://www.opensource.org/licenses/cpl1.0.txt)


