# NAME

pids - list calling shell process ids

# SYNOPSIS

`pids` \[ `options` \]

# DESCRIPTION

When invoked as a shell builtin, `pids` lists one or more of the
calling process ids determined by
[`getpid`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/getpid.html)(2),
[`getppid`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/getppid.html)(2),
[`getpgrp`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/getpgrp.html)(2),
[`tcgetpgrp`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/tcgetpgrp.html)(2)
and
[`getsid`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/getsid.html)(2).
Unknown or invalid ids have the value `-1`.

# OPTIONS

-`f`, --`format`=`format`
\
List the ids specified by `format`. `format` follows
[`printf`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
conventions, except that
[`sfio`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man3/sfio.html)(3)
inline ids are used instead of arguments: %\[-+\]\[`width`\[.`precis` \[.`base`\]\]\](`id`)`char`. The supported `id`s are:

`pid`
: The process id.

`pgid`
: The process group id.

`ppid`
: The parent process id.

`tid|tty`
:   The controlling terminal id.

`sid`
: The session id.

The default value is `PID=%(pid)d PPID=%(ppid)d PGID=%(pgid)d
TID=%(tid)d SID=%(sid)d`.

# SEE ALSO

[`getpid`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/getpid.html)(2),
[`getppid`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/getppid.html)(2),
[`getpgrp`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/getpgrp.html)(2),
[`tcgetpgrp`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/tcgetpgrp.html)(2),
[`getsid`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man2/getsid.html)(2)

# IMPLEMENTATION

`version`
:   pids (AT&T Research) 2011-08-27

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030248/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030248/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030248/http://www.eclipse.org/org/documents/epl-v10.html)


