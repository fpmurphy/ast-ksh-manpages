# NAME

sleep - suspend execution for an interval

# SYNOPSIS

`sleep` \[ `options` \] \[ duration \]

# DESCRIPTION

`sleep` suspends execution for at least the time specified by
`duration` or until a `SIGALRM` signal is received. `duration` may be
one of the following:

`integer`
: The number of seconds to sleep.

`floating point`
: The number of seconds to sleep. The actual granularity depends on
    the underlying system, normally around 1 millisecond.

`P``n``Y``n``M``n``DT``n``H``n``M``n``S`
: An ISO 8601 duration where at least one of the duration parts must
    be specified.

`P``n``W`
: An ISO 8601 duration specifying `n` weeks.

`p``n``Y``n``M``n``DT``n``H``n``m``n``S`
: A case insensitive ISO 8601 duration except that `M` specifies
    months, `m` before `s` or `S` specifies minutes and after
    specifies milliseconds, `u` or `U` specifies microseconds, and
    `n` specifies nanoseconds.

`date/time`
: Sleep until the
    [`date`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/date.html)(1)
    compatible date/time.

# OPTIONS

-`s`
: Sleep until a signal or a timeout is received. If `duration` is
    omitted or 0 then no timeout will be used.

# EXIT STATUS

`0`
: The execution was successfully suspended for at least `duration` or
    a `SIGALRM` signal was received.

`&gt;0`
: An error occurred.

# SEE ALSO

[`date`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/date.html)(1),
[`time`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/time.html)(1),
[`wait`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/wait.html)(1)

# IMPLEMENTATION

`version`
: sleep (AT&T Research) 2009-03-12

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030250/http://www.opensource.org/licenses/cpl1.0.txt)


