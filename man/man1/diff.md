# NAME

diff - find differences between two files

# SYNOPSIS

`diff` \[ `options` \] from-file to-file

# DESCRIPTION

In the simplest case, `diff` compares the contents of the two files
`from-file` and `to-file`. A file name of `-` stands for text read
from the standard input. As a special case, `diff - -` compares a copy
of standard input to itself.
If `from-file` is a directory and `to-file` is not, `diff` compares
the file in `from-file` whose file name is that of `to-file`, and vice
versa. The non-directory file must not be `-`.

If both `from-file` and `to-file` are directories, `diff` compares
corresponding files in both directories, in alphabetical order; this
comparison is not recursive unless the `--recursive` option is given.
`diff` never compares the actual contents of a directory as if it were
a file. The file that is fully specified may not be standard input,
because standard input is nameless and the notion of \`\`file with the
same name'' does not apply.

# OPTIONS

-`B`, --`ignore-blank-lines`
:   Ignore changes that just insert or delete blank lines.

-`C`, --`context`=`lines`
:   Use the context output format, showing `lines` lines of context. For
    proper operation,
    [`patch`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/patch.html)(1)
    typically needs at least 2 lines of context. The default value is
    `3`.

-`D`, --`ifdef`=`macro`
:   Make merged `if-then-else` format output, conditional on the
    preprocessor macro `macro`.

-`F`, --`show-function-line`=`pattern`
:   In context and unified format, for each hunk of differences, show
    some of the last preceding line that matches the regular expression
    `pattern`.

-`H`, --`speed-large-files`
:   Use heuristics to speed handling of large files that have numerous
    scattered small changes.

-`I`, --`ignore-matching-lines`=`pattern`
:   Ignore changes that just insert or delete lines that match the
    regular expression `pattern`.

-`L`, --`label|file-label`=`label`
:   Use `label` instead of the file name in the context format and
    unified format headers.

-`N`, --`new-file|entire-new-file`
:   In directory comparison, if a file is found in only one directory,
    treat it as present but empty in the other directory.

-`P`, --`unidirectional-new-file`
:   When comparing directories, if a file appears only in the second
    directory of the two, treat it as present but empty in the other.

-`S`, --`starting-file`=`file`
:   When comparing directories, start with the file `file`. This is for
    resuming an interrupted comparison.

-`T`, --`initial-tab`
:   Output a tab rather than a space before the text of a line in normal
    or context format. This causes the alignment of tabs in the line to
    look normal.

-`W`, --`width`=`columns`
:   Use an output width of `columns` in side by side format.

-`a`, --`text|ascii`
:   Treat all files as text and compare them line-by-line, even if they
    do not seem to be text.

-`b`, --`ignore-space-change`
:   Ignore changes in amount of white space.

-`d`, --`minimal`
:   Change the algorithm to perhaps find a smaller set of changes. This
    makes `diff` slower (sometimes `much` slower).

-`e`, --`ed`
:   Make output that is a valid
    [`ed`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/ed.html)(1) script.

-`f`, --`forward-ed`
:   Make output that looks vaguely like an
    [`ed`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/ed.html)(1)
    script but has changes in the order they appear in the file.

-`i`, --`ignore-case`
:   Ignore changes in case; consider upper- and lower-case
    letters equivalent.

-`l`, --`paginate|print`
:   Pass the output through
    [`pr`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/pr.html)(1)
    to paginate it.

-`n`, --`rcs`
:   Output
    [`rcs`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/rcs.html)(1)
    format diffs; like `--forward-ed` except that each command
    specifies the number of lines affected.

-`p`, --`show-c-function`
:   Show which C function each change is in.

-`q`, --`brief`
:   Report only whether the files differ, not the details of
    the differences.

-`r`, --`recursive`
:   When comparing directories, recursively compare any
    subdirectories found.

-`s`, --`report-identical-files`
:   Report when two files are the same.

-`t`, --`expand-tabs`
:   Expand tabs to spaces in the output, to preserve the alignment of
    tabs in the input files.

-`w`, --`ignore-all-space`
:   Ignore white space when comparing lines.

-`x`, --`exclude`=`pattern`
:   When comparing directories, ignore files and subdirectories whose
    basenames match the
    [`sh`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
    file match `pattern`.

-`X`, --`exclude-from`=`file`
:   When comparing directories, ignore files and subdirectories whose
    basenames match any pattern contained in `file`, where each is taken
    to be one
    [`sh`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
    file match pattern.

-`y`, --`side-by-side`
:   Use the side by side output format.

-`U`, --`unified`\[=`lines`\]
:   Use the unified output format, showing `lines` lines of context. For
    proper operation
    [`patch`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/patch.html)(1)
    typically needs at least 2 lines of context. The option value may
    be omitted. The default value is `3`.

--`left-column`
:   Print only the left column of two common lines in side by
    side format.

--`suppress-common-lines`
:   Do not print common lines in side by side format.

--`sdiff-merge-assist`
:   Print extra information to help
    [`sdiff`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/sdiff.html)(1).
    Not intended for other use besides `sdiff`.

--`old-line-format`=`format`
:   Use `format` to output a line taken from just the first file in
    `if-then-else` format.

--`new-line-format`=`format`
:   Use `format` to output a line taken from just the second file in
    `if-then-else` format.

--`unchanged-line-format`=`format`
:   Use `format` to output a line common to both files in
    `if-then-else` format.

--`line-format`=`format`
:   Use `format` to output all input lines in `if-then-else` format.

--`old-group-format`=`format`
:   Use `format` to output a group of lines taken from just the first
    file in `if-then-else` format.

--`new-group-format`=`format`
:   Use `format` to output a group of lines taken from just the second
    file in `if-then-else` format.

--`unchanged-group-format`=`format`
:   Use `format` to output a group of common lines taken from both files
    in if-then-else format.

--`changed-group-format`=`format`
:   Use `format` to output a line group containing differing lines from
    both files in if-then-else format.

--`horizon-lines`=`lines`
:   Do not discard the last `lines` lines of the common prefix and the
    first `lines` lines of the common suffix.

--`binary`
:   Read and write data in binary mode. Ignored on some systems.

-`c`
: Equivalent to `--context=3`.

-`h`
: Ignored by this implementation.

-`u`
: Equivalent to `--unified=3`.

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

[`cmp`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/cmp.html)(1),
[`comm`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/comm.html)(1),
[`diff3`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/diff3.html)(1),
[`ed`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/ed.html)(1),
[`patch`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/patch.html)(1),
[`pr`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/pr.html)(1),
[`sdiff`](/web/20150527150533/http://www2.research.att.com/~astopen/man/man1/sdiff.html)(1)

# IMPLEMENTATION

`version`
:   diff (GNU diffutils 2.7) 1994-10-01

`author`
:   Paul Eggert

`author`
:   Richard Stallman

`author`
:   Mike Haertel

`author`
:   David Hayes

`author`
:   Len Tower

`copyright`
:   Copyright © 1988-2012 GNU Free Software Foundation

`license`
:   [http://www.gnu.org/copyleft/gpl.html](https://web.archive.org/web/20150527150533/http://www.gnu.org/copyleft/gpl.html)


