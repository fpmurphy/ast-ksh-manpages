# NAME

dirname - return directory portion of file name

# SYNOPSIS

`dirname` \[ `options` \] string

# DESCRIPTION

`dirname` treats `string` as a file name and returns the name of the
directory containing the file name by deleting the last component from
`string`.
If `string` consists solely of `/` characters the output will be a
single `/` unless `PATH\_LEADING\_SLASHES` returned by
[`getconf`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/getconf.html)(1)
is `1` and `string` consists of multiple `/` characters in which
case `//` will be output. Otherwise, trailing `/` characters are
removed, and if there are no remaining `/` characters in `string`, the
string `.` will be written to standard output. Otherwise, all
characters following the last `/` are removed. If the remaining string
consists solely of `/` characters, the output will be as if the
original string had consisted solely as `/` characters as described
above. Otherwise, all trailing slashes are removed and the output will
be this string unless this string is empty. If empty the output will be
`.`.

# OPTIONS

-`f`, --`file`
:   Print the `\$PATH` relative regular file path for `string`.

-`r`, --`relative`
:   Print the `\$PATH` relative readable file path for `string`.

-`x`, --`executable`
:   Print the `\$PATH` relative executable file path for `string`.

# EXIT STATUS

`0`
: Successful Completion.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`basename`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/basename.html)(1),
[`getconf`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/getconf.html)(1),
[`dirname`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man3/dirname.html)(3),
[`pathname`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man3/pathname.html)(3)

# IMPLEMENTATION

`version`
:   dirname (AT&T Research) 2009-01-31

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030242/http://www.eclipse.org/org/documents/epl-v10.html)


