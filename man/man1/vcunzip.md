# NAME

vczip - vcodex method encode/decode filter

# SYNOPSIS

`vczip` \[ `options` \] \[ source \] &lt; input &gt; output

# DESCRIPTION

`vczip` is a filter that decodes the standard input and/or encodes the
standard output. The `--method` option specifies the encoding. The
default encoding is `--method=delta,huffgroup`. The method is
automatically determined when decoding.
For delta methods the `source` operand optionally specifies the file to
delta against. If `source` is omitted then the input file is simply
compressed. Delta-encoded data must be decoded with the same `source`.

Method aliases may be defined in `../lib/vcodex/aliases` in one of the
directories on `\$PATH`, or in `\$HOME/.vcziprc`, searched in order.
Each alias is a `name=value` pair where `value` is a `--method` option
value, described below. Method names are searched before alias names.

# OPTIONS

-`i`, --`input`=`file`
:   Input data is read from `file` instead of the standard input.

-`m`, --`method|encode`=`method\[.arg\]\[,method\[.arg\]...\]`
:   Set the transformation method from the `,` (or `\^`) separated
    list of `method`\[.`arg`\] elements, where `method` is a method
    alias or primitive method, `arg` is an optional method specific
    argument, and `-` denotes the default argument. Parenthesized
    values are implementation details. The `libvcodex` (`-catalog`)
    denotes a method supplied by the default library. Otherwise the
    method is a separate plugin; that plugin will be required to decode
    any encoded data. The primitive methods and method aliases are:

    [`delta`]()
    : \
        (Delta) Compression using the Vcdiff format. The arguments are:

        [`s`]()
        : String matching via suffix sorting.

        [`-`]()
        : String matching via hashing.

    [`hamming`]()
    : \
        Byte-wise differencing (like Hamming distance).

    [`huffgroup`]()
    : \
        Huffman encoding by groups

    [`huffman`]()
    : \
        Huffman encoding.

    [`huffpart`]()
    : \
        Huffman encoding by partitioning.

    [`bwt`]()
    : Burrows-Wheeler transform.

    [`map`]()
    : Mapping bytes from codeset to codeset. The arguments are:

        [`a2e`]()
        : ASCII -&gt; Xopen
            [`dd`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/dd.html)(1) EBCDIC.

        [`e2a`]()
        : Xopen
            [`dd`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/dd.html)(1)
            EBCDIC -&gt; ASCII.

        [`a2i`]()
        : ASCII -&gt; Xopen
            [`dd`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/dd.html)(1) IBM.

        [`i2a`]()
        : Xopen
            [`dd`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/dd.html)(1)
            IBM -&gt; ASCII.

        [`a2o`]()
        : ASCII -&gt; IBM OpenEdition.

        [`o2a`]()
        : IBM OpenEdition -&gt; ASCII.

        [`a2s`]()
        : ASCII -&gt; Siemens Posix-bc.

        [`s2a`]()
        : Siemens Posix-bc -&gt; ASCII.

        [`a2h`]()
        : ASCII -&gt; IBM-37 AS/400.

        [`h2a`]()
        : IBM-37 AS/400 -&gt; ASCII.

        [`-`]()
        : Identity mapping.

    [`mtf`]()
    : Move-to-front transform. The arguments are:

        [`0`]()
        : Pure move-to-front strategy.

        [`-`]()
        : Move-to-front with prediction.

    [`rle`]()
    : Run-length encoding. The arguments are:

        [`0`]()
        : Run-length-encoding: 0-sequences only.

        [`1`]()
        : Run-length-encoding: 0&1-sequences only.

        [`2`]()
        : Run-length-encoding: Alphabet has only two letters.

        [`-`]()
        : General run-length-encoding.

    [`strip`]()
    : \
        Strip head and tail data. The arguments are:

        [`nl`]()
        : Data is line-oriented

        [`head`]()
        : Header to strip is 'head=amount'

        [`tail`]()
        : Tail to strip is 'tail=amount'

        [`-`]()
        : Not stripping anything, only processing 'nl' if specified

    [`transpose`]()
    : \
        Transposing a table. The arguments are:

        [`rsep`]()
        : Rows are separated by 'rsep=character'.

        [`fsep`]()
        : This is equivalent to 'rsep'.

        [`columns`]()
        : \
            Number of columns is defined by 'columns=length'.

        [`0`]()
        : Only transposed data are coded, not meta-data.

        [`-`]()
        : Both transposed data and meta-data are coded.

    [`table`]()
    : \
        Fixed-length record table transform. The arguments are:

        [`columns`]()
        : \
            Number of columns is defined as 'columns=length'.

        [`left`]()
        : Use left to right column dependency (default).

        [`right`]()
        : \
            Use right to left column dependency.

        [`both`]()
        : Use both sides column dependency.

        [`rle`]()
        : Use run-length entropy (default).

        [`cee`]()
        : Use conditional empirical entropy.

        [`single`]()
        : \
            Use a single predictor.

    [`sum`]()
    : Checksumming data. The arguments are:

        [`aes`]()
        : AES digest, aes=size to set size

        [`md5`]()
        : MD5 digest, md5=size to set size

        [`crc`]()
        : CRC digest, crc=size to set size

        [`-`]()
        : Default CRC digest

    [`ss7`]()
    : Partitioning SS7 data into same-length groups. The arguments
        are:

        [`sid`]()
        : SS7 data with Session ID.

        [`-`]()
        : Plain SS7 data.

    [`sieve`]()
    : \
        (Delta) Compression via sieving. The arguments are:

        [`delta`]()
        : \
            Delta compression with approximate matching.

        [`reverse`]()
        : \
            Allowing reverse matching.

        [`map`]()
        : Specifying byte pairs to map for matching.

        [`mmin`]()
        : Setting amount of exact match before approximate matching.

        [`-`]()
        : Delta compression with exact matching.

    [`rtable`]()
    : \
        Transform/compress relational table data. The arguments are:

        [`fsep`]()
        : Fields are separated by 'fsep=character'

        [`rsep`]()
        : Records are separated by 'rsep=character'

        [`schema`]()
        : \
            Schema is defined as 'schema=\[fldlen1,fldlen2,...\]'

        [`-`]()
        : Field and record separators to be computed.

    [`rdb`]()
    : Transforming relational data by field dependency. The arguments
        are:

        [`fsep`]()
        : Field separator is defined as 'fsep=character'.

        [`rsep`]()
        : Record separator is defined as 'rsep=character'.

        [`schema`]()
        : \
            Schema is defined as 'schema=\[fldlen1,fldlen2,...\]'.

        [`plain`]()
        : \
            No reordering of field data based on dependency.

        [`pad`]()
        : Padding fields to uniform lengths.

        [`whole`]()
        : \
            Whole table is output or for secondary procesing.

        [`-`]()
        : Field and record separators to be computed.

    [`netflow`]()
    : \
        Netflow data from Cisco routers.

    [`crypt`]()
    : \
        Encrypting data. The arguments are:

        [`aes128`]()
        : \
            128-bit Advanced Encryption Standard

        [`aes192`]()
        : \
            192-bit Advanced Encryption Standard

        [`aes256`]()
        : \
            256-bit Advanced Encryption Standard

        [`-`]()
        : Default 128-bit Advanced Encryption Standard

    [`bdw`]()
    : Partitioning AMA record groups.

    [`amadiff`]()
    : \
        Xor-ing rows in an AMA table.

    [`ama`]()
    : Partitioning AMA records or text lines into same-length groups.
        The arguments are:

        [`nl`]()
        : Text records output without new-lines

        [`nls`]()
        : Text records output with new-lines

        [`-`]()
        : Records have header bytes for sizes

    [`b`]()
    : Equivalent to `bwt,mtf,rle.0,huffgroup`.

    [`delta`]()
    : \
        Equivalent to `sieve.delta,bwt,mtf,rle.0,huffgroup`.

    [`dna`]()
    : Equivalent to `sieve.reverse.map=ATGCatgc,huffgroup`.

    [`fixedrdb`]()
    : \
        Equivalent to `rdb.full,table,mtf,rle.0,huffgroup`.

    [`flatrdb`]()
    : \
        Equivalent to `rdb,bwt,mtf,rle.0,huffgroup`.

    [`netflow`]()
    : \
        Equivalent to `netflow,mtf,rle.0,huffgroup`.

    [`q`]()
    : Equivalent to `transpose,rle,huffman`.

    [`qnl`]()
    : Equivalent to `ama.nl,transpose,rle,huffman`.

    [`qv`]()
    : Equivalent to `ama,transpose,rle,huffman`.

    [`rt`]()
    : Equivalent to `rtable,mtf,rle.0,huffgroup`.

    [`rte`]()
    : Equivalent to
        `strip.nl.head=1.tail=1,rdb.pad.plain.whole,table,mtf,rle.0,huffgroup`.

    [`t`]()
    : Equivalent to `table,mtf,rle.0,huffgroup`.

    [`tbdw`]()
    : Equivalent to `bdw,ama,table,mtf,rle.0,huffgroup`.

    [`tnl`]()
    : Equivalent to `ama.nl,table,mtf,rle.0,huffgroup`.

    [`tnls`]()
    : Equivalent to `ama.nls,rtable,mtf,rle.0,huffgroup`.

    [`tss7`]()
    : Equivalent to `ss7,table,mtf,rle.0,huffpart`.

    [`tv`]()
    : Equivalent to `ama,table,mtf,rle.0,huffgroup`.

    [`vcdiff|ietf`]()
    : \
        Encode as defined in IETF RFC3284.

The default value is `delta,huffgroup`.\
-`o`, --`output`=`file`
:   Output data is written to `file` instead of the standard output.

-`p`, --`plain`
:   Do not encode transformation information in the data. This means the
    transform must be explicitly supplied to decode.

-`q`, --`identify`
:   Identify the standard input encoding and write the `--method`
    transformation string on the standard output. If the standard input
    is not vczip encoded then nothing is printed.

-`t`, --`transform`=`\[&lt;&gt;\]method\[-arg...\]...`
:   Apply the
    [`codex`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/codex.html)(3)
    data transform around the
    [`vcodex`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/vcodex.html)(3) transform.
    A codex transform is a catenation of the following methods, each
    method prefixed by `&lt;` to decode the input or `&gt;` to
    encode the output. Method arguments, if any, must be prefixed by
    `-`. The method are:

    [`uu`]()
    : uuencode printable encoding.

        [`posix`]()
        : \
            Posix
            [`uuencode`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/uuencode.html)(1).
            This is the default.

        [`base64|mime`]()
        : \
            MIME base64 encoding.

        [`bsd|ucb`]()
        : \
            BSD
            [`uuencode`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/uuencode.html)(1).

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
            &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030253/mailto:glenn.s.fowler@gmail.com)&gt;

    [`qp`]()
    : quoted printable encoding.

        [``(version)]()
        : \
            codex-qp (AT&T Research) 1998-11-11

        [``(author)]()
        : \
            Glenn Fowler
            &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030253/mailto:glenn.s.fowler@gmail.com)&gt;

    [`rot13`]()
    : \
        rot13 self-inverting encoding.

        [``(version)]()
        : \
            codex-rot13 (AT&T Research) 2003-12-11

        [``(author)]()
        : \
            Glenn Fowler
            &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030253/mailto:glenn.s.fowler@gmail.com)&gt;

    [`iconv`]()
    : \
        iconv character codeset conversion. One or two character codeset
        options must be specified. Two options specify the source and
        destination codesets. One option specifies the decode source or
        encode destination codeset; the implied second codeset defaults
        to `native`.

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
            &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030253/mailto:glenn.s.fowler@gmail.com)&gt;

    [`aes`]()
    : AES (FIPS-197 rijndael) encryption. The first option is the
        block size in bits. Sizes { 128 192 256 } are supported. The
        default is 256.

        [``(author)]()
        : \
            Peter Selinger (ccrypt)

        [``(license)]()
        : \
            GPL

    [`bzip` (ident)]()
    : \
        bzip2 compression. The first parameter is the compression level,
        1:least, 9:most(default).

    [`compress` (ident)]()
    : \
        compress LZW compression. The first parameter is the maximum
        number of bits per code { 9 - 16 }. The default is 16.

    [`crypt-rar`]()
    : \
        `rar` encryption. The first option is the `rar`
        implementation version. Versions { 13 15 20 } are supported.

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

    [`crypt-zip`]()
    : \
        zip encryption. The encryption is asymmetric.

    [`gzip` (ident)]()
    : \
        gzip compression. The first parameter is the compression level,
        1:least, 9:most(default). nocrc disables crc checks.

    [`lzd` (decode)]()
    : \
        [`zoo`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/zoo.html)(1)
        archive lzd compression.

        [``(version)]()
        : \
            codex-lzd 1991-07-07

        [``(author)]()
        : \
            Rahul Dhesi

    [`lzh` (decode)]()
    : \
        lzh compression. The options are ordered. A single option alias
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

    [`lzx` (decode)]()
    : \
        Microsoft cabinet archive lzx compression from cabextract 0.6.
        The first parameter is the window size which must be a power of
        2 between 32k and 2m inclusive. The second parameter is the
        optional block aligment; 32k is required for cabinet
        file decompression.

    [`quantum` (decode)]()
    : \
        Microsoft cabinet archive quantum compression from cabextract
        0.6. The first parameter is the window size which must be a
        power of 2 between 1k and 2m inclusive. The second parameter is
        the optional block aligment; 32k is required for cabinet
        file decompression.

    [`rar` (decode)]()
    : \
        [`rar`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/rar.html)(1)
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

    [`sum`]()
    : checksum filter. The checksum value returned by
        [`codexdata`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/codexdata.html)(3)
        is written to the standard error.

        [`att|sys5|s5|default`]()
        : \
            The system 5 release 4 checksum. This is the default for
            `sum` when `getconf UNIVERSE` is `att`. This is the
            only true sum; all of the other methods are order dependent.

        [`ast4|32x4|tw`]()
        : \
            The `ast` 128 bit PRNG hash generated by catenating 4
            separate 32 bit PNRG hashes. The block count is not printed.

        [`bsd|ucb`]()
        : \
            The BSD checksum.

        [`crc`]()
        : 32 bit CRC (cyclic redundancy check).

            [`polynomial=`mask``]()
            : \
                The 32 bit crc polynomial bitmask with implicit bit 32.
                The default value is `0xedb88320`.

            [`done\[=`number`\]`]()
            : \
                XOR the final crc value with `number`. 0xffffffff is
                used if `number` is omitted. The option value may
                be omitted. The default value is `0`.

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
                Include the total number of bytes in the crc. `number`,
                if specified, is first XOR'd into the size. The option
                value may be omitted. The default value is `0`.

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
            The RSA Data Security, Inc. MD5 Message-Digest Method,
            1991-2, used with permission. The block count is
            not printed.

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
                &lt;[steve@edmweb.com](https://web.archive.org/web/20141128030253/mailto:steve@edmweb.com)&gt;

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
            The posix 1003.2-1992 32 bit crc checksum. This is the
            default
            [`cksum`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/cksum.html)(1) method.
            Shorthand for `crc-0x04c11db7-rotate-done-size` .

        [`zip`]()
        : The
            [`zip`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/zip.html)(1) crc.
            Shorthand for `crc-0xedb88320-init-done` .

        [`fddi`]()
        : The FDDI crc. Shorthand for
            `crc-0xedb88320-size=0xcc55cc55`.

        [`fnv|fnv1`]()
        : \
            The Fowler-Noll-Vo 32 bit PRNG hash with non-zero
            initializer (FNV-1). Shorthand for
            `prng-0x01000193-init=0x811c9dc5`.

        [`ast|strsum`]()
        : \
            The `ast`
            [`strsum`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/strsum.html)(3)
            PRNG hash. Shorthand for `prng-0x63c63cd9-add=0x9c39c33d`.

        [``(version)]()
        : \
            codex-sum (AT&T Research) 2003-12-16

        [``(author)]()
        : \
            Glenn Fowler
            &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030253/mailto:glenn.s.fowler@gmail.com)&gt;

    [`zip`]()
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

-`u`, --`undo|decode`
:   Decode data.

-`v`, --`verbose`
:   List the compresses size on the standard error.

-`w`, --`window`=`window\[,method\]`
:   Set the data partition window size to `window`. `method` specifies
    an optional window matching method. The window methods are:

    [`prefix`]()
    : \
        Find windows with matching prefixes.

    [`mirror`]()
    : \
        Mirroring positions across files.

    [`vote`]()
    : Find windows by voting for matches.

-`d`, --`vcdiff|ietf`
:   Encode as defined in IETF RFC3284. Obsolete -- use --method=ietf.

-`D`, --`debug`=`level`
:   Set the debug trace level to `level`. Higher levels produce
    more output.

-`M`, --`move`
:   Use sfmove() for io.

-`P`, --`pause`
:   Debug: print the pid and sleep(10); then continue processing.

# FILES

`../lib/vcodex/aliases`
:   `--method` `name=value` alias file, found on `\$PATH` .

# SEE ALSO

[`codex`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man1/codex.html)(1),
[`codex`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/codex.html)(3),
[`vcodex`](/web/20141128030253/http://www2.research.att.com/~astopen/man/man3/vcodex.html)(3)

# IMPLEMENTATION

`version`
:   vczip (AT&T Research) 2009-10-01

`author`
:   Phong Vo
    &lt;[kpv@research.att.com](https://web.archive.org/web/20141128030253/mailto:kpv@research.att.com)&gt;

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030253/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 2003-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030253/http://www.eclipse.org/org/documents/epl-v10.html)


