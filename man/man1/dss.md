# NAME

dss - scan a data stream and apply a select expression to each record

# SYNOPSIS

`dss` \[ `options` \] \[ expression \] \[ file ... \]

# DESCRIPTION

`dss` scans a record-oriented data stream, applies a select
`expression` to each record, and writes the matching records to the
standard output. If `expression` is `-` or empty then all records
match. If `expression` begins with `&lt;` then the remainder of the
expression is a file containing the expression. If `file` is `-` or
omitted then the standard input is read. If `file` begins with `&lt;`
then the string with `&lt;` removed is a file containing a
newline-separated list of files to process. If |{`write` `format`}is
not specified then the output format is the same as the format of the
first input `file`.
Input files are
[`vczip`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/vczip.html)(1),
[`gzip`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1),
[`bzip2`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/bzip2.html)(1)
or
[`pzip`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1)
decompressed if necessary.

# EXPRESSIONS

Query expressions support C-style syntax. Strings may be specified with
'...', "..." or /.../ delimiters. `=\~` and `!\~` operations on
strings treat the right hand operand as a possibly field-specific
matching pattern. `string` field matching patterns are extended
[`regex`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man3/regex.html)(3)
regular expressions
([`egrep`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/egrep.html)(1)
style.)
Types, queries and functions are brought into scope by `--library`
references on the command line, library references within schema
definitions, or by explicit `lib`::`identifier` binding within
expressions. Variables and function return values within expressions and
`{print}` formats may be cast to another type using C style casts
(`lib`::`type`) and (`type` ).

An expression of the form { `query` \[--`option`...\] \[`arg`...\]
\[&gt; `output`\] } accesses the compiled `query` defined in a
`--library` dynamic library. { `query` `--man` } lists the
documentation for `query`.

Dynamic queries enclosed in {...} and interpreted queries enclosed in
(...) may be composed using the `|`, `?:`, and `;` operators.
`A`|`B` specifies that query `B` processes records selected by query
`A`. `A`?`B`:`C` specifies that query `B` processes the records selected
by query `A` and query `C` processes the records not selected by query
`A`; query `B` may be omitted. `A`;`B` specifies that queries `A` and
`B` process the same records.

`NOTE:`
:   Specify `--method`=`method` for a list of supported `formats and
    variables`.

# OPTIONS

-`a`, --`append`
:   Open output files in append mode. This disables file header output.

-`d`, --`debug`
:   Enable debug tracing.

-`I`, --`include`=`dir`
:   Add `dir` to the list of directories searched for include files. The
    default `../lib/dss` directories on `\$PATH` are added to
    this list.

-`l`, --`library`=`name`
:   Load the dynamic library `name`. `dss` libraries may define
    methods, types, maps, queries or functions.

-`m`, --`map`=`file`
:   Numeric field value map XML file. `--method=dss,man` describes the
    `&lt;MAP&gt;` tag.

-`P`, --`plugins`=`style`
:   List plugin information for each `file` operand in --`style` on the
    standard error. The `expression` operand is not specified in
    this case. If no `file` operands are specified then the first
    instance of each `dss` plugin installed on `\$PATH` or a sibling
    dir on `\$PATH` is listed. The special `style` `list` lists a
    line on the standard output for each plugin with the name, a tab
    character, and plugin specific command line options parameterized by
    `\${style}` (suitable for `eval`'ing in
    [`sh`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/sh.html)(1).)
    The default value is `list|man|html|nroff|usage`.

-`q`, --`quiet`
:   Disable non-fatal warning messages.

-`v`, --`verbose`
:   Enable verbose status messages.

-`x`, --`method`=`method\[,option\[=value\]...\]\[:schema\]`
:   Set the record method. This option must be specified. The method
    name may be followed by a , separated list of method specific
    `\[no\]name\[=value\]` options and a schema following the first :.
    Method specific usage may be listed by the `man` or `html`
    method specific options. Each method is typically implemented in a
    separate shared library. If the method shared library is not
    installed on `\$PATH` or a sibling dir on `\$PATH` then `method`
    must be the full path name of the shared library. The methods,
    determined by `\$PATH`, are:

    [`dss`]()
    : meta-method that specifies a method, value maps and constraints

    [`bgp`]()
    : BGP router dump and announce/withdraw messages

    [`dibbler`]()
    : \
        at&t ningaui dibbler billing data

    [`flat`]()
    : fixed-width and/or field-delimited flat file data

    [`gdat`]()
    : gigascope data with embedded GDAT schema header

    [`lsa`]()
    : OSPF LSA logs

    [`netflow`]()
    : \
        Cisco router netflow dump data

    [`opaque`]()
    : \
        opaque fixed record data with optional magic

    [`text`]()
    : Newline-terminated field-delimited text file; the method schema
        is a
        [`scanf`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man3/scanf.html)(3)
        like format string with embedded field names of the form:
        %(field1)format-char delimiter ...

    [`xml`]()
    : xml and json method

-`T`, --`test`=`mask`
:   Enable test code defined by `mask`. Test code is
    implementation specific.

    [`0x00f0`]()
    : \
        method specific tests

    [`0x0f00`]()
    : \
        cx library specific tests

    [`0x0100`]()
    : \
        enable cxeval() code trace

    [`0xf000`]()
    : \
        dss library specific tests

-`c`, --`count`
:   Write the `matched/total` records on the standard output.
    Deprecated: compose the expression with |{`count`} instead.

-`f`, --`format`=`format`
:   Set the output method format. Deprecated: compose the expression
    with |{`write` `format`} instead.

-`n`, --`nooutput`
:   Disable all output. Deprecated: not required when the expression
    contains a dynamic query.

-`p`, --`print`=`format`
:   Print selected records according to `format`. Deprecated: compose
    the expression with |{`print` `format`} instead.

# EXAMPLES

`dss -x dss '{stats --man}'`
:   List the `stats` query manpage.

`dss -x bgp '{write --man}'`
:   List the formats supported by the `bgp` method.

`dss -x netflow "{stats --group=prot bytes packets}" \`.gz`
:   List the stats for the `netflow` method fields `bytes` and
    `packets`, grouped by values in the field `prot`.

`dss -x bgp {count} cisco.dat`
:   Count the number of `bgp` records in `cisco.dat` .

`dss -x bgp '`(type=="A")?{write table &gt; a}:{write cisco &gt; b}' mrt.dat
:   Write the announce records from `mrt.dat` to the file `a` in the
    `table` format and all other records to the file `b` in the
    `cisco` format.

`dss -x foo-txt '{flat foo-bin}|{compress}' foo.txt &gt; foo.bin`
:   Convert the `foo-txt` file `foo.txt` to the `foo-bin` `flat`
    method format file `foo.bin` using the preferred compression
    method, where `foo-txt.dss` and `foo-bin.dss` are user supplied
    `dss` XML schema files describing the input and output formats.

`dss -x foo-bin '`(time&gt;="jan 1")|{flat foo-txt}' foo.bin
:   Select all `foo.bin` records with `time` &gt; jan 1 and list
    them in the `foo-txt` format.

# SEE ALSO

[`vczip`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/vczip.html)(1),
[`gzip`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1),
[`bzip2`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/bzip2.html)(1),
[`pzip`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/pzip.html)(1),
[`cql`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man1/cql.html)(1),
[`dss::dss`](/web/20150717160617/http://www2.research.att.com/~astopen/man/man5P/dss-dss.html)(5P)

# IMPLEMENTATION

`version`
:   dss (AT&T Research) 2011-09-11

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 2002-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150717160617/http://www.eclipse.org/org/documents/epl-v10.html)


