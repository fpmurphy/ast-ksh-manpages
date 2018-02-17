# NAME

crossexec - cross compiler a.out execution

# SYNOPSIS

`crossexec` \[ `options` \] crosstype command \[ option ... \] \[ file ... \]

# DESCRIPTION

`crossexec` runs a cross-compiled `command` in an environment that
supports a cross-compilation architecture different from the current
host. The cross environment is determined by `crosstype`, usually a host
type name produced by
[`package`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/package.html)(1).
`crosstype` is used to find an entry in `\$HOME/.crossexec` that
specifies the cross compiler host and access details.
The exit status of `crossexec` is the exit status of `command`.

# CROSS ENVIRONMENT FILE

`\$HOME/.crossexec` contains one line for each supported `crosstype`.
Each line contains 5 tab separated fields. Field default values are
specified as `-`. The fields are:

`crosstype`
:   The host type produced by
    [`package`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/package.html)(1).

`host`
: The host name.

`user`
: The user name on `host`. The default is the current user.

`dir`
: The directory to copy `command` and execute it. The default is the
    `user` `\$HOME` on `host`.

`shell`
:   The command used to get shell access to `host`. Currently only
    `rsh` and `ssh` are supported.

`copy`
: The command used to copy `command` to `host`. Currently only `rcp`
    and `scp` are supported.

# OPTIONS

-`n`, --`show`
:   Show the underlying commands but do not execute.

# SEE ALSO

[`rcp`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/rcp.html)(1),
[`rsh`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/rsh.html)(1),
[`scp`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/scp.html)(1),
[`ssh`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/ssh.html)(1)

# IMPLEMENTATION

`version`
:   crossexec (AT&T Labs Research) 2004-01-04

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030242/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1994-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030242/http://www.eclipse.org/org/documents/epl-v10.html)


