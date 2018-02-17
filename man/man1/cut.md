# NAME

cut - cut out selected columns or fields of each line of a file

# SYNOPSIS

`cut` \[ `options` \] \[file ...\]

# DESCRIPTION

`cut` bytes, characters, or character-delimited fields from one or
more files, contatenating them on standard output.
The option argument `list` is a comma-separated or blank-separated list
of positive numbers and ranges. Ranges can be of three forms. The first
is two positive integers separated by a hyphen (`low``-``high`), which
represents all fields from `low` to `high`. The second is a positive
number preceded by a hyphen (`-``high`), which represents all fields
from field `1` to `high`. The last is a positive number followed by a
hyphen (`low``-`), which represents all fields from `low` to the last
field, inclusive. Elements in the `list` can be repeated, can overlap,
and can appear in any order. The order of the output is that of the
input.

One and only one of `-b`, `-c`, or `-f` must be specified.

If no `file` is given, or if the `file` is `-`, `cut` cuts from
standard input. The start of the file is defined as the current offset.

# OPTIONS

-`b`, --`bytes`=`list`
:   `cut` based on a list of byte counts.

-`c`, --`characters`=`list`
:   `cut` based on a list of character counts.

-`d`, --`delimiter`=`delim`
:   The field character for the `-f` option is set to `delim`. The
    default is the `tab` character.

-`f`, --`fields`=`list`
:   `cut` based on fields separated by the delimiter character
    specified with the `-d` optiion.

-`n`, --`split`
:   Split multibyte characters selected by the `-b` option. On by
    default; -`n` means --`nosplit` .

-`R|r`, --`reclen`=`reclen`
:   If `reclen` &gt; 0, the input will be read as fixed length records
    of length `reclen` when used with the `-b` or `-c` option.

-`s`, --`suppress|only-delimited`
:   Suppress lines with no delimiter characters, when used with the
    `-f` option. By default, lines with no delimiters will be passsed
    in untouched.

-`D`, --`line-delimeter|output-delimiter`=`ldelim`
:   The line delimiter character for the `-f` option is set to
    `ldelim`. The default is the `newline` character.

-`N`, --`newline`
:   Output new-lines at end of each record when used with the `-b` or
    `-c` option. On by default; -`N` means --`nonewline`.

# EXIT STATUS

`0`
: All files processed successfully.

`&gt;0`
:   One or more files failed to open or could not be read.

# SEE ALSO

[`paste`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/paste.html)(1),
[`grep`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/grep.html)(1)

# IMPLEMENTATION

`version`
:   cut (AT&T Research) 2010-08-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030242/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030242/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030242/http://www.eclipse.org/org/documents/epl-v10.html)


