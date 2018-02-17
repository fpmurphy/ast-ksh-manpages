# NAME

du - summarize disk usage

# SYNOPSIS

`du` \[ `options` \] \[ path ... \]

# DESCRIPTION

`du` reports the number of blocks contained in all files and
recursively all directories named by the `path` arguments. The current
directory is used if no `path` is given. Usage for all files and
directories is counted, even when the listing is omitted. Directories
and files are only counted once, even if they appear more than once as a
hard link, a target of a symbolic link, or an operand.
The default block size is 512. The block count includes only the actual
data blocks used by each file and directory, and may not include other
filesystem data required to represent the file. Blocks are counted only
for the first link to a file; subsequent links are ignored. Partial
blocks are rounded up for each file.

If more than one of `-b`, `-h`, `-k`, `-K,` or `-m` are
specified only the rightmost takes affect.

# OPTIONS

-`a`, --`all`
:   List usage for each file. If neither `--all` nor `--summary` is
    specified then only usage for the `path` arguments and directories
    is listed.

-`b`, --`blocksize`\[=`size`\]
:   Set the block size to `size`. If omitted, `size` defaults to 512.
    The option value may be omitted. The default value is `512`.

-`f`, --`silent`
:   Do not report file and directory access errors.

-`h`, --`binary-scale|human-readable`
:   Scale disk usage to powers of 1024.

-`K`, --`decimal-scale`
:   Scale disk usage to powers of 1000.

-`k`, --`kilobytes`
:   List usage in units of 1024 bytes.

-`m`, --`megabytes`
:   List usage in units of 1024K bytes.

-`s`, --`summary|summarize`
:   Only display the total for each `path` argument.

-`t|c`, --`total`
:   Display a grand total for all files and directories.

-`v|r`, --`verbose`
:   Report all file and directory access errors. This is the default.

-`x|X|l`, --`xdev|local|mount|one-file-system`
:   Do not descend into directories in different filesystems than
    their parents.

-`L`, --`logical|follow`
:   Follow symbolic links. The default is `--physical`.

-`H`, --`metaphysical`
:   Follow command argument symbolic links, otherwise don't follow. The
    default is `--physical` .

-`P`, --`physical`
:   Don't follow symbolic links. The default is `--physical`.

# SEE ALSO

[`find`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/find.html)(1),
[`ls`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/ls.html)(1),
[`tw`](/web/20141128030242/http://www2.research.att.com/~astopen/man/man1/tw.html)(1)

# IMPLEMENTATION

`version`
:   du (AT&T Research) 2012-01-26

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030242/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030242/http://www.eclipse.org/org/documents/epl-v10.html)


