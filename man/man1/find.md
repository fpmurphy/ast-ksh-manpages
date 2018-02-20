# NAME

find - find files

# SYNOPSIS

`find` \[ `options` \] \[ path ... \] \[ options \]

# DESCRIPTION

`find` recursively descends the directory hierarchy for each `path`
and applies an `option` expression to each file in the hierarchy.
`-print` is implied if there is no action that generates output. The
expression starts with the first argument that matches \[(-!\]. Option
expressions may occur before and/or after the `path` arguments. For
numeric arguments `n` , `+n` means `&gt;n`, `-n` means `&lt;n`, and `n`
means exactly `n`.

# OPTIONS

-`begin`
:   Equivalent to \\(. Begin nested expression.

-`end`
: Equivalent to \\). End nested expression.

-`a|and`
:   Equivalent to \`\\&'. `expr1` `-and` `expr2`: Both `expr1` and
    `expr2` must evaluate `true`. This is the default operator for two
    expression in sequence.

-`amin` `minutes`
:   File was last accessed `minutes` minutes ago.

-`anewer` `file`
:   File was last accessed more recently than `file` was modified.

-`atime` `days`
:   File was last accessed `days` days ago.

-`check`
:   Turns off `-silent`; enables inaccessible file and
    directory warnings. This is the default.

-`chop`
:   Chop leading `./` from printed pathnames.

-`cmin` `minutes`
:   File status changed `minutes` minutes ago.

-`cnewer` `file`
:   File status changed more recently than `file` was modified.

-`codes` `path`
:   Sets the `find` or
    [`locate`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/locate.html)(1)
    database `path`. See
    [`updatedb`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/updatedb.html)(1)
    for a description of this database.

-`comma`
:   Equivalent to \`,'. Joins two expressions; the status of the first
    is ignored.

-`cpio`
:   File is written as a binary format
    [`cpio`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/cpio.html)(1)
    file entry.

-`ctime` `days`
:   File status changed `days` days ago.

-`daystart`
:   Measure times (-amin -atime -cmin -ctime -mmin -mtime) from the
    beginning of today. The default is 24 hours ago.

-`depth`
:   Process directory contents before the directory itself.

-`empty`
:   A directory with size 0 or with no entries other than . or .., or a
    regular file with size 0.

-`exec` `command ... ; | command ... {} +`
:   Execute `command ...`; true if 0 exit status is returned. Arguments
    up to `;` are taken as arguments to `command`. The string \`{}' in
    `command ...` is globally replaced by the current filename. The
    command is executed in the directory from which `find`
    was executed. The second form gathers pathnames until `ARG\_MAX`
    is reached, replaces {} preceding `+` with the list of pathnames,
    one pathname per argument, and executes `command` ... `pathname`
    ..., possibly multiple times, until all pathnames are exhausted.

-`false`
:   Always false.

-`fast` `pattern`
:   Searches the `find` or
    [`locate`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/locate.html)(1)
    database for paths matching the
    [`ksh`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    `pattern`. See
    [`updatedb`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/updatedb.html)(1)
    for details on this database. The command line arguments limit the
    search and the expression, but all depth options are ignored. The
    remainder of the expression is applied to the matching paths.

-`fls` `file`
:   Like -ls except the output is written to `file`.

-`fprint` `file`
:   Like -print except the output is written to `file`.

-`fprint0` `file`
:   Like -print0 except the output is written to `file`.

-`fprintf` `file format`
:   Like -printf except the output is written to `file`.

-`fprintx` `file`
:   Like -printx except the output is written to `file`.

-`fstype` `type`
:   File is on a filesystem `type`. See
    [`df`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/df.html)(1)
    or `-printf %F` for local filesystem type names.

-`group|gid` `id`
:   File group id name or number matches `id`.

-`ignorecase`
:   Ignore case in all pattern match expressions.

-`ilname` `pattern`
:   A case-insensitive version of `-lname` `pattern`.

-`iname` `pattern`
:   A case-insensitive version of `-name` `pattern`.

-`inum` `number`
:   File has inode number `number`.

-`ipath` `pattern`
:   A case-insensitive version of `-path` `pattern`.

-`iregex` `pattern`
:   A case-insensitive version of `-regex` `pattern`.

-`level` `level`
:   Current level (depth) is `level`.

-`links` `number`
:   File has `number` links.

-`lname` `pattern`
:   File is a symbolic link with text that matches `pattern`.

-`local`
:   File is on a local filesystem.

-`logical|follow|L`
:   Follow symbolic links.

-`ls`
: List the current file in \`ls -dils' format to the standard output.

-`magic` `pattern`
:   File magic number matches the
    [`file`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/file.html)(1)
    and
    [`magic`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man3/magic.html)(3)
    description `pattern`.

-`maxdepth` `level`
:   Descend at most `level` directory levels below the command
    line arguments. `-maxdepth 0` limits the search to the command
    line arguments.

-`metaphysical|H`
:   `-logical` for command line arguments, `-physical` otherwise.

-`mime` `type/subtype`
:   File mime type matches the pattern `type/subtype`.

-`mindepth` `level`
:   Do not apply tests or actions a levels less than `level`.
    `-mindepth 1` processes all but the command line arguments.

-`mmin` `minutes`
:   File was modified `minutes` minutes ago.

-`mount|x|xdev|X`
:   Do not descend into directories in different filesystems than
    their parents.

-`mtime` `days`
:   File was modified `days` days ago.

-`name` `pattern`
:   File base name (no directory components) matches `pattern`.

-`ncpio`
:   File is written as a character format
    [`cpio`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/cpio.html)(1)
    file entry.

-`newer` `file`
:   File was modified more recently than `file`.

-`nogroup`
:   There is no group name matching the file group id.

-`noleaf`
:   Disable `-physical` leaf file
    [`stat`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man2/stat.html)(2)
    optimizations. Only required on filesystems with . and .. as the
    first entries and link count not equal to 2 plus the number
    of subdirectories.

-`not`
: `-not` `expr`: inverts the truth value of `expr`.

-`nouser`
:   There is no user name matching the file user id.

-`ok` `command ... \\;`
:   Like `-exec` except a prompt is written to the terminal. If the
    response does not match \`\[yY\].\`' then the command is not run and
    false is returned.

-`o|or`
:   Equivalent to \`\\|'. `expr1` `-or` `expr2`: `expr2` is not
    evaluated if `expr1` is true.

-`path` `pattern`
:   File path name (with directory components) matches `pattern`.

-`perm` `mode`
:   File permission bits tests; `mode` may be octal or symbolic as in
    [`chmod`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/chmod.html)(1).
    `mode`: exactly `mode`; `-mode`: all `mode` bits are set; `+mode`:
    at least one of `mode` bits are set.

-`physical|phys|P`
:   Do not follow symbolic links. This is the default.

-`post`
:   Process directories before and and after the contents are processed.

-`print`
:   Print the path name (including directory components) to the standard
    output, followed by a newline.

-`print0`
:   Like `-print`, except that the path is followed by a
    NUL character.

-`printf` `format`
:   Print format `format` on the standard output, interpreting \`\\'
    escapes and \`%' directives.
    [`printf`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
    field width and precision are interpreted as usual, but the
    directive characters have special interpretation. [`----- escape sequences -----`]() [`\\a`]()
: alert [`\\b`]()
: backspace [`\\f`]()
: form feed [`\\n`]()
: newline [`\\t`]()
: horizontal tab [`\\v`]()
: vertical tab [`\\xnn`]()
: hexadecimal character `nn` [`\\nnn`]()
: octal character `nnn` [`----- format directives -----`]()
    [`%%`]()
: literal % [`%a`]()
: access time in
    [`ctime`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man3/ctime.html)(3)
    format [`%Ac`]()
: access time is
    [`strftime`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man3/strftime.html)(3)
    %`c` format [`%b`]()
: file size in 512 byte blocks [`%c`]()
: status change time in
    [`ctime`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man3/ctime.html)(3)
    format [`%Cc`]()
: status change time is
    [`strftime`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man3/strftime.html)(3)
    %`c` format [`%d`]()
: directory tree depth; 0 means command line argument [`%f`]()
: file base name (no directory components) [`%F`]()
: filesystem type name; use this for `-fstype` [`%g`]()
: group name, or numeric group id if no name found [`%G`]()
: numeric group id [`%h`]()
: file directory name (no base component) [`%H`]()
: command line argument under which file is found [`%i`]()
: file inode number [`%k`]()
: file size in kilobytes [`%l`]()
: symbolic link text, empty if not symbolic link [`%m`]()
: permission bits in octal [`%n`]()
: number of hard links [`%p`]()
: full path name [`%P`]()
: file path with command line argument prefix deleted [`%s`]()
: file size in bytes [`%t`]()
: modify time in
    [`ctime`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man3/ctime.html)(3)
    format [`%Tc`]()
: modify time is
    [`strftime`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man3/strftime.html)(3)
    %`c` format [`%u`]()
: user name, or numeric user id if no name found [`%U`]()
: numeric user id [`%x`]()
: %p quoted for
    [`xargs`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/xargs.html)(1)
    [`%X`]()
: %P quoted for
    [`xargs`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/xargs.html)(1)

-`printx`
:   Print the path name (including directory components) to the standard
    output, with
    [`xargs`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/xargs.html)(1)
    special characters preceded by `\\`, followed by a newline.

-`prune`
:   Ignored if `-depth` is given, otherwise do not descend the
    current directory.

-`regex` `pattern`
:   Path name matches the anchored regular expression `pattern`, i.e.,
    leading \^ and traling \$ are implied.

-`reverse`
:   Reverse the `-sort` sense.

-`silent`
:   Do not warn about inaccessible directories or symbolic link loops.

-`size` `number\[bcgkm\]`
:   File size is `number` units (b: 512 byte blocks, c: characters g:
    1024\`1024\`1024 blocks, k: 1024 blocks, m: 1024\`1024 blocks.)
    Sizes are rounded to the next unit.

-`sort` `option`
:   Search each directory in `-option` sort order, e.g., `-name` sorts
    by name, `-size` sorts by size.

-`test` `seconds`
:   Set the current time to `seconds` since the epoch. Other
    implementation defined test modes may also be enabled.

-`true`
:   Always true.

-`type` `type`
:   File type matches `type`:

    [`b`]()
    : block special

    [`c`]()
    : character special

    [`d`]()
    : directory

    [`f`]()
    : regular file

    [`l`]()
    : symbolic link

    [`p`]()
    : named pipe (FIFO)

    [`s`]()
    : socket

    [`C`]()
    : contiguous

    [`D`]()
    : door

-`used` `days`
:   File was accessed `days` days after its status changed.

-`user|uid` `id`
:   File user id matches the name or number `id`.

-`xargs` `command ... \\;`
:   Like `-exec` except as many file args as permitted are appended to
    `command ...` which may be executed 0 or more times depending on the
    number of files found and local system
    [`exec`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man2/exec.html)(2)
    argument limits.

-`xtype` `type`
:   Like `-type`, except if symbolic links are followed, the test is
    applied to the symbolic link itself, otherwise the test is applied
    to the pointed to file. Equivalent to `-type` if no symbolic links
    are involved.

# EXIT STATUS

If no commands were executed (`-exec`, `-xargs`) the exit status is
1 if errors were detected in the directory traversal and 0 if no errors
were ecountered. Otherwise the status is:

`0`
: All `command` executions returned exit status 0.

`1-125`
:   A command line meeting the specified requirements could not be
    assembled, one or more of the invocations of `command` returned
    non-0 exit status, or some other error occurred.

`126`
: `command` was found but could not be executed.

`127`
: `command` was not found.

# ENVIRONMENT

`FINDCODES`
:   Path name of the
    [`locate`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/locate.html)(1) database.

`LOCATE\_PATH`
:   Alternate path name of
    [`locate`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/locate.html)(1) database.

# FILES

`lib/find/codes`
:   Default
    [`locate`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/locate.html)(1) database.

# NOTES

In order to access the
[`slocate`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/slocate.html)(1)
database the `find` executable must be setgid to the `slocate`
group.

# SEE ALSO

[`cpio`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/cpio.html)(1),
[`file`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/file.html)(1),
[`locate`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/locate.html)(1),
[`ls`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/ls.html)(1),
[`sh`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/sh.html)(1),
[`slocate`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/slocate.html)(1),
[`test`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/test.html)(1),
[`tw`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/tw.html)(1),
[`updatedb`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/updatedb.html)(1),
[`xargs`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man1/xargs.html)(1),
[`stat`](/web/20150527150844/http://www2.research.att.com/~astopen/man/man2/stat.html)(2)

# IMPLEMENTATION

`version`
:   find (AT&T Research) 2012-04-11

`author`
:   Glenn Fowler

`author`
:   David Korn

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150527150844/http://www.eclipse.org/org/documents/epl-v10.html)


