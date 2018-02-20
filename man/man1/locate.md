# NAME

locate - locate files in pathname database

# SYNOPSIS

`locate` \[ `options` \] pattern ...

# DESCRIPTION

`locate` matches file patterns in a pathname database that is updated
daily by
[`updatedb`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/updatedb.html)(1).

# OPTIONS

-`d`, --`database`=`path`
:   File database path.

-`i`, --`ignorecase`
:   Ignore case in all pattern match expressions.

-`n`, --`show`
:   Show underlying
    [`tw`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/tw.html)(1)
    command but do not execute.

# OPERANDS

`pattern`
:   One or more file patterns. / is matched by pattern metacharacters.

# ENVIRONMENT

`FINDCODES`
:   Path name of locate database.

`LOCATE\_PATH`
:   Alternate path name of locate database.

# FILES

`lib/find/codes`
:   Default locate database.

# SEE ALSO

[`updatedb`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/updatedb.html)(1),
[`tw`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/tw.html)(1)

# IMPLEMENTATION

`version`
:   locate (AT&T Labs Research) 1999-01-23

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030245/http://www.eclipse.org/org/documents/epl-v10.html)


