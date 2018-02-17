# NAME

comm - select or reject lines common to two files

# SYNOPSIS

`comm` \[ `options` \] file1 file2

# DESCRIPTION

`comm` reads two files `file1` and `file2` which should be ordered in
the collating sequence of the current locale, and produces three text
columns as output:

`1`
: Lines only in `file1`.

`2`
: Lines only in `file2`.

`3`
: Lines in both files.

If lines in either file are not ordered according to the collating
sequence of the current locale, the results are not specified.
If either `file1` or `file2` is `-`, `comm` uses standard input
starting at the current location.

# OPTIONS

-`1`
: Suppress the output column of lines unique to `file1`.

-`2`
: Suppress the output column of lines unique to `file2`.

-`3`
: Suppress the output column of lines duplicate in `file1` and
    `file2`.

# EXIT STATUS

`0`
: Both files processed successfully.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`cmp`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/cmp.html)(1),
[`diff`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/diff.html)(1)

# IMPLEMENTATION

`version`
:   comm (AT&T Research) 1999-04-28

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030240/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030240/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030240/http://www.eclipse.org/org/documents/epl-v10.html)


