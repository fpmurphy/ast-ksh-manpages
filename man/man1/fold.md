# NAME

fold - fold lines

# SYNOPSIS

`fold` \[ `options` \] \[file ...\]

# DESCRIPTION

`fold` is a filter that folds lines from its input, breaking the lines
to have a maximum of `width` column positions (or bytes if the `-b`
option is specified). Lines are broken by the insertion of a newline
character such that each output line is the maximum width possible that
does not exceed the specified number of column positions, (or bytes). A
line will not be broken in the middle of a character.
Unless the `-b` option is specified, the following will be treated
specially:

`carriage-return`
:   The current count of line width will be set to zero. `fold` will
    not insert a newline immediately before or after a carriage-return.

`backspace`
:   If positive, the current count of line width will be decremented
    by one. `fold` will not insert a newline immediately before or
    after a backspace.

`tab`
: Each tab character encountered will advance the column position to
    the next tab stop. Tab stops are at each column position `n`, where
    `n` modulo 8 equals 1.

If no `file` is given, or if the `file` is `-`, `fold` reads from
standard input. The start of the file is defined as the current offset.

# OPTIONS

-`b`, --`bytes`
:   Count bytes rather than columns so that each carriage-return,
    backspace, and tab counts as 1.

-`c`, --`continue`=`text`
:   Emit `text` at line splits. The default value is `'\\n'`.

-`d`, --`delimiter`=`delim`
:   Break at `delim` boundaries.

-`s`, --`spaces`
:   Break at word boundaries. If the line contains any blanks, (spaces
    or tabs), within the first `width` column positions or bytes, the
    line is broken after the last blank meeting the `width` constraint.

-`w`, --`width`=`width`
:   Use a maximum line length of `width` columns instead of the default.
    The default value is `80`.

# EXIT STATUS

`0`
: All files processed successfully.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`paste`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/paste.html)(1)

# IMPLEMENTATION

`version`
:   fold (AT&T Research) 2004-11-18

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030244/http://www.eclipse.org/org/documents/epl-v10.html)


