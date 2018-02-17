# NAME

tty - write the name of the terminal to standard output

# SYNOPSIS

`tty` \[ `options` \]

# DESCRIPTION

`tty` writes the name of the terminal that is connected to standard
input onto standard output. If the standard input is not a terminal,
"`not a tty`" will be written to standard output.

# OPTIONS

-`l`, --`line-number`
:   Write the synchronous line number of the terminal on a separate line
    following the terminal name line. If the standard input is not a
    synchronous terminal then "`not on an active synchronous line`"
    is written.

-`s`, --`silent|quiet`
:   Disable the terminal name line. Use `\[\[ -t 0 \]\]` instead.

# EXIT STATUS

`0`
: Standard input is a tty.

`1`
: Standard input is not a tty.

`2`
: Invalid arguments.

`3`
: A an error occurred.

# IMPLEMENTATION

`version`
:   tty (AT&T Research) 2008-03-13

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030252/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030252/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030252/http://www.eclipse.org/org/documents/epl-v10.html)


