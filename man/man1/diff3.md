# NAME

diff3 - find differences between three files

# SYNOPSIS

`diff3` \[ `options` \] mine older yours

# DESCRIPTION

The `diff3` command compares three files and outputs descriptions of
their differences.
The files to compare are `mine`, `older`, and `yours`. At most one of
these three file names may be `-`, corresponding to the standard
input.

# OPTIONS

-`a`, --`text|ascii`
:   Treat all files as text and compare them line-by-line, even if they
    do not appear to be text.

-`A`, --`show-all`
:   Incorporate all unmerged changes from `older` to `yours` into
    `mine`, surrounding all overlapping changes with bracket lines.

-`e`, --`ed`
:   Generate an
    [`ed`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/ed.html)(1)
    script that incorporates all the changes from `older` to `yours`
    into `mine`.

-`E`, --`show-overlap`
:   Like `--ed`, except that overlapping changes are bracketed.

-`L`, --`label`=`label`
:   Use `label` instead of the file name.

-`m`, --`merge`
:   Apply the edit script to the first file and send the result to the
    standard output. Unlike piping the output from `diff3` to `ed`,
    this works even for binary files and incomplete lines.
    `--show-all` is assumed if no edit script option is specified.

-`T`, --`initial-tab`
:   Make tabs line up by prepending a tab to the output.

-`x`, --`overlap-only`
:   Like `--ed`, except output only the overlapping changes.

-`3`, --`easy-only`
:   Like `--ed`, except output only the nonoverlapping changes.

-`i`, --`compatibility`
:   Generate `w` and `q` commands at the end of the
    [`ed`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/ed.html)(1)
    script for System V compatibility.

-`v`
: Print the program version and exit.

# EXIT STATUS

`0`
: Success.

`1`
: Some conflicts were found.

`2`
: An error occurred.

# SEE ALSO

[`cmp`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/cmp.html)(1),
[`comm`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/comm.html)(1),
[`diff`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/diff.html)(1),
[`ed`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/ed.html)(1),
[`patch`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/patch.html)(1),
[`sdiff`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/sdiff.html)(1)

# IMPLEMENTATION

`version`
:   diff3 (GNU diffutils 2.7) 1994-10-01

`author`
:   Randy Smith

`copyright`
:   Copyright © 1988-2012 GNU Free Software Foundation

`license`
:   [http://www.gnu.org/copyleft/gpl.html](https://web.archive.org/web/20141128030242/http://www.gnu.org/copyleft/gpl.html)


