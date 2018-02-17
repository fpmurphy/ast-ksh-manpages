# NAME

shift - shift positional parameters

# SYNOPSIS

`shift` \[ `options` \] \[n\]

# DESCRIPTION

`shift` is a shell special built-in that shifts the positional
parameters to the left by the number of places defined by `n`, or `1`
if `n` is omitted. The number of positional parameters remaining will be
reduced by the number of places that are shifted.

If `n` is given, it will be evaluated as an arithmetic expression to
determinate the number of places to shift. It is an error to shift more
than the number of positional parameters or a negative number of places.

# EXIT STATUS

`0`
: The positional parameters were successfully shifted.

`&gt;0`
: An error occurred.

# SEE ALSO

[`set`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/set.html)(1)

# IMPLEMENTATION

`version`
: shift (AT&T Research) 1999-07-07

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030250/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030250/http://www.opensource.org/licenses/cpl1.0.txt)


