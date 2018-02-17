# NAME

cdb - display cql data files

# SYNOPSIS

`cdb` \[ `options` \] \[ file ... \]

# DESCRIPTION

`cdb` displays
[`cql`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/cql.html)(1)
and
[`cdb`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man3/cdb.html)(3)
data files. Input data information is optional if the input is self
describing. Otherwise the default input format is `flat`, the default
input schema is best guess, and the default input comment is empty. The
default output format is `flat`, the default output schema is the same
as the input schema with external types and virtuals omitted, and the
default output comment is the same as the input comment.

# OPTIONS

-`c`, --`count`
:   Print the total number of records on exit.

-`d`, --`debug`=`level`
:   Set the debug trace `level`. Higher levels produce more output.

-`h`, --`identify`
:   Display header identification information and exit.

-`i`, --`input`\[=`options...`\]
:   The following options describe the input data. Options describe the
    input by default. The option value may be omitted.

-`l`, --`library`=`lib`
:   `lib` is loaded as a runtime `dll`. `lib` must define the function
    `cdb\_init` . See
    [`cdb`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man3/cdb.html)(3).

-`m`, --`methods`
:   List all available methods and exit.

-`o`, --`output`\[=`options...`\]
:   The following options describe the output data. The option value may
    be omitted.

-`B`, --`bufsize`=`size`
:   Sets the data io buffer size to `size`.

-`C`, --`comment`=`string`
:   Sets the data comment to `string`.

-`D`, --`details`=`string`
:   Sets the method details to `string`.

-`X`, --`dump`
:   Enables record level trace messages.

-`F`, --`format`=`name`
:   The data format (method). Formats can be composed using a `:`
    separated list of these names:

    [`cdb`]()
    : For sparse records. `pzip` may perform better.

    [`flat`]()
    : Delimiter separated or fixed width fields, terminator separated
        or fixed length records.

    [`gzip`]()
    : [`gzip`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1) compression.

    [`pzip`]()
    : [`pzip`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1) compression.

    [`vdelta`]()
    : \
        [`vdelta`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/vdelta.html)(1)
        differencing and/or compression.

-`H`, --`header`
:   Generate and/or read data identification header.

-`M`, --`map`=`name`
:   Set the record data map to `name`.

-`P`, --`pack`
:   Set the `CDB\_PACK` hint.

-`R`, --`raw`
:   Display raw record data.

-`S`, --`schema`=`name`
:   Set the record data schema to `name` composed of:

    [`TBD`]()
    : TBD

-`E`, --`terminated`
:   An otherwise fixed length record also has a record terminator.

-`T`, --`test`=`mask`
:   Add the implementation defined `mask` to the data/library test mask.

-`V`, --`verbose`
:   Enable verbose trace messages.

-`W`, --`watch`=`count`
:   Enable `--dump` and `--verbose` after `count` records
    are processed.

# SEE ALSO

[`cql`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/cql.html)(1),
[`gzip`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1),
[`od`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/od.html)(1),
[`pzip`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1),
[`vdelta`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man1/vdelta.html)(1),
[`cdb`](/web/20141128030239/http://www2.research.att.com/~astopen/man/man3/cdb.html)(3)

# IMPLEMENTATION

`version`
:   cdb (AT&T Research) 1999-05-01

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030239/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1991-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030239/http://www.eclipse.org/org/documents/epl-v10.html)


