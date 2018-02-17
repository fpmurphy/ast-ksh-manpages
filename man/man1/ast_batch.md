# NAME

batch - run commands at specified time(s)

# SYNOPSIS

`batch` \[ `options` \] \[ job ... | time ... \]

# DESCRIPTION

`batch` is the command interface to the `at` daemon. It submits
commands to be executed at a future time, lists queue status, and
controls the daemon.
Options that refer to specific jobs interpret the operands as job ids,
otherwise if the `--time` option is not specified then the operands
are interpreted as the start time. If `time` is not specified then the
command is scheduled to be executed immediately, subject to the queue
constraints.

If `--time` is specified then the first non-option argument is the
command to be executed, otherwise the command to be executed is read
from the standard input. The command job id is written to the standard
output after the command has been successfully submitted to the daemon.

# OPTIONS

-`a`, --`access`
:   Check queue access and exit.

-`f`, --`file`=`file`
:   `file` is a script to be run at the specified time.

-`h`, --`label|heading`=`string`
:   Set the job label to `string`.

-`i`, --`info`
:   List queue information and exit.

-`l`, --`list`
:   List queue jobs and exit.

-`m`, --`mail`
:   Send mail when the command completes.

-`n`, --`exec`
:   Execute the command. `--noexec` shows what would be done but does
    not execute. On by default; -`n` means --`noexec`.

-`p`, --`status`
:   List detailed queue status.

-`q`, --`queue`=`queue`
:   Send request to `queue`. Standard queues are:

    [`a`]()
    : The
        [`at`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/at.html)(1) queue.

    [`b`]()
    : The
        [`batch`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/batch.html)(1) queue.

    [`c`]()
    : The
        [`cron`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/cron.html)(1) queue.

-`r`, --`remove`
:   Remove command named by the `job` ... operands from the queue.

-`s`, --`service`=`path`
:   Connect to the
    [`cs`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/cs.html)(1)
    service `path` . The default value is `/dev/tcp/local/at`.

-`t`, --`time|date`=`time`
:   Schedule the command to be run at `time`. Most common date formats
    are accepted. The keyword `every` can be combined with date parts
    to specify repeat executions, e.g., `every Monday`. The default
    value is `now`.

-`u`, --`user`
:   List the per user queue information. Requires sufficient privilege
    to view the status of other users.

-`A`, --`admin`
:   Enable administrative actions. Requires sufficient privilege.

-`D`, --`debug`=`\[level\]\[file\]`
:   Enable `at` daemon debug tracing to `file` at debug level
    `level` . Higher levels produce more output. Requires
    sufficient privilege.

-`L`, --`log`
:   Write the log file path name on the standard output and exit. The
    log file is renamed with a `.old` suffix at the beginning of each
    month and a new log file started.

-`Q`, --`quit`
:   Terminate the `at` daemon. Requires sufficient privilege.

-`U`, --`update`\[=`queuedef`\]
:   Causes the `at` daemon to do a schedule update and re-read the
    queue definition file if it has changed from the last time it
    was read. If `queuedef` is specified then it is interpreted as a
    queue definition file line. See `QUEUE DEFINITIONS` below.
    Requires sufficient privilege. The option value may be omitted.

# QUEUE DEFINITIONS

(`NOTE`: the
[`nroff`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/nroff.html)(1)
style syntax is taken from `X/Open`). The queue definition file
defines queue attributes, one queue per line. Lines starting with `\#`
are comments. The format of a definition line is:
`name`.\[`number``attribute`\]..., where `name` is a single letter
queue name and `number` applies to the following single character
`attribute`. If `number` is omitted then it defaults to `1`. The
default queues are: `a.4j1n2u`, `b.2j2n90w2u`, `c.h8j2u60w`.
Per-queue user access may be specified by appending a space separated
user names after the queue attributes. If the first list element is
`+` then the list specifies users allowed to use the queue; othewise
it specifies users denied access to the queue. If no user list is
specified then queue access is controlled by the global files described
in `QUEUE ACCESS` below. The attributes are:

`h`
: The job environment is initialized to contain at least the `HOME`,
    `LOGNAME`, `USER`, `PATH` and `SHELL` of the
    submitting user. The jobs are also run in the user
    `HOME` directory.

`j`
: The total number of running jobs for all queues is limited to
    `number`.

`l`
: No new jobs will be run until the load average is smaller than
    `number`. This only works on systems where the load average is
    easily determined.

`n`
: The default
    [`nice`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/nice.html)(1)
    priority is set to `number`.

`u`
: The per-user running job limit is set to `number`.

`w`
: At least `number` seconds will elapse before the next job from the
    queue is run.

# QUEUE ACCESS

The user `root` may submit jobs to all queues. If a queue definition
does not specify a user access list then the queue access is controlled
by the default access files in this order:

``(1)
: If the directory `/usr/lib/cron` does not exist then job access is
    granted to all users.

``(2)
: If the file `/usr/lib/cron/at.allow` exists then access is granted
    only to user names listed in this file, one name per line.

``(3)
: If the file `/usr/lib/cron/at.deny` exists then access is denied
    to user names listed in this file, one name per line.

``(4)
: Otherwise access is denied to all users but `root`.

# FILES

`/usr/lib/at/queuedefs`
:   The default queue definition file.

`/usr/lib/cron/at.`(allow|deny)
:   The default queue access files.

# SEE ALSO

[`batch`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/batch.html)(1),
[`crontab`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/crontab.html)(1),
[`nice`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/nice.html)(1),
[`sh`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)

# IMPLEMENTATION

`version`
:   at (AT&T Research) 2000-05-09

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030239/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1996-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030239/http://www.eclipse.org/org/documents/epl-v10.html)


