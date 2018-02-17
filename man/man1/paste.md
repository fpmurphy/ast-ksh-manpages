# NAME

paste - merge lines of files

# SYNOPSIS

`paste` \[ `options` \] \[file ...\]

# DESCRIPTION

`paste` concatenates the corresponding lines of a given input file and
writes the resulting lines to standard output. By default `paste`
replaces the newline character of every line other than the last input
file with the TAB character.
Unless the `-s` option is specified, if an end-of-file is encountered
on one or more input files, but not all input files, `paste` behaves
as if empty lines were read from the file(s) on which end-of-file was
detected.

Unless the `-s` option is specified, `paste` is limited by the
underlying operating system on how many `file` operands can be
specified.

If no `file` operands are given or if the `file` is `-`, `paste`
reads from standard input. The start of the file is defined as the
current offset.

# OPTIONS

-`s`, --`serial`
:   Paste the lines of one file at a time rather than one line from
    each file. In this case if the `-d` option is specified the
    delimiter will be reset to the first in the list at the beginning of
    each file.

-`d`, --`delimiters`=`list`
:   `list` specifies a list of delimiters. These delimiters are used
    circularly instead of TAB to replace the newline character of the
    input lines. Unless the `-s` option is specified, the delimiter
    will be reset to the first element of `list` each time a line is
    processed from each file. The delimiter characters corresponding to
    `list` will be found by treating `list` as an ANSI-C string, except
    that the `\\0` sequence will insert the empty string instead of
    the null character.

# EXIT STATUS

`0`
: All files processed successfully.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`cut`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/cut.html)(1),
[`cat`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/cat.html)(1),
[`join`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/join.html)(1)

# IMPLEMENTATION

`version`
:   paste (AT&T Research) 2010-06-12

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030248/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030248/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030248/http://www.eclipse.org/org/documents/epl-v10.html)


