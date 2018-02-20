# NAME

cd - change working directory

# SYNOPSIS

`cd` \[ `options` \] \[directory\]\

`cd` \[ `options` \] old new

# DESCRIPTION

`cd` changes the current working directory of the current shell
environment.

In the first form with one operand, if `directory` begins with `/`, or
if the first component is `.` or `..`, the directory will be changed
to this directory. If directory is `-`, the directory will be changed
to the last directory visited. Otherwise, if the `CDPATH` environment
variable is set, `cd` searches for `directory` relative to each
directory named in the colon separated list of directories defined by
`CDPATH`. If `CDPATH` not set, `cd` changes to the directory
specified by `directory`.

In the second form, the first occurrence of the string `old` contained
in the pathname of the present working directory is replaced by the
string `new` and the resulting string is used as the directory to which
to change.

When invoked without operands and when the `HOME` environment variable
is set to a nonempty value, the directory named by the `HOME`
environment variable will be used. If `HOME` is empty or unset, `cd`
will fail.

When `cd` is successful, the `PWD` environment variable will be set
to the name of an absolute pathname that does not contain any `..`
components corresponding to the new directory. The environment variable
`OLDPWD` will be set to the previous value of `PWD`. If the new
directory is found by searching the directories named by `CDPATH`, or
if `directory` is `-`, or if the two operand form is used, the new
value of `PWD` will be written to standard output.

If both `-L` and `-P` are specified, the last one specified will be
used. If neither `-P` or `-L` is specified then the behavior will be
determined by the `getconf` parameter `PATH\_RESOLVE`. If
`PATH\_RESOLVE` is `physical`, then the behavior will be as if
`-P` were specified. Otherwise, the behavior will be as if `-L` were
specified.

# OPTIONS

-`L`
: Handle each pathname component `..` in a logical fashion by moving
    up one level by name in the present working directory.

-`P`
: The present working directory is first converted to an absolute
    pathname that does not contain symbolic link components and symbolic
    name components are expanded in the resulting directory name.

# EXIT STATUS

`0`
: Directory successfully changed.

`&gt;0`
: An error occurred.

# SEE ALSO

[`pwd`](/web/20151120075915/http://www2.research.att.com:80/~astopen/man/man1/pwd.html)(1),
[`getconf`](/web/20151120075915/http://www2.research.att.com:80/~astopen/man/man1/getconf.html)(1)

# IMPLEMENTATION

`version`
: cd (AT&T Research) 1999-06-05

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20151120075915/http://www.opensource.org/licenses/cpl1.0.txt)


