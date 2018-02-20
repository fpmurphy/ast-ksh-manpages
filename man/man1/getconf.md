# NAME

getconf - get configuration values

# SYNOPSIS

`getconf` \[ `options` \] \[ name \[ path \[ value \] \] ... \]

# DESCRIPTION

`getconf` displays the system configuration value for `name`. If
`name` is a filesystem specific variable then the value is determined
relative to `path` or the current directory if `path` is omitted. If
`value` is specified then `getconf` attempts to change the process
local value to `value`. `-` may be used in place of `path` when it is
not relevant. If `path` is `=` then the the `value` is cached and used
for subsequent tests in the calling and all child processes. Only
`writable` variables may be set; `readonly` variables cannot be
changed.

The current value for `name` is written to the standard output. If
`name` is valid but undefined then `undefined` is written to the
standard output. If `name` is invalid or an error occurs in determining
its value, then a diagnostic written to the standard error and
`getconf` exits with a non-zero exit status.

More than one variable may be set or queried by providing the `name`
`path` `value` 3-tuple for each variable, specifying `-` for `value`
when querying.

If no operands are specified then all known variables are written in
`name`=`value` form to the standard output, one per line. Only one of
`--call`, `--name` or `--standard` may be specified.

This implementation uses the
[`astgetconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man3/astgetconf.html)(3)
string interface to the native
[`sysconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/sysconf.html)(2),
[`confstr`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/confstr.html)(2),
[`pathconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/pathconf.html)(2),
and
[`sysinfo`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/sysinfo.html)(2)
system calls. If `getconf` on `\$PATH` is not the default native
`getconf`, named by `\$(getconf GETCONF)`, then
[`astgetconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man3/astgetconf.html)(3)
checks only `ast` specific extensions and the native system calls;
invalid options and/or names not supported by
[`astgetconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man3/astgetconf.html)(3)
cause the `getconf` on `\$PATH` to be executed.

# OPTIONS

-`a`, --`all`
: Call the native
    [`getconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man1/getconf.html)(1)
    with option `-a`.

-`b`, --`base`
: List base variable name sans call and standard prefixes.

-`c`, --`call`=`RE`
: Display variables with call prefix that matches `RE`. The call
    prefixes are:

    [`CS`]()
    : [`confstr`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/confstr.html)(2)

    [`PC`]()
    : [`pathconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/pathconf.html)(2)

    [`SC`]()
    : [`sysconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/sysconf.html)(2)

    [`SI`]()
    : [`sysinfo`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/sysinfo.html)(2)

    [`XX`]()
    : Constant value.

-`d`, --`defined`

Only display defined values when no operands are specified.

-`l`, --`lowercase`

List variable names in lower case.

-`n`, --`name`=`RE`

Display variables with name that match `RE`.

-`p`, --`portable`

Display the named `writable` variables and values in a form that can
be directly executed by
[`sh`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man1/sh.html)(1)
to set the values. If `name` is omitted then all `writable` variables
are listed.

-`q`, --`quote`

"..." quote values.

-`r`, --`readonly`

Display the named `readonly` variables in `name`=`value` form. If
`name` is omitted then all `readonly` variables are listed.

-`s`, --`standard`=`RE`

Display variables with standard prefix that matches `RE`. Use the
`--table` option to view all standard prefixes, including local
additions. The standard prefixes available on all systems are:

[`AES`]()

[`AST`]()

[`C`]()

[`GNU`]()

[`POSIX`]()

[`SVID`]()

[`XBS5`]()

[`XOPEN`]()

[`XPG`]()

-`t`, --`table`

Display the internal table that contains the name, standard, standard
section, and system call symbol prefix for each variable.

-`w`, --`writable`

Display the named `writable` variables in `name`=`value` form. If
`name` is omitted then all `writable` variables are listed.

-`v`, --`specification`=`name`

Call the native
[`getconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man1/getconf.html)(1)
with option `-v` `name`.

# ENVIRONMENT

`\_AST\_FEATURES`
: Process local writable values that are different from the default
    are stored in the `\_AST\_FEATURES` environment variable. The
    `\_AST\_FEATURES` value is a space-separated list of `name` `path`
    `value` 3-tuples, where `name` is the system configuration name,
    `path` is the corresponding path, `-` if no path is applicable,
    and `value` is the system configuration value.

# SEE ALSO

[`pathchk`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man1/pathchk.html)(1),
[`confstr`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/confstr.html)(2),
[`pathconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/pathconf.html)(2),
[`sysconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man2/sysconf.html)(2),
[`astgetconf`](/web/20150530235509/http://www2.research.att.com:80/~astopen/man/man3/astgetconf.html)(3)

# IMPLEMENTATION

`version`
: getconf (AT&T Research) 2008-04-24

`author`
: Glenn Fowler

`author`
: David Korn

`copyright`
: Copyright © 1992-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20150530235509/http://www.opensource.org/licenses/cpl1.0.txt)


