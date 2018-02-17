# NAME

unalias - remove alias definitions

# SYNOPSIS

`unalias` \[ `options` \] name...

# DESCRIPTION

`unalias` removes the definition of each named alias from the current
shell execution environment, or all aliases if `-a` is specified. It
will not affect any commands that have already been read and
subsequently executed.

# OPTIONS

-`a`
: Causes all alias definitions to be removed. `name` operands are
    optional and ignored in this case.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
: `-a` was not specified and one or more `name` operands did not
    have an alias definition, or an error occurred.

# SEE ALSO

[`alias`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/alias.html)(1)

# IMPLEMENTATION

`version`
: unalias (AT&T Research) 1999-07-07

`author`
: David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030252/mailto:dgkorn@gmail.com)&gt;

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030252/http://www.opensource.org/licenses/cpl1.0.txt)


