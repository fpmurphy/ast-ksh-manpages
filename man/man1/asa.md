# NAME

asa - interpret carriage-control characters

# SYNOPSIS

`asa` \[ `options` \] \[file ... \]

# DESCRIPTION

`asa` writes its input files to standard output mapping carriage
control characters to line-printer control sequences.
The first character of each line or record is removed from the input and
is processed as follows before the rest of the line is output:

`0`
: A new-line is output.

`1`
: Advance to the next page.

`+`
: Overwrite the previous line.

`space`
:   Just output the remainder of the line.

Any other character as the first character is treated as if it were a
space.
If no `file` operands are given or if the `file` is `-`, `asa` reads
from standard input. The start of the file is defined as the current
offset.

# OPTIONS

-`r` `reclen`
:   If `reclen` is greater than zero, the file is assumed to consist of
    fixed length records of length `reclen`.

# EXIT STATUS

`0`
: Success.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`lpr`](/web/20141128030238/http://www2.research.att.com/~astopen/man/man1/lpr.html)(1)

# IMPLEMENTATION

`version`
:   asa (AT&T Research) 2003-03-25

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030238/mailto:dgkorn@gmail.com)&gt;

`license`
:   [http://www.research.att.com/sw/tools/reuse](https://web.archive.org/web/20141128030238/http://www.research.att.com/sw/tools/reuse)


