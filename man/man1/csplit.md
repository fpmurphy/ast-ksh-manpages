# NAME

csplit - split a file into sections determined by context lines

# SYNOPSIS

`csplit` \[ `options` \] file arg ...

# DESCRIPTION

`csplit` creates zero or more output files containing sections of the
given input `file`, or the standard input if the name `-` is given. By
default, `csplit` prints the number of bytes written to each output
file after it has been created.
The contents of the output files are determined by the `pattern`
arguments. An error occurs if a pattern argument refers to a nonexistent
line of the input file, such as if no remaining line matches a given
regular expression. After all the given patterns have been matched, any
remaining output is copied into one last output file. The types of
pattern arguments are:

`line`
: Create an output file containing the current line up to (but
    not including) line `line` (a positive integer) of the input file.
    If followed by a repeat count, also create an output file containing
    the next `line` lines of the input file once for each repeat.

`/regexp/\[offset\]`
:   Create an output file containing the current line up to (but
    not including) the next line of the input file that contains a match
    for `regexp`. The optional `offset` is a `+` or `-` followed by
    a positive integer. If it is given, the input up to the matching
    line plus or minus `offset` is put into the output file, and the
    line after that begins the next section of input.

`%regexp%\[offset\]`
:   Like the previous type, except that it does not create an output
    file, so that section of the input file is effectively ignored.

`{repeat-count}`
:   Repeat the previous pattern `repeat-count` (a positive integer)
    additional times. An asterisk may be given in place of the (integer)
    repeat count, in which case the preceeding pattern is repeated as
    many times as necessary until the input is exausted.

The output file names consist of a prefix followed by a suffix. By
default, the suffix is merely an ascending linear sequence of two-digit
decimal numbers starting with 00 and ranging up to 99, however this
default may be overridden by either the `--digits` option or by the
`--suffix-format` option (see below.) In any case, concatenating the
output files in sorted order by file name produces the original input
file, in order. The default output file name prefix is `xx`.
By default, if `csplit` encounters an error or receives a hangup,
interrupt, quit, or terminate signal, it removes any output files that
it has created so far before it exits.

# OPTIONS

-`b`, --`suffix-format`=`format`
:   Use the
    [`printf`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
    `format` to generate the file name suffix. The default value is
    ``%02d``.

-`f`, --`prefix`=`prefix`
:   Use `prefix` to generate the file name prefix. The default value is
    ``xx ``.

-`k`, --`keep-files`
:   Do not remove output files on errors.

-`a|n`, --`digits`=`digits`
:   Use `digits` in the generated file name suffixes. The default value
    is `2` .

-`s`, --`silent|quiet`
:   Do not print output file counts and sizes.

-`z`, --`elide-empty-files`
:   Remove empty output files.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`split`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/split.html)(1),
[`cat`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/cat.html)(1)

# IMPLEMENTATION

`version`
:   csplit (AT&T Research) 2003-08-21

`author`
:   David Korn

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1995-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030242/http://www.eclipse.org/org/documents/epl-v10.html)


