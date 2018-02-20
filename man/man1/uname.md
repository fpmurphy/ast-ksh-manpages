# NAME

uname - identify the current system

# SYNOPSIS

`uname` \[ `options` \] \[ name ... \]

# DESCRIPTION

By default `uname` writes the operating system name to standard
output. When options are specified, one or more system characteristics
are written to standard output, space separated, on a single line. When
more than one option is specified the output is in the order specfied by
the `-A` option below. Unsupported option values are listed as
`\[option\]`. If any unknown options are specified then the local
`/usr/bin/uname` is called.
If any `name` operands are specified then the
[`sysinfo`](/web/20150527154241/http://www2.research.att.com/~astopen/man/man2/sysinfo.html)(2)
values for each `name` are listed, separated by space, on one line.
[`getconf`](/web/20150527154241/http://www2.research.att.com/~astopen/man/man1/getconf.html)(1),
a pre-existing `standard` interface, provides access to the same
information; vendors should spend more time using standards than
inventing them.

Selected information is printed in the same order as the options below.

# OPTIONS

-`a`, --`all`
:   Equivalent to `-snrvmpio`.

-`s`, --`system|sysname|kernel-name`
:   The detailed kernel name. This is the default.

-`n`, --`nodename`
:   The hostname or nodename.

-`r`, --`release|kernel-release`
:   The kernel release level.

-`v`, --`version|kernel-version`
:   The kernel version level.

-`m`, --`machine`
:   The name of the hardware type the system is running on.

-`p`, --`processor`
:   The name of the processor instruction set architecture.

-`i`, --`implementation|platform|hardware-platform`
:   The hardware implementation; this is `--host-id` on some systems.

-`o`, --`operating-system`
:   The generic operating system name.

-`h`, --`host-id|id`
:   The host id in hex.

-`d`, --`domain`
:   The domain name returned by
    [`getdomainname`](/web/20150527154241/http://www2.research.att.com/~astopen/man/man2/getdomainname.html)(2).

-`R`, --`extended-release`
:   The extended release name.

-`A`, --`everything`
:   Equivalent to `-snrvmpiohdR`.

-`f`, --`list`
:   List all
    [`sysinfo`](/web/20150527154241/http://www2.research.att.com/~astopen/man/man2/sysinfo.html)(2)
    names and values, one per line.

-`S`, --`sethost`=`name`
:   Set the hostname or nodename to `name`. No output is written to
    standard output.

# SEE ALSO

[`hostname`](/web/20150527154241/http://www2.research.att.com/~astopen/man/man1/hostname.html)(1),
[`getconf`](/web/20150527154241/http://www2.research.att.com/~astopen/man/man1/getconf.html)(1),
[`uname`](/web/20150527154241/http://www2.research.att.com/~astopen/man/man2/uname.html)(2),
[`sysconf`](/web/20150527154241/http://www2.research.att.com/~astopen/man/man2/sysconf.html)(2),
[`sysinfo`](/web/20150527154241/http://www2.research.att.com/~astopen/man/man2/sysinfo.html)(2)

# IMPLEMENTATION

`version`
:   uname (AT&T Research) 2007-04-19

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150527154241/http://www.eclipse.org/org/documents/epl-v10.html)


