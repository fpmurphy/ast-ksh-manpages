# NAME

what - display binary identification strings

# SYNOPSIS

`what` \[ `options` \] \[ file ... \]

# DESCRIPTION

`what` searches the given files for all occurrences of the
identification pattern `@(\#)` or `\$Id:` and writes a line to the
standard output containing the text that follows until the first
occurrence of one of the following: `" &lt; &gt; \\ \$ newline NUL`.
If no `file` is given or if a `file` is `-` then the standard
input is read. The name of each input file, followed by a `:`, is also
written as a separate line to the standard output.

# OPTIONS

-`m`, --`matched`
:   Only list the names of files that match the identification pattern.

-`s`, --`first|single`
:   Find only the first occurrence of the pattern in each file.

# EXIT STATUS

`0`
: Some matches were found.

`1`
: Otherwise.

`2`
: Option error.

# SEE ALSO

[`ident`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/ident.html)(1),
[`grep`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/grep.html)(1),
[`strings`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/strings.html)(1)

# IMPLEMENTATION

`version`
:   what (AT&T Research) 2012-02-11

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030253/http://www.eclipse.org/org/documents/epl-v10.html)


