# NAME

df - summarize disk free space

# SYNOPSIS

`df` \[ `options` \] \[ file ... \]

# DESCRIPTION

`df` displays the available disk space for the filesystem of each file
argument. If no `file` arguments are given then all mounted filesystems
are displayed.

# OPTIONS

-`b`, --`blockbytes`
:   Measure disk usage in 512 byte blocks. This is the default if
    `getconf CONFORMANCE` is `standard`.

-`D`, --`define`=`key\[=value\]`
:   Define `key` with optional `value`. `value` will be expanded when
    `%(``key``)` is specified in `--format`. `key` may override
    internal `--format` identifiers.

-`e`, --`decimal-scale|thousands`
:   Scale disk usage to powers of 1000.

-`f`, --`format`=`format`
:   Append to the listing format string. The
    [`ls`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man1/ls.html)(1),
    [`pax`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man1/pax.html)(1)
    and
    [`ps`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man1/ps.html)(1)
    commands also have `--format` options in this same style. `format`
    follows
    [`printf`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man3/printf.html)(3)
    conventions, except that
    [`sfio`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man3/sfio.html)(3)
    inline ids are used instead of arguments:
    %\[\#-+\]\[`width`\[.`precis` \[.`base`\]\]\](`id`\[:`subformat`\])`char`. If `\#` is specified
    then the internal width and precision are used. If `base` is
    non-zero and `--posix` is not on then the field values are wrapped
    when they exceed the field width. If `char` is `s` then the string
    form of the item is listed, otherwise the corresponding numeric form
    is listed. If `char` is `q` then the string form of the item is
    \$'...' quoted if it contains space or non-printing characters. If
    `width` is omitted then the default width is assumed. `subformat`
    overrides the default formatting for `id`. Supported `id`s and
    `subformat`s are:

    [`available`]()
    : \
        Unused block count. The title string is `Available` and the
        default width is determined by the `-b`, `-g`, `-k`,
        `-m` and `-n` options.

    [`blocks`]()
    : \
        Total block count. The title string and the default width are
        determined by the `-b`, `-g`, `-k`, `-m` and
        `-n` options.

    [`capacity`]()
    : \
        Percent of total blocks used. The title string is `Capacity`
        and the default width is 4.

    [`filesystem`]()
    : \
        Filesystem special device name. The title string is
        `Filesystem` and the default width is -19.

    [`iavailable`]()
    : \
        Unused inode count. The title string is `Iavailable` and the
        default width is 7.

    [`icapacity`]()
    : \
        Percent of total inodes used. The title string is `Icapacity`
        and the default width is 4.

    [`inodes`]()
    : \
        Total inode count. The title string is `Inodes` and the
        default width is 7.

    [`iused`]()
    : \
        Used inode count. The title string is `Iused` and the default
        width is 7.

    [`mounted`]()
    : \
        Mounted on path. The title string is `Mounted on` and the
        default width is -19.

    [`size`]()
    : Native block size. The title string is `Size` and the default
        width is 4.

    [`options`]()
    : \
        [`mount`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man1/mount.html)(1) options.
        The title string is `Options` and the default width is -29.

    [`type`]()
    : Filesystem type. The title string is `Type` and the default
        width is 10.

    [`used`]()
    : Used block count. The title string is `Used` and the default
        width is determined by the `-b` , `-g`, `-k`, `-m` and
        `-n` options.

-`g`, --`gigabytes`
:   Measure disk usage in 1024M byte blocks.

-`h`, --`header|heading`
:   Display a heading line. On by default; -`h` means
    --`noheader|heading`.

-`i`, --`inodes`
:   Display inode usage instead of block usage. There is at least one
    inode for each active file and directory on a filesystem.

-`k`, --`kilobytes`
:   Measure disk usage in 1024 byte blocks.

-`K`, --`scale|binary-scale|human-readable`
:   Scale disk usage to powers of 1024. This is the default if `getconf
    CONFORMANCE` is not `standard`.

-`l`, --`local`
:   List information on local filesystems only, i.e., network mounts
    are omitted.

-`m`, --`megabytes`
:   Measure disk usage in 1024K byte blocks.

-`n`, --`native-block`
:   Measure disk usage in the native filesystem block size. This size
    may vary between filesystems; it is displayed by the `size`
    format identifier.

-`O`, --`options`
:   Display the
    [`mount`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man1/mount.html)(1) options.

-`P`, --`portable`
:   Display each filesystem on one line. By default output is folded
    for readability. Also implies `--blockbytes`.

-`s`, --`sync`
:   Call
    [`sync`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man2/sync.html)(2)
    before querying the filesystems.

-`F|t`, --`type`=`type`
:   Display all filesystems of type `type`. Unknown types are listed as
    `local`. Typical (but not supported on all systems) values are:

    [`ufs`]()
    : default UNIX file system

    [`ext2`]()
    : default linux file system

    [`xfs`]()
    : sgi XFS

    [`nfs`]()
    : network file system version 2

    [`nfs3`]()
    : network file system version 3

    [`afs3`]()
    : Andrew file system

    [`proc`]()
    : process file system

    [`fat`]()
    : DOS FAT file system

    [`ntfs`]()
    : nt file system

    [`reg`]()
    : windows/nt registry file system

    [`lofs`]()
    : loopback file system for submounts

-`v`, --`verbose`
:   Report all filesystem query errors.

-`q|T`
: Ignored by this implementation.

# EXAMPLES

The default `--format` is "%\#..1(filesystem)s %\#(type)s %\#(blocks)s
%\#(used)s %\#(available)s %\#(capacity)s %(mounted)s"

# SEE ALSO

[`getconf`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man1/getconf.html)(1),
[`mount`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man1/mount.html)(1),
[`ls`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man1/ls.html)(1),
[`pax`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man1/pax.html)(1),
[`ps`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man1/ps.html)(1),
[`mount`](/web/20150109080100/http://www2.research.att.com:80/~astopen/man/man2/mount.html)(2)

# IMPLEMENTATION

`version`
:   df (AT&T Research) 2010-08-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150109080100/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150109080100/http://www.eclipse.org/org/documents/epl-v10.html)


