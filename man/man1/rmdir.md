# NAME

rmdir - remove empty directories

# SYNOPSIS

`rmdir` \[ `options` \] directory ...

# DESCRIPTION

`rmdir` deletes each given directory. The directory must be empty;
containing no entries other than `.` or `..`. If a directory and a
subdirectory of that directory are specified as operands, the
subdirectory must be specified before the parent so that the parent
directory will be empty when `rmdir` attempts to remove it.

# OPTIONS

-`e`, --`ignore-fail-on-non-empty`
:   Ignore each non-empty directory failure.

-`p`, --`parents`
:   Remove each explicit `directory` argument directory that becomes
    empty after its child directories are removed.

-`s`, --`suppress`
:   Suppress the message printed on the standard error when `-p` is
    in effect.

# EXIT STATUS

`0`
: All directories deleted successfully.

`&gt;0`
:   One or more directories could not be deleted.

# SEE ALSO

[`mkdir`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/mkdir.html)(1),
[`rm`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/rm.html)(1),
[`rmdir`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man2/rmdir.html)(2),
[`unlink`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man2/unlink.html)(2)

# IMPLEMENTATION

`version`
:   rmdir (AT&T Research) 2006-08-24

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030249/http://www.eclipse.org/org/documents/epl-v10.html)


