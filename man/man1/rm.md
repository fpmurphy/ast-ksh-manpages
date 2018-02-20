# NAME

rm - remove files

# SYNOPSIS

`rm` \[ `options` \] file ...

# DESCRIPTION

`rm` removes the named `file` arguments. By default it does not remove
directories. If a file is unwritable, the standard input is a terminal,
and the `--force` option is not given, `rm` prompts the user for
whether to remove the file. An affirmative response (`y` or `Y`)
removes the file, a quit response (`q` or `Q`) causes `rm` to exit
immediately, and all other responses skip the current file.

# OPTIONS

-`c|F`, --`clear|clobber`
:   Clear the contents of each file before removing by writing a 0
    filled buffer the same size as the file, executing
    [`fsync`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man2/fsync.html)(2)
    and closing before attempting to remove. Implemented only on systems
    that support
    [`fsync`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man2/fsync.html)(2).

-`d`, --`directory`
:   [`remove`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man3/remove.html)(3)
    (or
    [`unlink`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man2/unlink.html)(2))
    directories rather than
    [`rmdir`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man2/rmdir.html)(2),
    and don't require that they be empty before removal. The caller
    requires sufficient privilege, not to mention a strong constitution,
    to use this option. Even though the directory must not be empty,
    `rm` still attempts to empty it before removal.

-`f`, --`force`
:   Ignore nonexistent files, ignore no file operands specified, and
    never prompt the user.

-`i`, --`interactive|prompt`
:   Prompt whether to remove each file. An affirmative response (`y`
    or `Y`) removes the file, a quit response (`q` or `Q`) causes
    `rm` to exit immediately, and all other responses skip the
    current file.

-`r|R`, --`recursive`
:   Remove the contents of directories recursively.

-`u`, --`unconditional`
:   If `--recursive` and `--force` are also enabled then the owner
    read, write and execute modes are enabled (if not already enabled)
    for each directory before attempting to remove directory contents.

-`v`, --`verbose`
:   Print the name of each file before removing it.

# SEE ALSO

[`mv`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/mv.html)(1),
[`rmdir`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man2/rmdir.html)(2),
[`unlink`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man2/unlink.html)(2),
[`remove`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man3/remove.html)(3)

# IMPLEMENTATION

`version`
:   rm (AT&T Research) 2012-02-14

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030250/http://www.eclipse.org/org/documents/epl-v10.html)


