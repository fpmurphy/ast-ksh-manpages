# NAME

pack - pack files using Huffman coding

# SYNOPSIS

`pack` \[ `options` \] file ...

# DESCRIPTION

`pack` attempts to store the specified files in a compressed form
using static Huffman coding. Wherever possible each `file` is replaced
by a packed file named `file``.z` with the same access modes, access
and modified dates, and owner as those of `file`. The `-f` option
forces packing of `file` even when there is no space benefit for packing
the file.
If `pack` is successful, `file` will be removed. Packed files can be
restored to their original form using `unpack` or `pcat`.

`pack` uses Huffman (minimum redundancy) codes on a byte-by-byte
basis. Ordinarily, for each file that is packed, a line is written to
standard output containing `file``.z` and the percent compression. If
the `-v` options is specified, or if the `-` argument is specified,
an internal flag is set that causes the number of times each byte is
used, its relative frequency, and the code for the byte to be written to
the standard output. Additional occurrences of `-` in place of name
cause the internal flag to be set and reset.

No packing occurs if:

`-`
: `file` appears to be already packed.

`-`
: `file` has links.

`-`
: `file` is a directory.

`-`
: `file` cannot be opened.

`-`
: No disk storage blocks will be saved by packing unless `-f`
    is specified.

`-`
: A file called `file``.z` already exists.

`-`
: The `.z` file cannot be created.

`-`
: An I/O error occurred during processing.

# OPTIONS

-`f`, --`force`
:   Pack the file even if the packed size is larger than the original.

-`v`, --`verbose`
:   Causes additional information to be written to standard ouput.

# EXIT STATUS

`0`
: All files packed successfully.

`n`
: `n` files failed to pack, where `n` is less than 125.

`125`
: 125 or more files failed to pack.

# SEE ALSO

[`unpack`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/unpack.html)(1),
[`pcat`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/pcat.html)(1),
[`compress`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/compress.html)(1),
[`gzip`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1)

# IMPLEMENTATION

`version`
:   pack (AT&T Research) 2003-04-28

`author`
:   David Korn

`copyright`
:   Copyright © 1993-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030247/http://www.eclipse.org/org/documents/epl-v10.html)


