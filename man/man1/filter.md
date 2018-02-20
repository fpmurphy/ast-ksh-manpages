# NAME

filter - run a command in stdin/stdout mode

# SYNOPSIS

`filter` \[ `options` \] command \[ option ... \] \[ file ... \]

# DESCRIPTION

`filter` runs `command` in a mode that takes input from the `file`
operands, or from the standard input if no `file` operands are
specified, and writes the results to the standard output. It can be used
to run commands like
[`split`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/split.html)(1),
that normally modify `file` operands in-place, in pipelines. The `file`
operands are not modified; `command` is run on copies in `/tmp`.

# SEE ALSO

[`strip`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/strip.html)(1)

# IMPLEMENTATION

`version`
:   filter (AT&T Labs Research) 2001-05-31

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1994-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030243/http://www.eclipse.org/org/documents/epl-v10.html)


