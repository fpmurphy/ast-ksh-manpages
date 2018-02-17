# NAME

kill - terminate or signal process

# SYNOPSIS

`kill` \[ `options` \] job ...\

`kill` \[ `options` \] -l \[arg ...\]

# DESCRIPTION

With the first form in which `-l` is not specified, `kill` sends a
signal to one or more processes specified by `job`. This normally
terminates the processes unless the signal is being caught or ignored.

A `job` can be specified as one of the following:

`number`
: `number` refers to a process id.

`-``number`
: `number` refers to a process group id.

`%``number`
: `number` refer to a job number.

`%``string`
: Refers to a job whose name begins with `string`.

`%?``string`
: Refers to a job whose name contains `string`.

`%+` or `%%`
: Refers to the current job.

`%-`
: Refers to the previous job.

If the signal is not specified with either the `-n` or the `-s`
option, the `SIGTERM` signal is used.

If `-l` is specified, and no `arg` is specified, then `kill` writes
the list of signals to standard output. Otherwise, `arg` can be either a
signal name, or a number representing either a signal number or exit
status for a process that was terminated due to a signal. If a name is
given the corresponding signal number will be written to standard
output. If a number is given the corresponding signal name will be
written to standard output.

# OPTIONS

-`l`
: List signal names or signal numbers rather than sending signals as
    described above. The `-n` and `-s` options cannot be specified.

-`n` `signum`
: Specify a signal number to send. Signal numbers are not portable
    across platforms, except for the following:

    [`0`]()
    : No signal

    [`1`]()
    : `HUP`

    [`2`]()
    : `INT`

    [`3`]()
    : `QUIT`

    [`6`]()
    : `ABRT`

    [`9`]()
    : `KILL`

    [`14`]()
    : `ALRM`

    [`15`]()
    : `TERM`

-`s` `signame`

Specify a signal name to send. The signal names are derived from their
names in `&lt;signal.h&gt;` without the `SIG` prefix and are case
insensitive. `kill -l` will generate the list of signals on the
current platform.

# EXIT STATUS

`0`
: At least one matching process was found for each `job` operand, and
    the specified signal was successfully sent to at least one
    matching process.

`&gt;0`
: An error occurred.

# SEE ALSO

[`ps`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/ps.html)(1),
[`jobs`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/jobs.html)(1),
[`kill`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/kill.html)(2),
[`signal`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/signal.html)(2)

# IMPLEMENTATION

`version`
: kill (AT&T Research) 1999-06-17

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030245/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030245/http://www.opensource.org/licenses/cpl1.0.txt)


