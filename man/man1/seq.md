# NAME

seq - print a sequence of numbers

# SYNOPSIS

`seq` \[ `options` \] \[ first \[ incr \] \] last

# DESCRIPTION

`seq` writes the numbers from `first` to `last` in steps of
increments. If `first` or `incr` is omitted, it defaults to 1. An
omitted `incr` defaults to 1 even when `last` is smaller than `first`.
`first` `incr`, and `last` are interpreted as floating point values.
`incr` is usually positive if `first` is smaller than `last`, and `incr`
is usually negative if `first` is greater than `last` . When given, the
`format` argument must contain exactly one of the printf-style, floating
point output formats `%e`, `%f`, `%g`.

# OPTIONS

-`f`, --`format`=`format`
:   use printf style floating point `format`. The default value is
    `%g` .

-`s`, --`separator`=`string`
:   use `string` to separate numbers. The default value is `\\n`.

-`w`, --`equal-width`
:   equalize width by padding with leading zeroes.

# EXIT STATUS

`0`
: Success.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`ksh`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1),
[`printf`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)

# IMPLEMENTATION

`version`
:   seq (AT&T Labs Research) 2012-04-14

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030250/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 2007-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030250/http://www.eclipse.org/org/documents/epl-v10.html)


