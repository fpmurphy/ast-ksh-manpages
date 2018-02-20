# NAME

mamsh - make abstract machine to shell script conversion filter

# SYNOPSIS

`mamsh` \[ `options` \]

# DESCRIPTION

`mamsh` converts `MAM` (Make Abstract Machine) instructions on the
standard input to a
[`sh`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
script that updates all targets on the standard output. The script
summarily builds each target; use
[`mamake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mamake.html)(1),
[`nmake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
or
[`gmake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/gmake.html)(1)
for target out-of-date testing.

# SEE ALSO

[`mamake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mamake.html)(1),
[`nmake`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)

# IMPLEMENTATION

`version`
:   mamsh (AT&T Labs Research) 1994-01-01

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030246/http://www.eclipse.org/org/documents/epl-v10.html)


