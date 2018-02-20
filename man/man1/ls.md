# NAME

ls - list files and/or directories

# SYNOPSIS

`ls` \[ `options` \] \[ file ... \]

# DESCRIPTION

For each directory argument `ls` lists the contents; for each file
argument the name and requested information are listed. The directory
`.` is assumed if no file arguments appear. The listing is sorted by
file name by default, except that file arguments are listed before
directories.
Multi-column terminal output display width is determined by
[`ioctl`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man2/ioctl.html)(2)
and/or the `COLUMNS` environment variable.

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

-`a`, --`all`
:   List entries starting with `.`; turns off `--almost-all`.

-`A`, --`almost-all`
:   List all entries but `.` and `..`; turns off `--all`.

-`b`, --`escape`
:   Print escapes for nongraphic characters.

-`B`, --`ignore-backups`
:   Do not list entries ending with \~.

-`c`, --`ctime`
:   Sort by change time; list ctime with `--long`.

-`C`, --`multi-column`
:   List entries by columns.

-`d`, --`directory`
:   List directory entries instead of contents.

-`D`, --`define`=`key\[=value\]`
:   Define `key` with optional `value`. `value` will be expanded when
    `%(``key``)` is specified in `--format`. `key` may override
    internal `--format` identifiers.

-`e`, --`long-iso|long-time`
:   Equivalent to `--long --time-style=long-iso`.

-`E`, --`full-iso|full-time`
:   Equivalent to `--long --time-style=full-iso`.

-`f`, --`force`
:   Force each argument to be interpreted as a directory and list the
    name found in each slot in the physical directory order. Turns on
    `-aU` and turns off `-lrst`. The results are undefined for
    non-directory arguments.

-`Z`, --`format`=`format`
:   Append to the listing format string. `format` follows
    [`printf`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man3/printf.html)(3)
    conventions, except that
    [`sfio`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man3/sfio.html)(3)
    inline ids are used instead of arguments:
    %\[-+\]\[`width`\[.`precis` \[.`base`\]\]\](`id`\[:`subformat`\])`char`. If `char` is `s` then
    the string form of the item is listed, otherwise the corresponding
    numeric form is listed. `subformat` overrides the default formatting
    for `id`. Supported `id`s and `subformat`s are:

    [`atime`]()
    : \
        access time

    [`blocks`]()
    : \
        size in blocks

    [`ctime`]()
    : \
        change time

    [`dev`]()
    : major/minor device numbers

    [`device`]()
    : \
        major/minor device numbers if block or character special device

    [`devmajor`]()
    : \
        major device number

    [`devminor`]()
    : \
        minor device number

    [`dir.blocks`]()
    : \
        directory blocks

    [`dir.bytes`]()
    : \
        directory size in bytes

    [`dir.count`]()
    : \
        directory entry count

    [`dir.files`]()
    : \
        directory file count

    [`flags`]()
    : \
        command line flags in effect

    [`gid`]()
    : group id

    [`header`]()
    : \
        listing header

    [`ino`]()
    : serial number

    [`linkop`]()
    : \
        link operation: -&gt; for symbolic, empty otherwise

    [`linkname`]()
    : \
        symbolic link text

    [`linkpath`]()
    : \
        symbolic link text

    [`mark`]()
    : file or directory mark character

    [`markdir`]()
    : \
        directory mark character

    [`mode`]()
    : access mode

    [`mtime`]()
    : \
        modification time

    [`name`]()
    : entry name

    [`nlink`]()
    : \
        hard link count

    [`path`]()
    : file path from original root dir

    [`perm`]()
    : access permissions

    [`size`]()
    : file size in bytes

    [`summary`]()
    : \
        listing summary info

    [`total.blocks`]()
    : \
        running total block count

    [`total.bytes`]()
    : \
        running total size in bytes

    [`total.files`]()
    : \
        running total file count

    [`trailer`]()
    : \
        listing trailer

    [`uid`]()
    : owner id

    [`view`]()
    : 3d fs view level, 0 for the top or 2d

    [`----`]()
    : subformats ----

    [`case`:`p``1`:`s``1`:...:`p``n`:`s``n`]()
    : \
        Expands to `s``i` if the value of `id` matches the shell
        pattern `p``i`, or the empty string if there is no match.

    [`mode`]()
    : The integral value as a
        [`fmtmode`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man3/fmtmode.html)(3) string.

    [`perm`]()
    : The integral value as a
        [`fmtperm`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man3/fmtperm.html)(3) string.

    [`time\[=``format`\]]()
    : \
        The integral value as a
        [`strftime`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man3/strftime.html)(3) string.
        For example, `--format="%8(mtime)u %(ctime:time=%H:%M:%S)s"`
        lists the mtime in seconds since the epoch and the ctime
        as hours:minutes:seconds.

-`F`, --`classify`
:   Append a character for typing each entry. Turns on `--physical`.

-`g`, --`group`
:   `--long` with no owner info.

-`G`
: `--long` with no group info.

-`h`, --`scale|binary-scale|human-readable`
:   Scale sizes to powers of 1024 { Ki Mi Gi Ti Pi Xi }.

-`i`, --`inode`
:   List the file serial number.

-`I`, --`ignore`=`pattern`
:   Do not list implied entries matching shell `pattern`.

-`k`, --`kilobytes`
:   Use 1024 blocks instead of 512.

-`K`, --`shell-quote`
:   Enclose entry names in shell \$'...' if necessary.

-`l`, --`long|verbose`
:   Use a long listing format.

-`m`, --`commas|comma-list`
:   List names as comma separated list.

-`n`, --`numeric-uid-gid`
:   List numeric user and group ids instead of names.

-`N`, --`literal|show-controls-chars`
:   Print raw entry names (don't treat e.g. control
    characters specially).

-`o`, --`owner`
:   `--long` with no group info.

-`O`
: `--long` with no owner info.

-`p`, --`markdir`
:   Append / to each directory name.

-`q`, --`hide-control-chars`
:   Print ? instead of non graphic characters.

-`Q`, --`quote-name`
:   Enclose all entry names in "...".

-`J`, --`quote-style|quoting-style`=`style`
:   Quote entry names according to `style`:

    [`c|C`]()
    : C "..." quote.

    [`escape`]()
    : \
        `\\` escape if necessary.

    [`literal`]()
    : \
        No quoting.

    [`question`]()
    : \
        Replace unprintable characters with `?`.

    [`shell`]()
    : \
        Shell \$'...' quote if necessary.

    [`S|shell-always`]()
    : \
        Shell \$'...' every name.

The default value is `question`.\
-`r`, --`reverse`
:   Reverse order while sorting.

-`R`, --`recursive`
:   List subdirectories recursively.

-`s`, --`size`
:   Print size of each file, in blocks.

-`S`, --`bysize`
:   Sort by file size.

-`t`
: Sort by modification time; list mtime with `--long`.

-`T`, --`tabsize`=`columns`
:   Ignored by this implementation.

-`u`, --`access`
:   Sort by last access time; list atime with `--long`.

-`U`
: Equivalent to `--sort=none`.

-`V`, --`colors|colours`\[=`key`\]
:   `key` determines when color is used to distinguish types:

    [`never`]()
    : \
        Never use color.

    [`always`]()
    : \
        Always use color.

    [`tty|auto`]()
    : \
        Use color when output is a tty.

The option value may be omitted. The default value is `never`.\
-`w`, --`width`=`\[screen-heightX\]screen-width`
:   Set the screen width to `screen-width` and the screen height to
    `screen-height` if specified.

-`W`, --`time`=`key`
:   Display `key` time instead of the modification time:

    [`atime|access|use`]()
    : \
        access time

    [`ctime|status`]()
    : \
        status change time

    [`mtime|time`]()
    : \
        modify time

-`x`, --`across`
:   List entries by lines instead of by columns.

-`X`, --`extension`
:   Sort alphabetically by entry extension.

-`y`, --`sort`\[=`key`\]
:   Sort by `key`:

    [`atime|access|use`]()
    : \
        Access time.

    [`ctime|status`]()
    : \
        Status change time.

    [`x|extension`]()
    : \
        File name extension.

    [`mtime|time`]()
    : \
        Modify time.

    [`f|name`]()
    : \
        File name.

    [`none`]()
    : Don't sort.

    [`size|blocks`]()
    : \
        File size.

    [`version`]()
    : \
        File name version.

The option value may be omitted.\
-`Y`, --`layout`=`key`
:   Listing layout `key`:

    [`across|horizontal`]()
    : \
        Multi-column across the page.

    [`comma`]()
    : \
        Comma separated names across the page.

    [`long|verbose`]()
    : \
        Long listing.

    [`v|multi-column|vertical`]()
    : \
        Multi-column by column.

    [`1|single-column`]()
    : \
        One column down the page.

-`z`, --`time-style`=`style`
:   List the time according to `style`:

    [`iso`]()
    : Equivalent to `+%Q/%m-%d+%H:%M/%Y-%m-%d /`.

    [`posix-iso`]()
    : \
        No change for the C or posix locales, `iso` otherwise.

    [`full-iso`]()
    : \
        Equivalent to `+%\_EK`.

    [`long-iso`]()
    : \
        Equivalent to `+%\_K`.

    [`posix-full-iso`]()
    : \
        No change for the C or posix locales, `full-iso` otherwise.

    [`L|locale`]()
    : \
        Equivalent to `+%c`.

    [`+``format`]()
    : \
        A
        [`date`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man1/date.html)(1)
        +`format`.

-`1`, --`one-column`
:   List one file per line.

-`L`, --`logical|follow`
:   Follow symbolic links. The default is determined by `getconf
    PATH\_RESOLVE`.

-`H`, --`metaphysical`
:   Follow command argument symbolic links, otherwise don't follow. The
    default is determined by `getconf PATH\_RESOLVE`.

-`P`, --`physical`
:   Don't follow symbolic links. The default is determined by `getconf
    PATH\_RESOLVE`.

--`block-size`=`blocksize`
:   Use `blocksize` blocks.

--`decimal-scale|thousands`
:   Scale sizes to powers of 1000 { K M G T P X }.

--`dump`
:   Print the generated `--format` string on the standard output
    and exit.

--`testdate`=`date`
:   `--format` time values newer than `date` will be printed as
    `date`. Used for regression testing.

--`testsize`=`shift`
:   Shift file sizes left `shift` bits and set file block counts to the
    file size divided by 512. Used for regression testing.

# SEE ALSO

[`chmod`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man1/chmod.html)(1),
[`find`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man1/find.html)(1),
[`getconf`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man1/getconf.html)(1),
[`tw`](/web/20150817032516/http://www2.research.att.com:80/~astopen/man/man1/tw.html)(1)

# BUGS

Can we add options to something else now?

# IMPLEMENTATION

`version`
:   ls (AT&T Research) 2012-04-20

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150817032516/http://www.eclipse.org/org/documents/epl-v10.html)


