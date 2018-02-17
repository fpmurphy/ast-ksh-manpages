# NAME

expand - convert tabs to spaces

# SYNOPSIS

`expand` \[ `options` \] \[file ...\]

# DESCRIPTION

`expand` writes the contents of each given file to standard output
with tab characters replaced with one or more space characters needed to
pad to the next tab stop. Each backspace character copied to standard
output causes the column position to be decremented by 1 unless already
in the first column.
If no `file` is given, or if the `file` is `-`, `expand` copies from
standard input. The start of the file is defined as the current offset.

# OPTIONS

-`i`, --`initial`
:   Only convert initial tabs (those that precede all non space or
    tab characters) on each line to spaces.

-`t`, --`tabs`=`tablist`
:   `tablist` is a comma or space separated list of positive integers
    that specifies the tab stops. If only one tab stop is specified,
    then tabs will be set at that many column positions apart.
    Otherwise, the value in `tablist` must be in ascending order and the
    tab stops will be set to these positions. In the event of `expand`
    having to process tab characters beyond the last specified tab stop,
    each tab character is replaced by a single tab. The default value is
    `8`.

# EXIT STATUS

`0`
: All files expanded successfully.

`&gt;0`
:   One or more files failed to open or could not be read.

# SEE ALSO

[`unexpand`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/unexpand.html)(1),
[`pr`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/pr.html)(1)

# IMPLEMENTATION

`version`
:   expand (AT&T Research) 1999-06-17

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030243/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1995-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030243/http://www.eclipse.org/org/documents/epl-v10.html)


