# NAME

sdiff - find differences between two files and merge interactively

# SYNOPSIS

`sdiff` \[ `options` \] from-file to-file

# DESCRIPTION

The `sdiff` command merges two files and interactively outputs the
results.
If `from-file` is a directory and `to-file` is not, `sdiff` compares
the file in `from-file` whose file name is that of `to-file`, and vice
versa. `from-file` and `to-file` may not both be directories.

`sdiff` without `--output` produces a side-by-side difference. This
usage is obsolete; use `diff --side-by-side` instead.

# OPTIONS

-`o`, --`output`=`file`
:   Output interactively, sending output to `file`. This option is
    required for merging.

-`a`, --`text|ascii`
:   Treat all files as text and compare them line-by-line, even if they
    do not appear to be text.

-`i`, --`ignore-case`
:   Consider upper- and lower-case to be the same.

-`W`, --`ignore-all-space`
:   Ignore all white space. For historical reasons this option is `-w`
    in
    [`diff`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/diff.html)(1).

-`b`, --`ignore-space-change`
:   Ignore changes in the amount of white space.

-`B`, --`ignore-blank-lines`
:   Ignore changes whose lines are all blank.

-`I`, --`ignore-matching-lines`=`pattern`
:   Ignore changes whose lines all match the regular expression
    `pattern` .

-`w`, --`width`=`columns`
:   Output at most `columns` 130) characters per line. For historical
    reasons this option is `-w` in
    [`diff`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/diff.html)(1).
    The default value is `130`.

-`l`, --`left-column`
:   Output only the left column of common lines.

-`s`, --`suppress-common-lines`
:   Do not output common lines.

-`t`, --`expand-tabs`
:   Expand tabs to spaces in output.

-`d`, --`minimal`
:   Try hard to find a smaller set of changes.

-`H`, --`speed-large-files`
:   Assume large files and many scattered small changes.

-`v`
: Print the program version and exit.

# EXIT STATUS

`0`
: No differences were found.

`1`
: Some differences were found.

`2`
: An error occurred.

# SEE ALSO

[`cmp`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/cmp.html)(1),
[`comm`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/comm.html)(1),
[`diff`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/diff.html)(1),
[`diff3`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/diff3.html)(1),
[`ed`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/ed.html)(1),
[`patch`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/patch.html)(1)

# IMPLEMENTATION

`version`
:   sdiff (GNU diffutils 2.7) 1994-10-01

`author`
:   Thomas Lord

`copyright`
:   Copyright © 1992-2012 GNU Free Software Foundation

`license`
:   [http://www.gnu.org/copyleft/gpl.html](https://web.archive.org/web/20141128030250/http://www.gnu.org/copyleft/gpl.html)


