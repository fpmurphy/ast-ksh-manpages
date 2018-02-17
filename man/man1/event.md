# NAME

event - shared event client and server

# SYNOPSIS

`event` \[ `options` \] name \[ request \[ options \] \[ arg ... \] \]
\[ : request ... \]

# DESCRIPTION

`event` is a shared event client and server. Events are stored in a
persistent database named by the `name` operand. Each event has a name,
an expiration, and a binary status `raised` or `not-raised`. A
non-existent event is `not-raised`. Events may be raised, deleted,
cleared, tested and waited for. If no `request` operands are specified
then requests are prompted for, with an `EVENT&gt;` prompt, and read
from the standard input. Multiple command line requests must be
separated by `:`. In the following events operands are matched by
[`ksh`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
patterns. The client requests are:

`all` `connection`
:   Raise all pending events for the `connection`. Mainly for debugging.

`clear` `event` ...
:   Mark `event` not-raised but do not delete from the database. This
    allows the events to be matched by patterns.

`delete` `event` ...
:   Delete `event`.

`exit`
: Close the client connection.

`hold \[` `event` ...\]
:   If `event` operands are specified then clients are not notified
    about the those events until they are explicitly released by
    `release` `event` ... If no events are specified then all current
    and future events will be unconditionally held until a `release`
    with no event operands.

`info`
: List the server status pending events by client connection. The list
    is terminated by a `done` message.

`list \[` `pattern` \]
:   Start an event dictionary scan and list the first event. If
    `pattern` is specified then only events matching `pattern`
    are listed.

`next`
: List the next event in the `list` event scan. The list is
    terminated by a `done` message.

`quit`
: Equivalent to exit.

`raise` `event` ...
:   Raise `event` ...

`release \[` `event` ...\]
:   If `event` operands are specified then they are released from a
    previous `hold` `event` ... If no `event` operands are specified
    then any previous unconditional `hold` is turned off.

[`set` `option` ...]()\
`stop`
: Terminate the server. Persistent data is preserved.

`test` `event`
:   Determine the `event` status.

`wait` `event`
:   Wait for `event` status to be `raised`.

The `--cs`, `--expire`, `--initialize`, and `--log` options
apply to the initial service command, and the `--expire` , `--log`,
`--newer`, `--older`, and `--quiet` options apply to client
requests.

# OPTIONS

-`c`, --`cs|connect-stream`=`connect-stream`
:   Use `connect-stream` instead of the default. The default value is
    `/dev/tcp/local/event`.

-`e`, --`expire`=`date-expression`
:   Set the current event expiration to the
    [`date`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/date.html)(1)
    or
    [`cron`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/cron.html)(1)
    expression `date-expression`.

-`i`, --`initialize`
:   Initialize the service if it is not already running.

-`l`, --`log`
:   Log server activity to `state-name`.log, where `state-name` is the
    state path name sans suffix. On by default; -`l` means
    --`nolog`.

-`n`, --`newer`=`date`
:   Match events newer than `date`. If `--older` is also specified
    then only event times &gt; newer and &lt; older match.

-`o`, --`older`=`date`
:   Match events older than `date`. If `--newer` is also specified
    then only event times &gt; newer and &lt; older match.

-`q`, --`quiet`
:   Suppress request confirmation messages.

# CAVEATS

Expirations, logging and the `set` request are not implemented yet.

# SEE ALSO

[`coshell`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/coshell.html)(1),
[`cs`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/cs.html)(1),
[`nmake`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1),
[`dbm`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man3/dbm.html)(3),
[`ndbm`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man3/ndbm.html)(3),
[`gdbm`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man3/gdbm.html)(3)

# IMPLEMENTATION

`version`
:   event (AT&T Research) 2007-06-05

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030243/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1990-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030243/http://www.eclipse.org/org/documents/epl-v10.html)


