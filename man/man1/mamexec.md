# NAME

mamexec - make abstract machine executor

# SYNOPSIS

`mamexec` \[ `options` \] \[ target ... \]

# DESCRIPTION

`mamexec` reads MAM (Make Abstract Machine) target and prerequisite
file descriptions from the standard input and executes actions to update
targets that are older than their prerequisites. Mamfiles are generated
by the `--mam` option of
[`nmake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
and
[`gmake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/gmake.html)(1)
and are portable to environments that only have
[`sh`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
and
[`cc`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/cc.html)(1).
A separate
[`mamstate`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mamstate.html)(1)
program is used to compare current and state file target times.
`mamexec` is a
[`ksh`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
script implementation that has been replaced by the standalone
[`mamake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mamake.html)(1).
New applications should use `mamake`.

# OPTIONS

-`d`, --`debug`
:   Set the debug trace level to `level`. Higher levels produce
    more output.

-`f`, --`force`
:   Force all targets to be out of date.

-`i`, --`ignore`
:   Ignore shell action errors.

-`n`, --`exec`
:   Enable shell action execution. On by default; -`n` means
    --`noexec`.

-`s`, --`silent`
:   Do not trace shell actions as they are executed.

# SEE ALSO

[`mamake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mamake.html)(1),
[`mamstate`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mamstate.html)(1),
[`nmake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)

# IMPLEMENTATION

`version`
:   mamexec (AT&T Labs Research) 1994-04-17

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030246/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030246/http://www.eclipse.org/org/documents/epl-v10.html)


