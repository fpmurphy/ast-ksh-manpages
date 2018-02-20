# NAME

updatedb - generate locate pathname database

# SYNOPSIS

`updatedb` \[ `options` \]

# DESCRIPTION

`updatedb` generates the locate pathname database that is used by
[`locate`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/locate.html)(1),
[`find`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/find.html)(1),
and
[`tw`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/tw.html)(1).
Sufficient privilege is required to change the system locate database.
This implemenation is a script that generates a
[`tw`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/tw.html)(1)
command that does all the work.

# OPTIONS

-`a`, --`auto-home`
:   Include the
    [`nis`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/nis.html)(1)
    `auto.home` auto mounter home directories in `/home`. NOTE: this
    causes the home directories to be mounted and may swamp the
    mount table.

-`d`, --`directory|localpaths`=`"dir1 dir2 ..."`
:   Local directories to include in the database. If the first `dir` is
    `+` then the default list is appended. The default value is `/`.

-`i`, --`ignore-errors`
:   Omit inaccessible files and directory error messages.

-`k`, --`keep`=`"dir1 dir2 ..."`
:   Directories to retain in the database; used to override
    `--nocrossdevice`. If any of the paths are symbolic links then
    they are followed. If the first `dir` is `+` then the default list
    is appended. The default value is `/home /usr/local /usr/common`.

-`l`, --`local`
:   Do not descend into non-local filesystem directories.

-`r`, --`netpaths`=`"dir1 dir2 ..."`
:   Network directories to include in the database. Currently equivalent
    to `--localpaths`.

-`p`, --`prunepaths|drop`=`"dir1 dir2 ..."`
:   Directories to exclude from the database. If the first `dir` is
    `+` then the default list is appended. The default value is `/afs
    /backup /dev /proc /tmp /usr/tmp /var/tmp`.

-`o`, --`output|codes`=`dbfile`
:   The path of the generated database. The default value is
    `lib/find/codes` .

-`P`, --`public`
:   Omit files that are not publicly readable and directories that are
    not publicly searchable.

-`u`, --`user|netuser`=`user`
:   The user id used to search directories.

-`m`, --`dir-format`
:   Generate a database similar to `--gnu-format`, except that
    directories are marked for efficient implementations of
    [`find`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/find.html)(1)
    and
    [`tw`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/tw.html)(1).
    This is the default database format.

-`g`, --`gnu-format`
:   Generate a machine independent gnu
    [`locate`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/locate.html)(1)
    compatible database.

-`O`, --`old-format`
:   Generate a database compatible with the obsolete
    [`fastfind`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/fastfind.html)(1).
    This format has a machine dependent encoding.

-`D`, --`depth`=`level`
:   Limit the directory traversal depth to `level`.

-`X`, --`crossdevice`
:   Retain subdirectories that cross device boundaries. On by default;
    -`X` means --`nocrossdevice`.

-`n`, --`show`
:   Show the underlying the
    [`tw`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/tw.html)(1)
    command but do not execute.

# FILES

`lib/find/codes`
:   Default locate database on `\$PATH`.

# CAVEATS

If you run `updatedb` as root then protected directory contents may be
visible to everyone via the database. Use the `--public` option to
limit the database to publically visible files and directories.

# SEE ALSO

[`locate`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/locate.html)(1),
[`fastfind`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/fastfind.html)(1),
[`find`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/find.html)(1),
[`nis`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/nis.html)(1),
[`tw`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/tw.html)(1)

# IMPLEMENTATION

`version`
:   updatedb (AT&T Labs Research) 2003-11-14

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030253/http://www.eclipse.org/org/documents/epl-v10.html)


