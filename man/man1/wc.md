# NAME

wc - print the number of bytes, words, and lines in files

# SYNOPSIS

`wc` \[ `options` \] \[file ...\]

# DESCRIPTION

`wc` reads one or more input files and, by default, for each file
writes a line containing the number of newlines, `word`s, and bytes
contained in each file followed by the file name to standard output in
that order. A `word` is defined to be a non-zero length string delimited
by
[`isspace`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/isspace.html)(3)
characters.
If more than one file is specified, `wc` writes a total count for all
of the named files with `total` written instead of the file name.

By default, `wc` writes all three counts. Options can specified so
that only certain counts are written. The options `-c` and `-m` are
mutually exclusive.

If no `file` is given, or if the `file` is `-`, `wc` reads from
standard input and no filename is written to standard output. The start
of the file is defined as the current offset.

# OPTIONS

-`l`, --`lines`
:   List the line counts.

-`w`, --`words`
:   List the word counts.

-`c`, --`bytes|chars`
:   List the byte counts.

-`m|C`, --`multibyte-chars`
:   List the character counts.

-`q`, --`quiet`
:   Suppress invalid multibyte character warnings.

-`L`, --`longest-line|max-line-length`
:   List the longest line length; the newline,if any, is not counted in
    the length.

-`N`, --`utf8`
:   For `UTF-8` locales `--noutf8` disables `UTF-8` optimzations
    and relies on the native
    [`mbtowc`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/mbtowc.html)(3).
    On by default; -`N` means --`noutf8`.

# EXIT STATUS

`0`
: All files processed successfully.

`&gt;0`
:   One or more files failed to open or could not be read.

# SEE ALSO

[`cat`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/cat.html)(1),
[`isspace`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/isspace.html)(3)

# IMPLEMENTATION

`version`
:   wc (AT&T Research) 2009-11-28

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030253/http://www.eclipse.org/org/documents/epl-v10.html)


