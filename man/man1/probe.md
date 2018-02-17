# NAME

probe - generate/install/display language processor probe information

# SYNOPSIS

`probe` \[ `options` \] language tool processor

# DESCRIPTION

`probe` generates, installs and displays on the standard output probe
information for the `language` programming language with respect to the
`tool` command as implemented by the `processor` command. The probe
information is in the `tool` command syntax. In general the commands
that rely on probe information (re)generate the information when it is
out of date (see `--generate` ), so direct control is not usually
necessary. However, not all changes to `processor` that would affect the
probe information are detected by this mechanism; such changes require
manual intervention (see `--delete` and `--override`.) A probe
information file (see `--key`) with write mode enabled signifies that
manual changes have been made and disables automatic regeneration (see
`--generate`.)
`probe` information is kept in a file with a pathname based on a hash
of `language`, `tool`, and `processor`. The information is generated by
a
[`sh`](/web/20150527152353/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
script (`probe script`) specific to each `language-processor` pair. Any
options that change the semantics of the language handled by `processor`
should be included in the `processor` operand. e.g., if `cc -++`
processes C++ files, then `processor` should be `cc -++`, not `cc`.

`probe` generation may take a few minutes on some systems or for some
`processors`. Information is shared between users as much as possible.
If the `--key` option produces a path under your `\$HOME` directory
then the probe installation does not support sharing and each user will
have private copies of the generated information.

For some `language`/`tool` combinations, the file
`lib/probe/``language``/``tool``/probe.lcl`, if it exists in the
same directory as the `probe` script, is sourced (via the `.`
[`sh`](/web/20150527152353/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
command) before the probe variables are emitted. The emitted values may
be modified by assigning appropriate `sh` variables (non-identifier
name characters converted to `\_`.) Additional non-standard values may
be written directly to the standard output.

For all `language`/`tool` combinations, the file
`lib/probe/``language``/``tool``/probe.ini`, if it exists in the
same directory as the `probe` script, is sourced (via the `.`
[`sh`](/web/20150527152353/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
command) before the `probe` script proper. `probe.ini` may
completely override the `probe` script by exiting (presumably after
printing its own values on the standard output.)

Sometimes it is necessary to maintain private `probe` information for
some processors or tools. See `--override` for details.

# OPTIONS

-`a`, --`attributes`
:   List probe attribute definitions.

-`d`, --`delete`
:   Delete the current information. Information can only be deleted by
    the generating user.

-`f`, --`force`
:   Force information generation even if it is out of date. Only probe
    information files with write mode disabled can be regenerated.

-`g`, --`generate`
:   Generate the probe information if it is out of date. Only probe
    information files with write mode disabled can be regenerated.

-`k`, --`key`
:   List the probe key path name on the standard output.

-`l`, --`list`
:   List the probe information on the standard output. An error occurs
    if the information has not been generated, unless `--generate` is
    also specified.

-`o`, --`override`=`bindir`
:   Make a writable copy of the probe information file in the directory
    `bindir` `/../lib/probe/``lang`/`tool` and list the generated file
    pathname on the standard output. If `--key` is also specified then
    the override path is listed but not created. When `probe`-based
    commands are run with `bindir` in `\$PATH` before the bin
    directory of the standard probe information the override information
    will be used. Note that since the override file is user writable
    automatic regeneration is disabled.

-`s`, --`silent`
:   By default a message is printed on the standard error when probe
    generation starts; `--silent` disables this message.

-`t`, --`test`
:   Start probe generation but do not save the results. Used for
    debugging probe scripts.

-`v`, --`verify`
:   Each probe information file contains a comment (in the
    `tool` syntax) that can be used to verify the contents. This option
    does that verification.

-`D`, --`debug`
:   Start probe generation, do not save the results, and write the probe
    script trace (see
    [`sh`](/web/20150527152353/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
    `-x`) to the standard error.

# FILES

`lib/probe/``language`/`tool`
:   `tool` specific information directory for `language` processors.

`\$HOME/.probe`
:   Per-user directory when `probe` is installed non-set-uid or the
    probe directory is on a readonly filesystem.

# CAVEATS

To allow probe information to be generated and shared among all users
the executable `lib/probe/probe` must be set-uid to the owner of the
`lib/probe` directory hierarchy and the probe directory filesystem must
be mounted read-write.
Automatic language processor probing is mostly black magic, but then so
are most language processor implementations.

# SEE ALSO

[`cpp`](/web/20150527152353/http://www2.research.att.com/~astopen/man/man1/cpp.html)(1),
[`nmake`](/web/20150527152353/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1),
[`pathkey`](/web/20150527152353/http://www2.research.att.com/~astopen/man/man3/pathkey.html)(3),
[`pathprobe`](/web/20150527152353/http://www2.research.att.com/~astopen/man/man3/pathprobe.html)(3)

# IMPLEMENTATION

`version`
:   probe (AT&T Research) 2007-02-22

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150527152353/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150527152353/http://www.eclipse.org/org/documents/epl-v10.html)

