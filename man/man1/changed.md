# NAME

changed - check local host/server entities for change

# SYNOPSIS

`changed` \[ `options` \]

# DESCRIPTION

`changed` checks local host/server entities for change or stangnation.
The file `\$HOME/lib/changed/CHECK` must contain calls to the
`check` function for each entity to be checked. `changed` is
typically set to run daily via
[`crontab`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/crontab.html)(1).
The `check` function operands are:

`\[ every` `day` \]
:   Optional day of week limitation.

`operation`
:   Either `changed` or `stagnant`. `changed` expects no change
    between checks and `stagnant` expects any change between checks.

`check\_function`
:   A user supplied function (in the `CHECK` file) that does the
    actual check. The standard output and standard error of this
    function are compared against previous results to determine change.
    This output should be enough to identify the nature of
    the change(s).

`entity`
:   The entity being checked.

`host ...`
:   One or more hosts to check. The caller must have password-less
    [`ssh`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/ssh.html)(1)
    access to the hosts.

These `check\_function`s are provided by `changed`:

`check\_file\_changed`
:   Checks regular and executable files for change.

`check\_ksh\_changed`
:   Checks ksh executables for change.

# OPTIONS

-`m`, --`mail`=`user`
:   Mail changes to `user`.

-`n`, --`show`
:   Show actions but do not execute.

-`r`, --`recent`
:   Show most recent changes.

# EXAMPLES

`\$HOME/lib/changed/CHECK` example `check` calls: check changed
check\_ksh\_changed /bin/ksh penguin www check every friday stagnant
check\_sw\_download\_stagnant downloads www public
Example
[`crontab`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/crontab.html)(1)
entry: 11 23 \` \` \` ksh -c 'PATH=\$HOME/bin:/usr/common/ast/bin:\$PATH
changed -m bozo'

# SEE ALSO

[`ssh`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/ssh.html)(1)

# IMPLEMENTATION

`version`
:   changed (AT&T Research) 2011-04-11

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1990-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030240/http://www.eclipse.org/org/documents/epl-v10.html)


