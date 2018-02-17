# NAME

funzip - fast gunzip

# SYNOPSIS

`funzip` \[ `options` \] \[ file \]

# DESCRIPTION

`funzip` decompresses
[`gzip`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1)
compressed files. By default `gzip` crc32 cyclic redundancy checking
is disabled. This may speed up decompression by 25% or more over
[`gunzip`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/gunzip.html)(1).
Most data corruption errors are still caught even with crc disabled.

# OPTIONS

-`x`, --`crc`
:   Enable `gzip` crc32 cyclic redundancy checking for decompress. On
    some systems this can double the execution wall time. Most data
    corruption errors are still caught even with `nocrc`.

# SEE ALSO

[`gzip`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1),
[`gunzip`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/gunzip.html)(1),
[`libz`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man3/libz.html)(3)

# IMPLEMENTATION

`version`
:   funzip (AT&T Research) 1998-08-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030244/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1998-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030244/http://www.eclipse.org/org/documents/epl-v10.html)


