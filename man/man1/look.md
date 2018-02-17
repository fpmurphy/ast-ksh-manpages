# NAME

look - displays lines beginning with a given prefix

# SYNOPSIS

`look` \[ `options` \] prefix \[- max-prefix\] \[file ...\]

# DESCRIPTION

`look` displays all lines in the sorted `file` arguments that begin
with the given prefix `prefix` onto the standard output. The results are
unspecified if any `file` is not sorted. If `max-prefix` is specified
then then records matching prefixes in the inclusive range
`prefix`..`max-prefix` are displayed.
If `file` is not specified, `look` uses the file `/usr/dict/words`
and enables `--dictionary` and `--ignorecase` .

# OPTIONS

-`d`, --`dictionary`
:   \`Phone dictionary order': only letters, digits, and white space
    characters are significant in string comparisons.

-`f`, --`fold|ignorecase`
:   The search is case insensitive.

-`h`, --`header`
:   Skip flat file header (all lines up to first blank line.)

# EXIT STATUS

`0`
: The specified `prefix` was found in the file.

`1`
: The specified `prefix` was not found in the file.

`&gt;1`
:   An error occurred.

# SEE ALSO

[`grep`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/grep.html)(1),
[`sort`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/sort.html)(1)

# IMPLEMENTATION

`version`
:   look (AT&T Research) 2008-02-14

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030246/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030246/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030246/http://www.eclipse.org/org/documents/epl-v10.html)


