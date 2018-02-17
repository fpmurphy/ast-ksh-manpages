# NAME

mount - mount and display filesystems

# SYNOPSIS

`mount` \[ `options` \] \[ fs \[ dir \] \]

# DESCRIPTION

`mount` attaches a named filesystem `fs` to the directory `dir`, which
must already exist. The contents of `dir` are hidden until the
filesystem is unmounted. The filesystem mount table is consulted if
either of `fs` or `dir` are omitted. Information on all mounted
filesystems is displayed if both `fs` and `dir` are omitted.

# OPTIONS

-`a`, --`all`
:   Operate on all filesystems in the filesystem table. The `--host`
    and `--type` options can be used to match parts of the table.

-`f`, --`show|fake`
:   Display but do not execute the underlying
    [`mount`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man2/mount.html)(2)
    system calls.

-`h`, --`hosts`=`\[!\]host,...`
:   Limit the filesystem table scan to entries matching the
    `host` names. A leading `!` inverts the match sense.

-`M`, --`mtab|fstab`=`file`
:   Use `file` instead of the default filesystem table.

-`b`, --`omit`=`\[!\]type,...`
:   Omit filesystem table entries matching any of the `type` names.

-`o`, --`options`=`\[no\]name\[=value\]\[,...\]`
:   Specify filesystem specific mount options. Options are a comma
    separated list of words preceded by an optional `no` to turn the
    option off, or `name=value` pairs. Multiple `--options` are
    concatenated with a `comma` separator. See
    [`fstab`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man4/fstab.html)(4)
    for a detailed description of mount options.

-`p`, --`portable`
:   Print information in
    [`fstab`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man4/fstab.html)(4) format.

-`r`, --`readonly`
:   Mount the filesystems read only. Equivalent to `--option=ro`.

-`t|T`, --`types`=`\[!\]type,...`
:   Limit the filesystem table scan to entries matching the
    `type` names. A leading `!` inverts the match sense.

-`u`, --`unmount|umount`
:   Unmount the matched filesystems.

-`c`, --`check`
:   Ignored by this implementation.

-`m`, --`multiplex|nproc`
:   Distribute multiple mounts across `nproc` processes. Ignored by
    this implementation.

-`P`, --`prefix`=`string`
:   Ignored by this implementation.

-`n`, --`tab`
:   Ignored by this implementation. On by default; -`n` means
    --`notab`.

-`v`, --`verbose`
:   Ignored by this implementation.

# SEE ALSO

[`df`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/df.html)(1),
[`umount`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/umount.html)(1),
[`mount`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man2/mount.html)(2),
[`fstab`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man4/fstab.html)(4)

# IMPLEMENTATION

`version`
:   mount (AT&T Research) 2011-02-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030239/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1998-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030239/http://www.eclipse.org/org/documents/epl-v10.html)


