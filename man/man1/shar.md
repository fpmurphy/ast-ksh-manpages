# NAME

shar - create a shell archive

# SYNOPSIS

`shar` \[ `options` \] \[files ...\]

# DESCRIPTION

`shar` reads one or more input files and creates a shell script which
when executed will restore the contents of these files. This is called a
shell archive or `shar`. The resulting archive is sent to standard
output unless the `-o` option is specified.

# OPTIONS

-`a`, --`net-headers`
:   Automatic generation of headers. The `-n` option must also
    be specified. If the archive name does not contain a `/`, then
    `/part` will be append to the given archive name when constructing
    the header.

-`b`, --`bits-per-code`=`bits`
:   When doing compression, use `-b` `bits` as a parameter to
    [`compress`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/compress.html)(1).
    The `-b` option turns on `-Z`.

-`c`, --`cut-mark`
:   Start the shar with a cut line.

-`d`, --`here-delimiter`=`string`
:   Use `string` to delimit the files in the shar instead of
    `SHAR\_EOF`.

-`f`, --`basenames`
:   Use the basenames for the files.

-`g`, --`level-for-gzip`=`level`
:   When doing compression, use `-``level` as a parameter to
    [`gzip`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1).
    The `-g` option turns on `-z`.

-`l`, --`whole-size-limit`=`size`
:   Limit the output file size to `size` bytes. A suffix of `b` ,
    `k`, or `m` can be specified to indicate 512-byte blocks,
    kilobytes, or megabytes respectively.

-`n`, --`archive-name`=`name`
:   Override automatically determined name for the archive with `name` .

-`o`, --`output-prefix`=`prefix`
:   Save the archive files `prefix``.01` through `prefix` `.``nn`
    instead of standard output. This option must be used when `-l` or
    the `-L` is specified.

-`p`, --`intermix-type`
:   Allow positional parameter options. The options `-B`, `-T`,
    `-z` and `-Z` may be embedded, and files to the right of the
    option will be processed in the specified mode.

-`q`, --`quit|silent`
:   Do not output verbose messages locally when producing the archive.

-`s`, --`submitter`=`user`
:   Override automatically determined submitter name with `user` which
    is of the form `who``@``where`.

-`t`, --`tty`
:   Write errors and the name of each file to `/dev/tty` as it
    is archived.

-`w`, --`no-character-count`
:   Do NOT check each file with `wc -c` after unpack.

-`z`, --`gzip`
:   [`gzip`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1)
    and
    [`uuencode`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/uuencode.html)(1)
    all files prior to packing.

-`B`, --`uuencode,binary-files-files`
:   Treat all files as binary and
    [`uuencode`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/uuencode.html)(1)
    prior to packing.

-`D`, --`no-md5-digest`
:   Do NOT use `cksum md5sum` digest to verify the unpacked files. The
    default is to check.

-`L`, --`split-size-limit`=`size`
:   Limit the output file size to `size` bytes as with `-l` , but
    split the archive into multiple files.

-`Q`, --`quiet-unshar`
:   Verbose OFF. Disables the inclusion of comments to be output when
    the archive is unpacked.

-`M`, --`mixed-uuencode`
:   Mixed mode. Determine if the files are text or binary and archive
    correctly. Files found to be binary are uuencoded prior to packing.
    This is the default.

-`S`, --`stdin-file-list`
:   Read list of files to be packed from the standard input rather than
    from the command line in the format generated by
    [`find`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/find.html)(1)
    and
    [`tw`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/tw.html)(1).
    If `-p` is specified, the options `-B`, `-T`, `-z` and
    `-Z` must be included in the standard input.

-`T`, --`text-files`
:   Treat all files as text.

-`X`, --`query-user`
:   When unpacking, ask the user if files should be overwritten.

-`Z`, --`compress`
:   [`compress`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/compress.html)(1)
    and
    [`uuencode`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/uuencode.html)(1)
    all files prior to packing.

# SEE ALSO

[`cksum`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/cksum.html)(1),
[`compress`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/compress.html)(1),
[`find`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/find.html)(1),
[`gzip`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1),
[`pax`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/pax.html)(1),
[`tw`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/tw.html)(1),
[`uuencode`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/uuencode.html)(1),
[`wc`](/web/20141128030250/http://www2.research.att.com/~astopen/man/man1/wc.html)(1)

# IMPLEMENTATION

`version`
:   shar (AT&T Labs Research) 1999-04-20

`author`
:   David Korn

`copyright`
:   Copyright © 1999-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030250/http://www.eclipse.org/org/documents/epl-v10.html)


