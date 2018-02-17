# NAME

warp - execute a command in a different time frame

# SYNOPSIS

`warp` \[ `options` \] date \[ command \[ arg ... \] \]

# DESCRIPTION

`warp` executes a dynamically linked `command` in a different time
frame by intercepting time related system calls and modifying the times
seen by `command` using the formula: [`time = time + warp +` (time - base) \` (factor - 1)]()
where `warp` is `date-now`, `base` is `date` by default, and `factor` is
1 by default. Command argument date specifications support common
conventions: [`yesterday`]() [`next week`]() [`50 days`]()
[`2000-02-28+00`]() [`feb 28 2000`]() [`\#``seconds`]()
A `time\_t` value in `seconds` since the epoch.

# OPTIONS

-`b`, --`base`=`date`
:   Set the base or starting date to `date`. Useful for repeating a set
    of tests. The default value is `date`.

-`f`, --`factor`=`factor`
:   Set the warped clock to tick at `factor` seconds per real second.
    The default value is `1`.

-`n`, --`exec`
:   Execute `command`. `--noexec` shows how `command` would be invoked
    but does not execute. On by default; -`n` means --`noexec`.

-`t`, --`trace`
:   Trace each intercepted system call on the standard error.

# DETAILS

`warp` executes `command` with optional `args`, or
[`sh`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
if `command` is omitted. All processes executed by `command` are warped
in the same time frame. Time progresses for `command` and its children
at the rate of `factor` times the system clock. Any files created by
`command` or its children will appear newer than `date` to `command` and
its children, but will actually be in the normal time frame for
non-warped commands.
Processes are warped by intercepting system calls with a dll that is
preloaded at process startup before `main`() is called. The interception
mechanism may involve the environment on some systems; in those cases
commands like
[`env`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man1/env.html)(1)
that clear the enviroment before execution may defeat the `warp`
intercepts. The intercepted system calls are: [`alarm`]()
[`fstat`]() [`getitimer`]() [`gettimeofday`]() [`lstat`]()
[`poll`]() [`select`]() [`setitimer`]() [`stat`]() [`time`]()
[`times`]() [`utime`]() [`utimes`]()

Also intercepted are the `\_` and `\_libc\_` name permutations of
the calls, as well as any 32-bit and 64-bit versions, and the abominable
System V `x` versions of the
[`stat`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man2/stat.html)(2)
family. `warp` ignores calls not present in a particular host system.
In addition, `warp` only works on dynamically linked executables that
have neither set-uid set-uid nor set-gid permissions. It may not have
the intended effect on programs written in a language or linked with a
language runtime that hides or mangles system call library symbols, or
that directly emit system call instruction sequences rather than using
the corresponding library functions, or that dynamically link libraries
outside of the scope of the `warp` intercepts.

Multi-process client-server applications may misbehave if the `warp`
environment between the related processes is not kept in sync.

# ENVIRONMENT

`warp` is implemented by three components: the `warp` script,
located on `\$PATH`; the `warp` dll (shared library), located either
on `\$PATH` or in one of the `../lib`\` directories on `\$PATH`,
depending on local compilation system conventions; and the `ast`
[`date`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man1/date.html)(1)
command, located on `\$PATH`, that supports conversion to/from
`time\_t` values at the shell level. Systems like `sgi.mips3` that
support multiple a.out formats may have multiple versions of the
`warp` dll. In all cases the `warp` script handles the dll search.

# EXAMPLES

`\$ date -f %K`
:   1998-03-11+13:41

`\$ warp 2000-02-29+12:30:30 date -f %K`
:   2000-02-29+12:30

`\$ warp "2 years" date -f %K`
:   2000-01-01+00:00

`\$ PS1="`(warp) " warp -f \$((60\`60\`24)) 2000-02-29+12:30:30
:   \# interactive
    [`sh`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
    where 1 warped day passes for each real second.

# SEE ALSO

[`3d`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man1/3d.html)(1),
[`date`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man1/date.html)(1),
[`env`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man1/env.html)(1),
[`ie`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man1/ie.html)(1),
[`sh`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man1/sh.html)(1),
[`trace`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man1/trace.html)(1),
[`stat`](/web/20150527153211/http://www2.research.att.com/~astopen/man/man2/stat.html)(2)

# IMPLEMENTATION

`version`
:   warp (AT&T Labs Research) 1999-11-19

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150527153211/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1998-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150527153211/http://www.eclipse.org/org/documents/epl-v10.html)


