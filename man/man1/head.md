# NAME

head - output beginning portion of one or more files

# SYNOPSIS

`head` \[ `options` \] \[ file ... \]

# DESCRIPTION

`head` copies one or more input files to standard output stopping at a
designated point for each file or to the end of the file whichever comes
first. Copying ends at the point indicated by the options. By default a
header of the form `==&gt;` `filename` `&lt;==` is output before all
but the first file but this can be changed with the `-q` and `-v`
options.
If no `file` is given, or if the `file` is `-`, `head` copies from
standard input starting at the current location.

The option argument for `-c`, and `-s` can optionally be followed by
one of the following characters to specify a different unit other than a
single byte:

`b`
: 512 bytes.

`k`
: 1-killobyte.

`m`
: 1-megabyte.

For backwards compatibility, `-``number` is equivalent to `-n`
`number`.

# OPTIONS

-`n`, --`lines`=`lines`
:   Copy `lines` lines from each file. The default value is `10`.

-`c`, --`bytes`=`chars`
:   Copy `chars` bytes from each file.

-`q`, --`quiet|silent`
:   Never ouput filename headers.

-`s`, --`skip`=`skip`
:   Skip `skip` characters or lines from each file before copying.

-`v`, --`verbose`
:   Always ouput filename headers.

# EXIT STATUS

`0`
: All files copied successfully.

`&gt;0`
:   One or more files did not copy.

# SEE ALSO

[`cat`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/cat.html)(1),
[`tail`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/tail.html)(1)

# IMPLEMENTATION

`version`
:   head (AT&T Research) 2012-05-31

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030244/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030244/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030244/http://www.eclipse.org/org/documents/epl-v10.html)


