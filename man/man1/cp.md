# NAME

cp - copy files

# SYNOPSIS

`cp` \[ `options` \] source destination\
`cp` \[ `options` \] file ... directory

# DESCRIPTION

If the last argument names an existing directory, `cp` copies each
`file` into a file with the same name in that directory. Otherwise, if
only two files are given, `cp` copies the first onto the second. It is
an error if the last argument is not a directory and more than two files
are given. By default directories are not copied.

# OPTIONS

-`a`, --`archive`
:   Preserve as much as possible of the structure and attributes of the
    original files in the copy. Equivalent to `--physical`
    `--preserve` `--recursive`.

-`A`, --`attributes`=`eipt`
:   Preserve selected file attributes:

    [`e`]()
    : Everything permissible.

    [`i`]()
    : Owner uid and gid.

    [`p`]()
    : Permissions.

    [`t`]()
    : Access and modify times.

-`p`, --`preserve`
:   Preserve file owner, group, permissions and timestamps.

-`h`, --`hierarchy|parents`
:   Form the name of each destination file by appending to the target
    directory a slash and the specified source file name. The last
    argument must be an existing directory. Missing destination
    directories are created.

-`H`, --`metaphysical`
:   Follow command argument symbolic links, otherwise don't follow.

-`l`, --`link`
:   Make hard links to destination files instead of copies.

-`U`, --`remove-destination`
:   Remove existing destination files before copying.

-`L`, --`logical|dereference`
:   Follow symbolic links and copy the files they point to.

-`P|d`, --`physical|nodereference`
:   Don't follow symbolic links; copy symbolic rather than the files
    they point to.

-`f`, --`force`
:   Replace existing destination files.

-`i`, --`interactive|prompt`
:   Prompt whether to replace existing destination files. An affirmative
    response (`y` or `Y`) replaces the file, a quit response (`q`
    or `Q`) exits immediately, and all other responses skip the file.

-`r|R`, --`recursive`
:   Operate on the contents of directories recursively.

-`s`, --`symlink|symbolic-link`
:   Make symbolic links to destination files.

-`u`, --`update`
:   Replace a destination file only if its modification time is older
    than the corresponding source file modification time.

-`v`, --`verbose`
:   Print the name of each file before operating on it.

-`F`, --`fsync|sync`
:   [`fsync`](/web/20150817032506/http://www2.research.att.com:80/~astopen/man/man2/fsync.html)(2)
    each file after it is copied.

-`B`, --`backup`\[=`type`\]
:   Make backups of files that are about to be replaced. `--suffix`
    sets the backup suffix. The backup type is determined in this order:
    this option, the `VERSION\_CONTROL` environment variable, or the
    default value `existing`. `type` may be one of:

    [`numbered|t`]()
    : \
        Always make numbered backups. The numbered backup suffix is
        `.``SNS`, where `S` is the `backup-suffix` and `N` is the
        version number, starting at 1, incremented with each version.

    [`existing|nil`]()
    : \
        Make numbered backups of files that already have them, otherwise
        simple backups.

    [`simple|never`]()
    : \
        Always make simple backups.

    [`none|off`]()
    : \
        Disable backups.

The option value may be omitted.\
-`S`, --`suffix`=`suffix`
:   A backup file is made by renaming the file to the same name with the
    backup suffix appended. The backup suffix is determined in this
    order: this option, the `SIMPLE\_BACKUP\_SUFFIX`, environment
    variable, or the default value `\~`.

-`b`
: `--backup` using the type in the `VERSION\_CONTROL`
    environment variable.

-`x|X`, --`xdev|local|mount|one-file-system`
:   Do not descend into directories in different filesystems than
    their parents.

# SEE ALSO

[`pax`](/web/20150817032506/http://www2.research.att.com:80/~astopen/man/man1/pax.html)(1),
[`fsync`](/web/20150817032506/http://www2.research.att.com:80/~astopen/man/man2/fsync.html)(2),
[`rename`](/web/20150817032506/http://www2.research.att.com:80/~astopen/man/man2/rename.html)(2),
[`unlink`](/web/20150817032506/http://www2.research.att.com:80/~astopen/man/man2/unlink.html)(2),
[`remove`](/web/20150817032506/http://www2.research.att.com:80/~astopen/man/man3/remove.html)(3)

# IMPLEMENTATION

`version`
:   cp (AT&T Research) 2012-04-20

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150817032506/http://www.eclipse.org/org/documents/epl-v10.html)


