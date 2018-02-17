# NAME

unpack - unpack files created by pack

# SYNOPSIS

`unpack` \[ `options` \] file ...

# DESCRIPTION

`unpack` expands files created by `pack`. For each `file` specified,
a search is made for a file named `file``.z` (or just `file`, if
`file` ends in `.z`). If this file appears to be a packed file, it is
replaced by its original expanded version. The new file has the `.z`
suffix stripped from its name, and has the same access modes, access and
modification dates, and owner as those of the packed file.

# EXIT STATUS

`0`
: All files unpacked successfully.

`n`
: `n` files failed to unpack, where `n` is less than 125.

`125`
: 125 or more files failed to unpack.

# SEE ALSO

pack(1), pcat(1), uncompress(1), gunzip(1)

# IMPLEMENTATION

`version`
:   unpack (AT&T Research) 2003-04-28

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030252/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1993-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030252/http://www.eclipse.org/org/documents/epl-v10.html)


