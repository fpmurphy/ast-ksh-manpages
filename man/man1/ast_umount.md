# NAME

umount - unmount filesystems

# SYNOPSIS

`umount` \[ `options` \] \[ fs | dir \]

# DESCRIPTION

`umount` unmounts one or more currently mounted filesystems, which can
be specified either as mounted-on directories or filesystems.

# OPTIONS

-`a`, --`all`
:   Operate on all filesystems in the filesystem table. The `--host`
    and `--type` options can be used to match parts of the table.

-`f`, --`show|fake`
:   Display but do not execute the underlying
    [`umount`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man2/umount.html)(2)
    system calls.

-`h`, --`hosts`=`\[!\]host,...`
:   Limit the filesystem table scan to entries matching the
    `host` names. A leading `!` inverts the match sense.

-`M`, --`mtab|fstab`=`file`
:   Use `file` instead of the default filesystem table.

-`b`, --`omit`=`\[!\]type,...`
:   Omit filesystem table entries matching any of the `type` names.

-`t|T`, --`types`=`\[!\]type,...`
:   Limit the filesystem table scan to entries matching the
    `type` names. A leading `!` inverts the match sense.

-`m`, --`multiplex|nproc`
:   Distribute multiple mounts across `nproc` processes. Ignored by
    this implementation.

-`P`, --`prefix`=`string`
:   Ignored by this implementation.

-`v`, --`verbose`
:   Ignored by this implementation.

# SEE ALSO

[`df`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/df.html)(1),
[`mount`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/mount.html)(1),
[`umount`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man2/umount.html)(2),
[`fstab`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man4/fstab.html)(4)

# IMPLEMENTATION

`version`
:   umount (AT&T Research) 1999-11-19

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1998-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030239/http://www.eclipse.org/org/documents/epl-v10.html)


