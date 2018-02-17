# NAME

ss - list local network system status

# SYNOPSIS

`ss` \[ `options` \] \[ host ... \]

# DESCRIPTION

`ss` writes the system status of hosts on the local network to the
standard output. The option order determines the listing sort keys, from
left to right, hightest to lowest precedence. If one or more `host`
operands are given then only the status to those hosts is listed,
otherwise the status for all hosts on the local network is listed.
Static information for hosts in the local network is in the file
`../share/lib/cs/local` on `\$PATH`; see
[`cs`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/cs.html)(1)
for details. Dynamic status for each active host is maintained in the
file `../share/lib/ss/``host` by a status daemon `ssd` running on each
host. This information is updated once a minute, plus or minus a random
part of a minute. `ss` starts an `ssd`s as necessary. An `ssd` may
be killed by removing the corresponding host status file.

# OPTIONS

-`c`, --`cpu`
:   Sort by cpu utilization.

-`i`, --`idle`
:   Sort by user idle time.

-`l`, --`load`
:   Sort by load average.

-`r`, --`reverse`
:   Reverse the sort order.

-`t`, --`time`
:   Sort by system up time.

-`u`, --`users`
:   Sort by number of active users.

# FILES

`../share/lib/cs/local`
:   Local host info list on `\$PATH`.

`../share/lib/ss/``host`
:   Host status files on `\$PATH`.

# SEE ALSO

[`cs`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/cs.html)(1)

# IMPLEMENTATION

`version`
:   ss (AT&T Research) 1995-05-09

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030251/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1990-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030251/http://www.eclipse.org/org/documents/epl-v10.html)


