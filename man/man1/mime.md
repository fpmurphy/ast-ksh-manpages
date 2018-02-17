# NAME

mime - list mime capabilities

# SYNOPSIS

`mime` \[ `options` \] type\
`mime` \[ `options` \] view name type \[ attribute ... \]

# DESCRIPTION

`mime` matches and/or lists mime capability entries. With no operands
all mime entries are listed. With just a `type` operand the mime entry
for `type` is listed. Otherwise the expanded
[`sh`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
command for the `view` operation on the object `name` with mime type
`type` and optional `attribute`(s) is written to the standard output.
`view` may be `-` for the most common action.

# OPTIONS

-`s`, --`silent|quiet`
:   Exit 0 if match found, 1 otherwise, with no diagnostics.

# SEE ALSO

[`file`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/file.html)(1),
[`mailx`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mailx.html)(1),
[`magic`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man3/magic.html)(3),
[`mime`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man3/mime.html)(3)

# IMPLEMENTATION

`version`
:   mime (AT&T Research) 1999-08-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030246/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030246/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030246/http://www.eclipse.org/org/documents/epl-v10.html)


