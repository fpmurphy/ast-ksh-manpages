# NAME

rt - run "nmake test" and filter output

# SYNOPSIS

`rt` \[ `options` \] \[ test ... | - \[ file ... \] \]

# DESCRIPTION

`rt` runs `nmake test` and filters the regression test output to
contain only test summary lines. If no `test` operands are specified
then `test` is assumed. If `-` is specified then the `file`
operands, or the standard input if no `file` operands are specified, are
filtered instead of the output from `nmake`.

# OPTIONS

-`f`, --`failed`
:   Only list failed test results.

-`h`, --`heading`
:   Enable per-file heading when more than one `file` operand follows
    `-`. On by default; -`h` means --`noheading`.

-`v`, --`verbose`
:   Run with `REGRESSFLAGS=-v`.

# SEE ALSO

[`nmake`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1),
[`regress`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/regress.html)(1)

# CAVEATS

`rt` guesses the regression test output style. Garbled output
indicates a bad guess.

# IMPLEMENTATION

`version`
:   rt (AT&T Research) 2010-07-27

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 2005-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030250/http://www.eclipse.org/org/documents/epl-v10.html)


