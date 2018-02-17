# NAME

unexpand - convert spaces to tabs

# SYNOPSIS

`unexpand` \[ `options` \] \[file ...\]

# DESCRIPTION

`unexpand` writes the contents of each given file to standard output
with strings of two or more space and tab characters at the beginning of
each line converted to as many tabs as possible followed by as many
spaces needed to fill the same number of column positions. By default,
tabs are set at every 8th column. Each backspace character copied to
standard output causes the column position to be decremented by 1 unless
already in the first column.
If no `file` is given, or if the `file` is `-`, `unexpand` copies
from standard input. The start of the file is defined as the current
offset.

# OPTIONS

-`a`, --`all`
:   Convert all strings of two or more spaces or tabs, not just
    initial ones.

-`t`, --`tabs`=`tablist`
:   `tablist` is a comma or space separated list of positive integers
    that specifies the tab stops. If only one tab stop is specified,
    then tabs will be set at that many column positions apart.
    Otherwise, the value in `tablist` must be in ascending order and the
    tab stops will be set to these positions. This option implies the
    `-a` option. The default value is `8`.

# EXIT STATUS

`0`
: All files unexpanded successfully.

`&gt;0`
:   One or more files failed to open or could not be read.

# SEE ALSO

[`expand`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/expand.html)(1),
[`pr`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/pr.html)(1)

# IMPLEMENTATION

`version`
:   unexpand (AT&T Research) 1999-06-07

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030252/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1995-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030252/http://www.eclipse.org/org/documents/epl-v10.html)


