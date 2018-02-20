# NAME

ln - link files

# SYNOPSIS

`ln` \[ `options` \] source destination\

`ln` \[ `options` \] file ... directory

# DESCRIPTION

If the last argument names an existing directory, `ln` links each
`file` into a file with the same name in that directory. Otherwise, if
only two files are given, `ln` links the first onto the second. It is
an error if the last argument is not a directory and more than two files
are given. By default directories are not linked.

# OPTIONS

-`f`, --`force`
: Replace existing destination files.

-`i`, --`interactive|prompt`
: Prompt whether to replace existing destination files. An affirmative
    response (`y` or `Y`) replaces the file, a quit response (`q`
    or `Q`) exits immediately, and all other responses skip the file.

-`r|R`, --`recursive`
: Operate on the contents of directories recursively.

-`s`, --`symlink|symbolic-link`
: Make symbolic links to destination files.

-`u`, --`update`
: Replace a destination file only if its modification time is older
    than the corresponding source file modification time.

-`v`, --`verbose`
: Print the name of each file before operating on it.

-`b`, --`backup`
: Make backups of files that are about to be replaced. See
    `--suffix` and `--version-control` for more information.

-`F`, --`fsync|sync`
: [`fsync`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/fsync.html)(2)
    each file after it is copied.

-`S`, --`backup-suffix|suffix`=`suffix`
: A backup file is made by renaming the file to the same name with the
    backup suffix appended. The backup suffix is determined in this
    order: this option, the `SIMPLE\_BACKUP\_SUFFIX` , environment
    variable, or the default value `\~`.

-`V`, --`backup-type|version-control`=`type`
: The backup type is determined in this order: this option, the
    `VERSION\_CONTROL` environment variable, or the default value
    `existing`. `type` may be one of:

    [`numbered|t`]()
    : Always make numbered backups. The numbered backup suffix is
        `.` `SNS`, where `S` is the `backup-suffix` and `N` is the
        version number, starting at 1, incremented with each version.

    [`existing|nil`]()
    : Make numbered backups of files that already have them, otherwise
        simple backups.

    [`simple|never`]()
    : Always make simple backups.

-`x|X|l`, --`xdev|local|mount|one-file-system`

Do not descend into directories in different filesystems than their
parents.

# SEE ALSO

[`pax`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man1/pax.html)(1),
[`fsync`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/fsync.html)(2),
[`rename`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/rename.html)(2),
[`unlink`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man2/unlink.html)(2),
[`remove`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man3/remove.html)(3)

# IMPLEMENTATION

`version`
: cp (AT&T Research) 2010-01-20

`author`
: Glenn Fowler

`author`
: David Korn

`copyright`
: Copyright © 1992-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030245/http://www.opensource.org/licenses/cpl1.0.txt)


