# NAME

basename - strip directory and suffix from filenames

# SYNOPSIS

`basename` \[ `options` \] string \[suffix\]\
`basename` \[ `options` \] string ...

# DESCRIPTION

`basename` removes all leading directory components from the file name
defined by `string`. If the file name defined by `string` has a suffix
that ends in `suffix`, it is removed as well.
If `string` consists solely of `/` characters the output will be a
single `/` unless `PATH\_LEADING\_SLASHES` returned by
[`getconf`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/getconf.html)(1)
is `1` and `string` consists of multiple `/` characters in which
case `//` will be output. Otherwise, trailing `/` characters are
removed, and if there are any remaining `/` characters in `string`,
all characters up to and including the last `/` are removed. Finally,
if `suffix` is specified, and is identical the end of `string`, these
characters are removed. The characters not removed from `string` will be
written on a single line to the standard output.

# OPTIONS

-`a`, --`all`
:   All operands are treated as `string` and each modified pathname is
    printed on a separate line on the standard output.

-`s`, --`suffix`=`suffix`
:   All operands are treated as `string` and each modified pathname,
    with `suffix` removed if it exists, is printed on a separate line on
    the standard output.

# EXIT STATUS

`0`
: Successful Completion.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`dirname`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/dirname.html)(1),
[`getconf`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/getconf.html)(1),
[`basename`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man3/basename.html)(3)

# IMPLEMENTATION

`version`
:   basename (AT&T Research) 2010-05-06

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030239/http://www.eclipse.org/org/documents/epl-v10.html)


