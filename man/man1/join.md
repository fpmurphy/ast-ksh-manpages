# NAME

join - relational database operator

# SYNOPSIS

`join` \[ `options` \] file1 file2

# DESCRIPTION

`join` performs an `equality join` on the files `file1` and `file2`
and writes the resulting joined files to standard output. By default, a
field is delimited by one or more spaces and tabs with leading spaces
and/or tabs ignored. The `-t` option can be used to change the field
delimiter.
The `join field` is a field in each file on which files are compared. By
default `join` writes one line in the output for each pair of lines in
`files1` and `files2` that have identical join fields. The default
output line consists of the join field, then the remaining fields from
`file1`, then the remaining fields from `file2`, but this can be changed
with the `-o` option. The `-a` option can be used to add unmatched
lines to the output. The `-v` option can be used to output only
unmatched lines.

The files `file1` and `file2` must be ordered in the collating sequence
of `sort -b` on the fields on which they are to be joined otherwise
the results are unspecified.

If either `file1` or `file2` is `-`, `join` uses standard input
starting at the current location.

# OPTIONS

-`e`, --`empty`=`string`
\
Replace empty output fields in the list selected with `-o` with
`string`.
-`o`, --`output`=`list`
\
Construct the output line to comprise the fields specified in a blank or
comma separated list `list`. Each element in `list` consists of a file
number (either 1 or 2), a period, and a field number or `0`
representing the join field. As an obsolete feature multiple occurrences
of `-o` can be specified.
-`t`, --`separator|tabs`=`delim`
\
Use `delim` as the field separator for both input and output.
-`1`, --`j1`=`field`
\
Join on field `field` of `file1`. Fields start at 1.
-`2`, --`j2`=`field`
\
Join on field `field` of `file2`. Fields start at 1.
-`j`, --`join`=`field`
\
Equivalent to `-1` `field` `-2` `field`.
-`a`, --`unpairable`=`fileno`
\
Write a line for each unpairable line in file `fileno`, where `fileno`
is either 1 or 2, in addition to the normal output. If `-a` options
appear for both 1 and 2, then all unpairable lines will be output.
-`v`, --`suppress`=`fileno`
\
Write a line for each unpairable line in file `fileno`, where `fileno`
is either 1 or 2, instead of the normal output. If `-v` options appear
for both 1 and 2, then all unpairable lines will be output.
-`i`, --`ignorecase`
\
Ignore case in field comparisons.
-`B`, --`mmap`
\
Enable memory mapped reads instead of buffered. On by default; -`B`
means --`nommap`.
The following obsolete option forms are also recognized: `-j` `field`
is equivalent to `-1` `field` `-2` `field`, `-j1` `field` is
equivalent to `-1` `field`, and `-j2` `field` is equivalent to
`-2` `field`.

# EXIT STATUS

`0`
: Both files processed successfully.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`cut`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/cut.html)(1),
[`comm`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/comm.html)(1),
[`paste`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/paste.html)(1),
[`sort`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/sort.html)(1),
[`uniq`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/uniq.html)(1)

# IMPLEMENTATION

`version`
:   join (AT&T Research) 2009-12-10

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030245/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030245/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030245/http://www.eclipse.org/org/documents/epl-v10.html)


