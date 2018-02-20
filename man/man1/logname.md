# NAME

logname - return the user's login name

# SYNOPSIS

`logname` \[ `options` \]

# DESCRIPTION

`logname` writes the users's login name to standard output. The login
name is the string that is returned by the
[`getlogin`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/getlogin.html)(2)
function. If
[`getlogin`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/getlogin.html)(2)
does not return successfully, the corresponding to the real user id of
the calling process is used instead.

# EXIT STATUS

`0`
: Successful Completion.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`getlogin`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/getlogin.html)(2)

# IMPLEMENTATION

`version`
:   logname (AT&T Research) 1999-04-30

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030245/http://www.eclipse.org/org/documents/epl-v10.html)


