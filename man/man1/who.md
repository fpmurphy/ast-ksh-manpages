# NAME

who - display who is on the system

# SYNOPSIS

`who` \[ `options` \] \[am I\]

# DESCRIPTION

`who` displays various pieces of information about logged in users to
standard output.
`who` lists the user's name, terminal line, login time, and remote
host name, if applicable, for each logged in user it reports.

The second form, `who am I` is equivalent to `who -m`.

# OPTIONS

-`i`, --`idle`
:   Also writes the idle time for each displayed user. The idle time is
    the time since last activity on that line.

-`m`
: Write only information about the current terminal.

-`q`, --`count`
:   Writes only the login names and the number of users logged on. This
    options overrides other options.

-`s`
: This option is ignored.

-`u`
: Equivalent to `-i`.

-`w`, --`writable`
:   Equivalent to `-T`.

-`H`, --`heading`
:   Put a heading line in before of the output.

-`T`, --`mesg`
:   Specifies the state of the terminal as one of the following:

    [`+`]()
    : The terminal allows write access to other users.

    [`-`]()
    : The terminal denies write access to other users.

    [`?`]()
    : The write access cannot be determined.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
:   One or more errors occurred.

# SEE ALSO

[`date`](/web/20141128030254/http://www2.research.att.com/~astopen/man/man1/date.html)(1),
[`login`](/web/20141128030254/http://www2.research.att.com/~astopen/man/man1/login.html)(1)

# IMPLEMENTATION

`version`
:   who (AT&T Research) 2004-03-25

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030254/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030254/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030254/http://www.eclipse.org/org/documents/epl-v10.html)


