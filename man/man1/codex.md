# NAME

codex - encode/decode filter

# SYNOPSIS

`codex` \[ `options` \] \[ \[ &lt;,&gt; \] method \[ &lt;,&gt;,| method ... \] \]

# DESCRIPTION

`codex` decodes the standard input and/or encodes the standard output
according to the `method` operand.
Codex method names consist of a leading identifier and 0 or more options
separated by `-` or `+`. Method names with identical `-` options
are equivalent. For example, `uu-base64-text` specifies the `uu`
method with the `base64` and `text` options, and
`pzip-crc+partition=test` specifies the `pzip` method with `crc`
enabled using the `test` partition.

Methods may be composed using the `&lt;` and `&gt;` operators (with
no intervening space.) `&lt;``method` applies the `method` decoder and
`&gt;``method` applies the `method` encoder.

Supported methods are listed below. Each method may have one or more of
these attributes:

`decode`
:   Only decoding is supported -- most likely because the encoder has
    not been published. If omitted then both encoding and are supported.

`ident`
:   The decoder self-identifies from the input data and does not require
    an explicit `method` operand.

`vcodex`
:   A self-identifying
    [`vcodex`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man3/vcodex.html)(3) method.
    The encoder and decoder may be applied to either the input
    or output. Otherwise decode is restricted to the input and encode is
    restricted to the output.

By default decoders are applied to the standard input from left to
right, and encoders are applied to the standard output from right to
left. `vcodex` methods may be applied to either the input or output
depending on the composition context.
All methods accept these options:

`PASSPHRASE=``passphrase`
:   The method specific passphrase. If not specified then
    `--passphrase`=`passphrase` is used. If `--passphrase` is not
    specified then the passphrase for each method requiring one is
    prompted on and read from `/dev/tty`. Default to the interactive
    prompt to avoid exposing passphrases to other processes.

`RETAIN`
:   Decode/encode state is retained across discipline
    `initf`/`donef` calls.

`SIZE=``size`
:   The decoded size is `size`. Some decode methods that lack end of
    data markers require this because they may read/write garbage data
    at the end of the encoded data.

`SOURCE=``file`
:   The delta method source `file`.

`TRACE`
:   Enable method trace.

`VERBOSE`
:   Enable verbose method trace.

The `CODEX\_OPTIONS` environment variable may contain space separated
options that control all
[`codex`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man3/codex.html)(3)
methods. The environment options are:

`trace=``pattern`
:   Enable method trace for all methods matching the
    [`ksh`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    `pattern`.

`verbose=``pattern`
:   Enable verbose method trace for all methods matching the
    [`ksh`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    `pattern`. A verbose trace includes
    [`codex`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man3/codex.html)(3)
    discipline exception calls.

The supported methods are:

`uu`
: uuencode printable encoding.

    [`posix`]()
    : \
        Posix
        [`uuencode`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/uuencode.html)(1).
        This is the default.

    [`base64|mime`]()
    : \
        MIME base64 encoding.

    [`bsd|ucb`]()
    : \
        BSD
        [`uuencode`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/uuencode.html)(1).

    [`string`]()
    : \
        Encode into a string with no separators (base64 only).

    [`text`]()
    : Encode \\n =&gt; \\r\\n, decode \\r\\n =&gt; \\n.

    [``(version)]()
    : \
        codex-uu (AT&T Research) 2010-01-15

    [``(author)]()
    : \
        Glenn Fowler
        &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030240/mailto:glenn.s.fowler@gmail.com)&gt;

`qp`
: quoted printable encoding.

    [``(version)]()
    : \
        codex-qp (AT&T Research) 1998-11-11

    [``(author)]()
    : \
        Glenn Fowler
        &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030240/mailto:glenn.s.fowler@gmail.com)&gt;

`rot13`
:   rot13 self-inverting encoding.

    [``(version)]()
    : \
        codex-rot13 (AT&T Research) 2003-12-11

    [``(author)]()
    : \
        Glenn Fowler
        &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030240/mailto:glenn.s.fowler@gmail.com)&gt;

`iconv`
:   iconv character codeset conversion. One or two character codeset
    options must be specified. Two options specify the source and
    destination codesets. One option specifies the decode source or
    encode destination codeset; the implied second codeset defaults to
    `native`.

    [a|ascii|?(iso)?(-)646|?(iso)?(-)8859|latin]()
    : \
        8 bit ascii

    [e|ebcdic?(-)?(\[1e\]]()
    : \
        X/Open ebcdic

    [o|ebcdic?(-)\[3o\]|?(cp|ibm)1047|open?(-)edition]()
    : \
        mvs OpenEdition ebcdic

    [h|ebcdic?(-)h|?(cp|ibm)?(00)37|\[oa\]s?(/-)400]()
    : \
        ibm OS/400 AS/400 ebcdic

    [s|ebcdic?(-)s|siemens|posix-bc]()
    : \
        siemens posix-bc ebcdic

    [i|ebcdic?(-)\[2i\]|ibm]()
    : \
        X/Open ibm ebcdic (not idempotent)

    [m|ebcdic?(-)m|mvs]()
    : \
        mvs ebcdic

    [u|ebcdic?(-)(u|mf)|microfocus]()
    : \
        microfocus cobol ebcdic

    [n|native|local]()
    : \
        native code set

    [un|unicode|utf]()
    : \
        multibyte 8-bit unicode

    [um|ume|utf?(-)7]()
    : \
        multibyte 7-bit unicode

    [big|euc)\`]()
    : \
        euc family

    [dos?(-)?(855]()
    : \
        dos code page

    [ucs?(-)?(2)?(be)|utf-16?(be]()
    : \
        unicode runes

    [ucs?(-)?(2)le|utf-16le]()
    : \
        little endian unicode runes

    [``(version)]()
    : \
        codex-iconv (AT&T Research) 2000-05-09

    [``(author)]()
    : \
        Glenn Fowler
        &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030240/mailto:glenn.s.fowler@gmail.com)&gt;

`aes`
: AES (FIPS-197 rijndael) encryption. The first option is the block
    size in bits. Sizes { 128 192 256 } are supported. The default
    is 256.

    [``(author)]()
    : \
        Peter Selinger (ccrypt)

    [``(license)]()
    : \
        GPL

`bzip` (ident)
:   bzip2 compression. The first parameter is the compression level,
    1:least, 9:most(default).

`compress` (ident)
:   compress LZW compression. The first parameter is the maximum number
    of bits per code { 9 - 16 }. The default is 16.

`crypt-rar`
:   `rar` encryption. The first option is the `rar` implementation
    version. Versions { 13 15 20 } are supported.

    [``(version)]()
    : \
        crypt-rar-13 2003-12-29

    [``(author)]()
    : \
        Eugene Roshal

    [``(copyright)]()
    : \
        Copyright © 1999-2003 Eugene Roshal

    [``(license)]()
    : \
        GPL

`crypt-zip`
:   zip encryption. The encryption is asymmetric.

`gzip` (ident)
:   gzip compression. The first parameter is the compression level,
    1:least, 9:most(default). nocrc disables crc checks.

`lzd` (decode)
:   [`zoo`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/zoo.html)(1)
    archive lzd compression.

    [``(version)]()
    : \
        codex-lzd 1991-07-07

    [``(author)]()
    : \
        Rahul Dhesi

`lzh` (decode)
:   lzh compression. The options are ordered. A single option alias
    (example `lzh-lh5` ) or `window-ccode`\[-`pcode`\] (example
    `lzh-4k-d0-s0`) are accepted. `pcode` defaults to `ccode`
    if omitted.

    [`lh0`]()
    : Equivalent to `copy`.

    [`lh1`]()
    : Equivalent to `lzh-4k-d0-s0`.

    [`lh2`]()
    : Equivalent to `lzh-8k-d1`.

    [`lh3`]()
    : Equivalent to `lzh-8k-s0`.

    [`lh4`]()
    : Equivalent to `lzh-4k-s1`.

    [`lh5`]()
    : Equivalent to `lzh-8k-s1`.

    [`lhd`]()
    : Equivalent to `copy`.

    [`lhj`]()
    : Equivalent to `lzh-26624-s1`.

    [`lz4`]()
    : Equivalent to `copy`.

    [`lz5`]()
    : Equivalent to `lzh-4k-s3`.

    [`lz6`]()
    : Equivalent to `lzh-32k-s1`.

    [`lz7`]()
    : Equivalent to `lzh-64k-s1`.

    [`lzs`]()
    : Equivalent to `lzh-2k-s2`.

    [`window=`size``]()
    : \
        Window size &lt;= 64k.

    [`coding`]()
    : \
        `ccode` or `pcode` coding method { d0 s0 s1 s2 s3 }.

    [``(version)]()
    : \
        codex-lzh 1998-11-11

`lzx` (decode)
:   Microsoft cabinet archive lzx compression from cabextract 0.6. The
    first parameter is the window size which must be a power of 2
    between 32k and 2m inclusive. The second parameter is the optional
    block aligment; 32k is required for cabinet file decompression.

`quantum` (decode)
:   Microsoft cabinet archive quantum compression from cabextract 0.6.
    The first parameter is the window size which must be a power of 2
    between 1k and 2m inclusive. The second parameter is the optional
    block aligment; 32k is required for cabinet file decompression.

`rar` (decode)
:   [`rar`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/rar.html)(1)
    2.0 archive compression.

    [``(version)]()
    : \
        codex-rar 2003-12-23

    [``(author)]()
    : \
        Eugene Roshal

    [``(copyright)]()
    : \
        Copyright © 1999-2003 Eugene Roshal

    [``(license)]()
    : \
        GPL

`sum`
: checksum filter. The checksum value returned by
    [`codexdata`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man3/codexdata.html)(3)
    is written to the standard error.

    [`att|sys5|s5|default`]()
    : \
        The system 5 release 4 checksum. This is the default for `sum`
        when `getconf UNIVERSE` is `att`. This is the only true sum;
        all of the other methods are order dependent.

    [`ast4|32x4|tw`]()
    : \
        The `ast` 128 bit PRNG hash generated by catenating 4 separate
        32 bit PNRG hashes. The block count is not printed.

    [`bsd|ucb`]()
    : \
        The BSD checksum.

    [`crc`]()
    : 32 bit CRC (cyclic redundancy check).

        [`polynomial=`mask``]()
        : \
            The 32 bit crc polynomial bitmask with implicit bit 32. The
            default value is `0xedb88320`.

        [`done\[=`number`\]`]()
        : \
            XOR the final crc value with `number`. 0xffffffff is used if
            `number` is omitted. The option value may be omitted. The
            default value is `0`.

        [`init\[=`number`\]`]()
        : \
            The initial crc value. 0xffffffff is used if `number`
            is omitted. The option value may be omitted. The default
            value is `0`.

        [`rotate`]()
        : \
            XOR each input character with the high order crc byte
            (instead of the low order).

        [`size\[=`number`\]`]()
        : \
            Include the total number of bytes in the crc. `number`, if
            specified, is first XOR'd into the size. The option value
            may be omitted. The default value is `0`.

    [`prng`]()
    : 32 bit PRNG (pseudo random number generator) hash.

        [`mpy=`number``]()
        : \
            The 32 bit PRNG multiplier. The default value is
            `0x01000193`.

        [`add=`number``]()
        : \
            The 32 bit PRNG addend. The default value is `0`.

        [`init\[=`number`\]`]()
        : \
            The PRNG initial value. 0xffffffff is used if `number`
            is omitted. The option value may be omitted. The default
            value is `0x811c9dc5`.

    [`md5|MD5`]()
    : \
        The RSA Data Security, Inc. MD5 Message-Digest Method, 1991-2,
        used with permission. The block count is not printed.

        [``(version)]()
        : \
            md5 (RSA Data Security, Inc. MD5 Message-Digest, 1991-2)
            1996-02-29

    [`sha1|SHA1|sha-1|SHA-1`]()
    : \
        FIPS 180-1 SHA-1 secure hash algorithm 1.

        [``(version)]()
        : \
            sha1 (FIPS 180-1) 1996-09-26

        [``(author)]()
        : \
            Steve Reid
            &lt;[steve@edmweb.com](https://web.archive.org/web/20141128030240/mailto:steve@edmweb.com)&gt;

    [`sha256|sha-256|SHA256|SHA-256`]()
    : \
        FIPS SHA-256 secure hash algorithm.

        [``(version)]()
        : \
            sha-256 (FIPS) 2000-01-01

        [``(author)]()
        : \
            Aaron D. Gifford

    [`sha384|sha-384|SHA384|SHA-384`]()
    : \
        FIPS SHA-384 secure hash algorithm.

        [``(version)]()
        : \
            sha-384 (FIPS) 2000-01-01

        [``(author)]()
        : \
            Aaron D. Gifford

    [`sha512|sha-512|SHA512|SHA-512`]()
    : \
        FIPS SHA-512 secure hash algorithm.

        [``(version)]()
        : \
            sha-512 (FIPS) 2000-01-01

        [``(author)]()
        : \
            Aaron D. Gifford

    [`posix|cksum|std|standard`]()
    : \
        The posix 1003.2-1992 32 bit crc checksum. This is the default
        [`cksum`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/cksum.html)(1) method.
        Shorthand for `crc-0x04c11db7-rotate-done-size` .

    [`zip`]()
    : The
        [`zip`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/zip.html)(1) crc.
        Shorthand for `crc-0xedb88320-init-done` .

    [`fddi`]()
    : The FDDI crc. Shorthand for `crc-0xedb88320-size=0xcc55cc55`.

    [`fnv|fnv1`]()
    : \
        The Fowler-Noll-Vo 32 bit PRNG hash with non-zero
        initializer (FNV-1). Shorthand for
        `prng-0x01000193-init=0x811c9dc5`.

    [`ast|strsum`]()
    : \
        The `ast`
        [`strsum`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man3/strsum.html)(3)
        PRNG hash. Shorthand for `prng-0x63c63cd9-add=0x9c39c33d`.

    [``(version)]()
    : \
        codex-sum (AT&T Research) 2003-12-16

    [``(author)]()
    : \
        Glenn Fowler
        &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030240/mailto:glenn.s.fowler@gmail.com)&gt;

`zip`
: zip compression. The first parameter is the PKZIP
    compression method.

    [`copy|0`]()
    : \
        No compression.

    [`shrink|1`]()
    : \
        Shrink compression.

    [`reduce|2|3|4|5`]()
    : \
        Reduce compression.

    [`implode|6`]()
    : \
        Implode compression.

    [`deflate|8`]()
    : \
        Deflate compression.

# OPTIONS

-`d`, --`decode`
:   Apply the `method` operand to the standard input only.

-`e`, --`encode`
:   Apply the `method` operand to the standard output only.

-`f`, --`passfile`=`file`
:   Like `--passphrase`, except the passphrase is the first line (sans
    newline) from `file`.

-`i`, --`identify`
:   Identify and write the standard input encoding name on the standard
    output and exit.

-`n`, --`null`
:   Write to the
    [`codenull`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man3/codenull.html)(3)
    stream instead of the standard output.

-`p`, --`passphrase`=`passphrase`
:   The default passphrase for all methods requiring passphrases. The
    method specific `PASSPHRASE`=`passphrase` overrides the default.
    If `--passphrase` and `PASSPHRASE`=`passphrase` are not
    specified then the passphrase for each method requiring one is
    prompted on and read from `/dev/tty`. Default to the interactive
    prompt to avoid exposing passphrases to other processes.

-`r`, --`invert|reverse`
:   Invert the method composition.

-`t`, --`trace`
:   Enable method trace. Equivalent to `export
    CODEX\_OPTIONS='trace=\`'`.

-`v`, --`verbose`
:   Enable verbose method trace. A verbose trace includes
    [`codex`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man3/codex.html)(3)
    discipline exception calls. Equivalent to `export
    CODEX\_OPTIONS='verbose=\`'`.

# SEE ALSO

[`codex`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man3/codex.html)(3),
[`vcodex`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man3/vcodex.html)(3)

# IMPLEMENTATION

`version`
:   codex (AT&T Research) 2009-04-15

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030240/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030240/mailto:dgkorn@gmail.com)&gt;

`author`
:   Phong Vo
    &lt;[kpv@research.att.com](https://web.archive.org/web/20141128030240/mailto:kpv@research.att.com)&gt;

`copyright`
:   Copyright © 2003-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030240/http://www.eclipse.org/org/documents/epl-v10.html)


