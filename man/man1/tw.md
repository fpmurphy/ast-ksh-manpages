# NAME

tw - file tree walk

# SYNOPSIS

`tw` \[ `options` \] \[ cmd \[ arg ... \] \]

# DESCRIPTION

`tw` recursively descends the file tree rooted at the current
directory and lists the pathname of each file found. If `cmd arg ...` is
specified then the pathnames are collected and appended to the end of
the `arg`list and `cmd` is executed by the equivalent of
[`execvp`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man2/execvp.html)(2).
`cmd` will be executed 0 or more times, depending the number of
generated pathname arguments.
If the last option is `-` and `--fast` was not specified then the
pathnames are read, one per line, from the standard input, the
`--directory` options are ignored, and the directory tree is not
traversed.

`getconf PATH\_RESOLVE` determines how symbolic links are handled.
This can be explicitly overridden by the `--logical`,
`--metaphysical`, and `--physical` options below. `PATH\_RESOLVE`
can be one of:

`logical`
:   Follow all symbolic links.

`metaphysical`
:   Follow command argument symbolic links, otherwise don't follow.

`physical`
:   Don't follow symbolic links.

# OPTIONS

-`a`, --`arg-list`=`string`
:   The first `arg` named `string` is replaced by the current pathname
    list before `cmd` is executed.

-`c`, --`args|arg-count`=`count`
:   `cmd` is executed after `count` arguments are collected.

-`d`, --`directory`=`dir`
:   The file tree traversal is rooted at `dir`. Multiple `--directory`
    directories are traversed in order from left to right. If the last
    option was `-` then all `--directory` are ignored.

-`e`, --`expr`=`expr`
:   `expr` defines expression functions that control tree traversal.
    Multiple `--expr` expressions are parsed in order from left
    to right. See EXPRESSIONS below for details.

-`f`, --`fast`=`pattern`
:   Searches the
    [`find`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/find.html)(1)
    or
    [`locate`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/locate.html)(1)
    database for paths matching the
    [`ksh`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/ksh.html)(1)
    `pattern`. See
    [`updatedb`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/updatedb.html)(1)
    for details on this database. Any `--expr` expressions are applied
    to the matching paths.

-`i`, --`ignore-errors`
:   Ignore inaccessible files and directories.

-`I`, --`ignore-case`
:   Ignore case in pathname comparisons.

-`l`, --`local`
:   Do not descend into non-local filesystem directories.

-`m`, --`intermediate`
:   Before visiting a selected file select and visit intermediate
    directories leading to the file that have not already been selected.

-`n`, --`notraverse`
:   Evaluate the `begin`, `select` and `end` expressions but
    eliminate the tree traversal.

-`p`, --`post`
:   Visit each directory after its files have been processed. By default
    directories are visited pre-order.

-`q`, --`query`
:   Emit an interactive query for each visited path. An affirmative
    response accepts the path, a negative response rejects the path, and
    a quit response exits `tw`.

-`r`, --`recursive`
:   Visit directories listed on the standard input.

-`S`, --`separator`=`string`
:   The input file list separator is set to the first character of
    `string`.

-`s`, --`size|max-chars`=`chars`
:   Use at most `chars` characters per command. The default is as large
    as possible.

-`t`, --`trace|verbose`
:   Print the command line on the standard error before executing it.

-`x`, --`error-exit`=`code`
:   Exit `tw` with the exit code of the first `cmd` that returns an
    exit code greater than or equal to `code`. By default `cmd` exit
    codes are ignored (mostly because of
    [`grep`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/grep.html)(1).)

-`z`, --`snapshot`
:   Write a snapshot of the selected files to the standard output. For
    the first snapshot the standard input must either be empty or a
    single line containing delimiter separated output format fields,
    with the delimiter appearing as both the first and last character.
    The format is in the same style as
    [`ls`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/ls.html)(1)
    and
    [`ps`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/ps.html)(1)
    formats: %(`identifier` )`printf-format`, where `identifier` is one
    of the file status identifiers described below, and `printf-format`
    is a
    [`printf`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man3/printf.html)(3)
    format specification. A default delimiter ("|") and field values are
    assumed for an empty snapshot input file. The format fields are:

    [`snapshot`]()
    : \
        The literal string `snapshot`.

    [`path-format`]()
    : \
        The current path format, default "%(url)s".

    [`easy-format`]()
    : \
        The `easy` part of the snapshot file state,
        default "%(ctime)..64u,%(perm)..64u,%(size)..64u,%(uid)..64u,%(gid)..64u".
        This part is recomputed for each file.

    [`hard-format`]()
    : \
        The `hard` part of the snapshot file state,
        default "%(md5sum)s". This part is computed only if the easy
        part has changed.

    [`change-status`]()
    : \
        This field, with both a leading and trailing delimiter, is
        ignored on input and set to one of the following values for
        files that have changed since the last snapshot:

        [`C`]()
        : The file changed.

        [`D`]()
        : The file was deleted.

        [`N`]()
        : The file is new.

-`C`, --`chop`
:   Chop leading `./` from printed pathnames. This is implied by
    `--logical`.

-`E`, --`file`=`file`
:   Compile `--expr` expressions from `file`. Multiple `--file`
    options may be specified. See EXPRESSIONS below for details.

-`F`, --`codes`=`path`
:   Set the
    [`locate`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/locate.html)(1)
    fast find codes database `path`.

-`G`, --`generate`=`format`
:   Generate a `format`
    [`locate`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/locate.html)(1)
    database of the visited files and directories. Exit status 1 means
    some files were not accessible but the database was properly
    generated; exit status 2 means that database was not generated.
    Format may be:

    [`dir`]()
    : machine independent with directory trailing /.

    [`old`]()
    : old fast find

    [`gnu`]()
    : gnu
        [`locate`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/locate.html)(1)

    [`type`]()
    : machine independent with directory and mime types

-`L`, --`logical|follow`
:   Follow symbolic links. The default is determined by `getconf
    PATH\_RESOLVE`.

-`H`, --`metaphysical`
:   Follow command argument symbolic links, otherwise don't follow. The
    default is determined by `getconf PATH\_RESOLVE`.

-`P`, --`physical`
:   Don't follow symbolic links. The default is determined by `getconf
    PATH\_RESOLVE`.

-`X`, --`xdev|mount`
:   Do not descend into directories in different filesystems than
    their parents.

-`D`, --`debug`=`level`
:   Set the debug trace `level`; higher levels produce more output.

# EXPRESSIONS

Expressions are C style and operate on elements of the
[`stat`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man2/stat.html)(2)
struct with the leading `st\_` omitted. A function expression is
defined by one of: function-name : statement-list type function-name() {
statement-list }
where `function-name` is one of:

`begin`
:   Evaluated before the traversal starts. The return value is ignored.
    The default is a no-op.

`select`
:   Evaluated as each file is visited. A 0 return value skips `action`
    for the file; otherwise `action` is evaluated. All files are
    selected by default. `select` is assumed when `function-name`:
    is omitted.

`action`
:   Evaluated for each select file. The return value is ignored. The
    default `action` list the file path name, with leading `./`
    stripped, one per line on the standard output.

`end`
: Evaluated after the traversal completes. The return value
    is ignored.

`sort`
: A pseudo-function: the statement list is a , separated list of
    identifiers used to sort the entries of each directory. If any
    identifier is preceded by `!` then the sort order is reversed. If
    any identifier is preceded by `\~` then case is ignored.

`statement-list` is a C style
[`expr`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man3/expr.html)(3)
expression that supports: `int` `var`, ...; and `float` `var`, ...;
declarations, `(int)` and `(float)` casts, `if`-`else`
conditionals, `for` and `while` loops, and `{...}` blocks. The
trailing `;` in any expression list is optional. The expression value
is the value of the last evaluated expression in `statement-list`.
Numbers and comments follow C syntax. String operands must be quoted
with either `"..."` or `'...'`. String comparisons `==` and `!=`
treat the right hand operand as a
[`ksh`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/ksh.html)(1)
file match pattern.
The expressions operate on the current pathname file status that is
provided by the following field identifiers, most of which are described
under `st\_``field` in
[`stat`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man2/stat.html)(2).
In general, if a status identifier appears on the left hand side of a
binary operator then the right hand side may be a string that is
converted to an integral constant according to the identifier semantics.

`atime`
:   access time; time/date strings are interpreted as
    [`date`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/date.html)(1)
    expressions

`blocks`
:   number of 1k blocks

`checksum`
:   equivalent to `sum("tw")`

`ctime`
:   status change time

`dev`
: file system device

`fstype`
:   file system type name; `ufs` if it can't be determined

`gid`
: owner group id; `gid` strings are interpreted as group names

`gidok`
:   1 if `gid` is a valid group id in the system database, 0 otherwise.

`ino`
: inode/serial number

`level`
:   the depth of the file relative to the traversal root

`local`
:   an integer valued field associated with each active object in the
    traversal; This field may be assigned. The initial value is 0.
    Multiple `local` elements may be declared by
    `int local.``element1`...;. In this case the `local` field
    itself is not accessible.

`md5sum`
:   equivalent to `sum("md5")`

`mime`
: the file contents
    [`file`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/file.html)(1)
    `--mime` type

`mode`
: type and permission bits; the `FMT` constant may be used to mask
    mask the file type and permission bits; `mode` strings are
    interpreted as
    [`chmod`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/chmod.html)(1)
    expressions

`mtime`
:   modify time

`name`
: file name with directory prefix stripped

`nlink`
:   hard link count

`path`
: full path name relative to the current active `--directory`

`perm`
: the permission bits of `mode`

`rdev`
: the major.minor device number if the file is a device

`size`
: size in bytes

`status`
:   the
    [`fts`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man3/fts.html)(3)
    `FTS\_`\` or
    [`ftwalk`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man3/ftwalk.html)(3)
    `FTW\_`\` status. This field may be assigned:

    [`AGAIN`]()
    : \
        visit the file again

    [`FOLLOW`]()
    : \
        if the file is a symbolic link then follow it

    [`NOPOST`]()
    : \
        cancel any post order visit to this file

    [`SKIP`]()
    : do not consider this file or any subdirectories if it is a
        directory

`sum`("`method`")
:   file contents checksum using `method`; see
    [`sum`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/sum.html)(1)
    `--method` for details.

`symlink`
:   the symbolic link text if the file is a symbolic link

`type`
: the type bits of `mode`:

    [`BLK`]()
    : block special

    [`CHR`]()
    : block special

    [`DIR`]()
    : directory

    [`DOOR`]()
    : door

    [`FIFO`]()
    : fifo

    [`LNK`]()
    : symbolic link

    [`REG`]()
    : regular

    [`SOCK`]()
    : unix domain socket

`uid`
: owner user id; `uid` strings are interpreted as user names

`uidok`
:   1 if `uid` is a valid user id in the system database, 0 otherwise.

`url`
: unprintable chars n path converted to %XX hex

`visit`
:   an integer variable associated with each unique object visited;
    Objects are identified using the `dev` and `ino`
    status identifiers. This field may be assigned. The initial value
    is 0. Multiple `visit` elements may be declared by `int visit.`
    `element`...;. In this case the `visit` field itself is
    not accessible.

Status identifiers may be prefixed by 1 or more `parent.` references,
to access ancestor directory information. The parent status information
of a top level object is the same as the object except that `name` and
`path` are undefined. If a status identifier is immediately preceded
by `"string"`. then string is a file pathname from which the status is
taken.
The following
[`expr`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man3/expr.html)(3)
functions are supported:

`exit`(expr)
:   causes `tw` to exit with the exit code `expr` which defaults to 0 if
    omitted

`printf`(format\[,arg...\])
:   print the arguments on the standard output using the
    [`printf`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man3/printf.html)(3)
    specification `format`.

`eprintf`(format\[,arg...\])
:   print the arguments on the standard error using the
    [`printf`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man3/printf.html)(3)
    specification `format`.

`query`(format\[,arg...\])
:   prompt with the
    [`printf`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man3/printf.html)(3)
    message on the standard error an read an interactive response. An
    affirmative response returns 1, `q` or `EOF` causes `tw` to to
    exit immediately, and any other input returns 0.

# EXAMPLES

`tw`
: Lists the current directory tree.

`tw chmod go-w`
:   Turns off the group and other write permissions for all files in the
    current directory tree using a minimal amount of
    [`chmod`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/chmod.html)(1)
    command execs.

`tw -e "uid != 'bozo' ||` (mode & 'go=w')"
:   Lists all files in the current directory that don't belong to the
    user `bozo` or have group or other write permission.

`tw -m -d / -e "fstype == '/'.fstype && mtime &gt; '/etc/backup.time'.mtime"`
:   Lists all files and intermediate directories on the same file system
    type as `/` that are newer than the file `/etc/backup.time`.

`tw - chmod +x &lt; commands`
:   Executes `chmod +x` on the pathnames listed in the file
    `commands`.

`tw -e "int count;`
:   `action: count++; printf('name=%s inode=%08ld\\\\n', name, ino);
    end: printf('%d file%s\\\\n', count, count==1 ? '' : 's');"` Lists
    the name and inode number of each file and also the total number
    of files.

`tw -pP -e "`
:   `action: if (visit++ == 0) { parent.local += local + blocks; if
    (type == DIR) printf('%d\\\\t%s\\\\n', local + blocks, path); }"`
    Exercise for the reader.

# EXIT STATUS

`0`
: All invocations of `cmd` returned exit status 0.

`1-125`
:   A command line meeting the specified requirements could not be
    assembled, one or more of the invocations of `cmd` returned non-0
    exit status, or some other error occurred.

`126`
: `cmd` was found but could not be executed.

`127`
: `cmd` was not found.

# ENVIRONMENT

`FINDCODES`
:   Path name of the
    [`locate`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/locate.html)(1) database.

`LOCATE\_PATH`
:   Alternate path name of
    [`locate`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/locate.html)(1) database.

# FILES

`lib/find/find.codes`
:   Default
    [`locate`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/locate.html)(1) database.

# NOTES

In order to access the
[`slocate`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/slocate.html)(1)
database the `tw` executable must be setgid to the `slocate` group.

# SEE ALSO

[`find`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/find.html)(1),
[`getconf`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/getconf.html)(1),
[`locate`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/locate.html)(1),
[`slocate`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/slocate.html)(1),
[`sum`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/sum.html)(1),
[`updatedb`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/updatedb.html)(1),
[`xargs`](/web/20150530235520/http://www2.research.att.com:80/~astopen/man/man1/xargs.html)(1)

# IMPLEMENTATION

`version`
:   tw (AT&T Research) 2012-04-11

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150530235520/http://www.eclipse.org/org/documents/epl-v10.html)


