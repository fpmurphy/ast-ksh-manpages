# NAME

vmstate - list the calling process vmalloc region state

# SYNOPSIS

`vmstate` \[ `options` \]

# DESCRIPTION

When invoked as a shell builtin, `vmstate` lists the calling process
[`vmalloc`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/vmalloc.html)(3)
state for all regions.

# OPTIONS

-`f`, --`format`=`format`
\
List the ids specified by `format`. `format` follows
[`printf`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
conventions, except that
[`sfio`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/sfio.html)(3)
inline ids are used instead of arguments: %\[-+\]\[`width`\[.`precis` \[.`base`\]\]\](`id`)`char`. The supported `id`s are:

`method`
:   The vmalloc method name.

`flags`
:   The vmalloc method flags.

`size`
: The total region size.

`segments`
:   The number of segments in the region.

`busy\_size`
:   The total busy block size.

`busy\_blocks`
:   The number of busy blocks.

`busy\_max`
:   The maximum busy block size.

`free\_size`
:   The total free block size.

`free\_blocks`
:   The number of free blocks.

`free\_max`
:   The maximum free block size.

The default value is `region=%(region)p method=%(method)s
flags=%(flags)s size=%(size)d segments=%(segments)d
busy=(%(busy\_size)d,%(busy\_blocks)d,%(busy\_max)d)
free=(%(free\_size)d,%(free\_blocks)d,%(free\_max)d)`.

# SEE ALSO

[`vmalloc`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/vmalloc.html)(3)

# IMPLEMENTATION

`version`
:   vmstate (AT&T Research) 2010-04-08

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030253/http://www.eclipse.org/org/documents/epl-v10.html)


