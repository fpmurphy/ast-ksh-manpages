# NAME

ie - execute a command with ksh-style input editing

# SYNOPSIS

`ie` \[ `options` \] command \[ arg ... \]

# DESCRIPTION

`ie` executes a dynamically linked `command` with ksh-style input
editing on the standard input terminal. The default history file name is
`\$HOME/.``base`, where `base` is the base name of `command` with
leading \[`nox`\] deleted. All processes executed by `command` will
have input editing enabled on the same history file.

# OPTIONS

-`h`, --`history`=`path`
:   Sets the history file name to `path`.

-`n`, --`exec`
:   Execute `command`. `--noexec` shows how `command` would be invoked
    but does not execute. On by default; -`n` means --`noexec`.

# DETAILS

Input editing is implemented by intercepting the
[`read`](/web/20150527152745/http://www2.research.att.com/~astopen/man/man2/read.html)(2)
system call on file descriptor 0 with a dll that is preloaded at process
startup before `main`() is called. The interception mechanism may
involve the environment on some systems; in those cases commands like
[`env`](/web/20150527152745/http://www2.research.att.com/~astopen/man/man1/env.html)(1)
that clear the enviroment before execution may defeat the `ie`
intercept.
Also intercepted are the `\_` and `\_libc\_` name permutations of
the `read` call, as well as any 32-bit and 64-bit versions. `ie`
ignores calls not present in a particular host system. In addition,
`ie` only works on dynamically linked executables that have neither
set-uid nor set-gid permissions. It may not have the intended effect on
programs written in a language or linked with a language runtime that
hides or mangles system call library symbols, or that directly emit
system call instruction sequences rather than using the corresponding
library functions, or that dynamically link libraries outside of the
scope of the `ie` intercepts.

Multi-process client-server applications may misbehave if the `ie`
environment between the related processes is not kept in sync.

# ENVIRONMENT

`ie` is implemented by two components: the `ie` script, located on
`\$PATH` and the `ie` dll (shared library), located either on
`\$PATH` or in one of the `../lib`\` directories on `\$PATH`,
depending on local compilation system conventions. Systems like
`sgi.mips3` that support multiple a.out formats may have multiple
versions of the `ie` dll. In all cases the `ie` script handles the
dll search.

# SEE ALSO

[`3d`](/web/20150527152745/http://www2.research.att.com/~astopen/man/man1/3d.html)(1),
[`sh`](/web/20150527152745/http://www2.research.att.com/~astopen/man/man1/sh.html)(1),
[`trace`](/web/20150527152745/http://www2.research.att.com/~astopen/man/man1/trace.html)(1),
[`warp`](/web/20150527152745/http://www2.research.att.com/~astopen/man/man1/warp.html)(1),
[`read`](/web/20150527152745/http://www2.research.att.com/~astopen/man/man2/read.html)(2)

# IMPLEMENTATION

`version`
:   ie (AT&T Labs Research) 1998-11-30

`author`
:   David Korn

`author`
:   Pat Sullivan

`copyright`
:   Copyright © 1984-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150527152745/http://www.eclipse.org/org/documents/epl-v10.html)


