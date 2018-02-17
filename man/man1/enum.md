# NAME

enum - create an enumeration type

# SYNOPSIS

`enum` \[ `options` \] `typename`\[`=`( `` `value` ... `)`\]

# DESCRIPTION

`enum` is a declaration command that creates an enumeration type
`typename` that can only store any one of the values in the indexed
array variable `typename`.

If the list of `value`s is omitted, then `typename` must name an indexed
array variable with at least two elements.

# OPTIONS

-`i`, --`ignorecase`
: The values are case insensitive.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
: An error occurred.

# SEE ALSO

[`ksh`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1),
[`typeset`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/typeset.html)(1).

# IMPLEMENTATION

`version`
: enum (AT&T Research) 2008-01-08

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030243/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030243/http://www.opensource.org/licenses/cpl1.0.txt)


