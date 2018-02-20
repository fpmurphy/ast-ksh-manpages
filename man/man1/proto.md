# NAME

proto - make prototyped C source compatible with K&R, ANSI and C++

# SYNOPSIS

`proto` \[ `options` \] file ...

# DESCRIPTION

`proto` converts ANSI C prototype constructs in `file` to constructs
compatible with K&R C, ANSI C, and C++. Only files with the line
`\#pragma prototyped` appearing in one of the first 64 lines are
processed; other files are silently ignored. Output is written to the
standard output unless the `--replace` option is specified, in which
case `file` is modified in-place.

# OPTIONS

-`c`, --`comment`=`bme`
:   `b\[m\[e\]\]` are the beginning, middle, and end comment characters.
    If `e` is omitted then it defaults to `b`. If `m` is omitted then it
    defaults to `b`. Use "`/\``" for C comments, "`\#`" for shell,
    and "`(\`)`" for pascal. If `bme` is "" (the empty string) then
    the comment style is determined from the input `file` suffix; no
    notice is prepended if the comment style cannot be determined. The
    default value is `"/\`"`.

-`d`, --`disable`
:   Disable prototype conversion but still emit the
    identification comment.

-`e`, --`externs`=`package`
:   All `extern` references are for `package`. Some systems require
    special attributes for imported and exported dll data symbols. If
    `\_BLD\_``package` is not defined then `extern` data references
    will be assigned the dll import attribute when supported by the
    local compiler.

-`f`, --`force`
:   Force conversion for files that do not contain `\#pragma
    prototyped`.

-`h`, --`header`
:   Emit the `proto` header definition preamble. On by default; -`h`
    means --`noheader`.

-`i`, --`inverse`
:   Specifies inverse proto: classic function definitions are converted
    to ANSI prototype form and non-ANSI directives are commented out. In
    this case files with the line `\#pragma noprototyped` within the
    first 64 lines are silently ignored. If `--header` is also
    specified then only `extern` prototypes are emitted for each
    non-static function. This option requires that all classic function
    formal arguments be declared, i.e., omitted declarations for `int`
    formals will not generate the correct prototype. Typical usage would
    be to first run `proto --inverse --header \`.c` to generate the
    external prototypes that should be placed in a `.h` file shared by
    `\`.c` and then `proto --inverse --replace \`.c` to convert the
    function prototypes in place. Note that prototype code conditioned
    on `\_\_STDC\_\_` will most likely confuse `--inverse` .

-`l`, --`license`=`file`
:   Generate a license notice comment at the top of the output
    controlled by one or more `name`=`value` pairs in `file`. If a
    `value` contains space characters then it must be enclosed in either
    single or double quotes. `name` may be:

    [`type`]()
    : The license type:

        [`bsd`]()
        : The BSD open source license.

        [`cpl`]()
        : The Common Public License.

        [`epl`]()
        : The Eclipse Public License.

        [`gpl`]()
        : The GNU Public License.

        [`mit`]()
        : The MIT open source license.

        [`inline`]()
        : \
            License text already in source.

        [`none`]()
        : No license.

        [`noncommercial`]()
        : \
            Non-commercial use.

        [`nonexclusive`]()
        : \
            Single person non-commercial use.

        [`open`]()
        : Open source.

        [`proprietary`]()
        : \
            Only by individual agreement.

        [`special`]()
        : \
            License text in `notice`.

        [`usage`]()
        : \
            License specific
            [`optget`](/web/20150527154245/http://www2.research.att.com/~astopen/man/man3/optget.html)(3)
            usage strings.

        [`verbose`]()
        : \
            Include the disclaimer notice if any.

        [`zlib`]()
        : The ZLIB open source license.

    [`author`]()
    : \
        A `,` separated list of `name` &lt;`email`&gt; pairs.

    [`class`]()
    : \
        The license class. The default values are:

        [`gpl`]()
        : The GNU Public License.

        [`open`]()
        : `www.opensource.org` sanctioned open source.

        [`proprietary`]()
        : \
            Internal or non-disclosure use only.

        [`special`]()
        : \
            Nonstandard license text and notices.

    [`corporation`]()
    : \
        Within the parent, e.g., `AT&T`.

    [`company`]()
    : \
        Within the corporation, e.g., `Research`.

    [`location`]()
    : \
        Company location.

    [`organization`]()
    : \
        Within the company, e.g., `Network Services Research
        Department`.

    [`notice`]()
    : \
        `type=special` notice text with embedded newlines or
        additional notice text listed by `type=verbose`.

    [`package`]()
    : \
        The generic software package name, e.g., `ast`.

    [`parent`]()
    : \
        They own it all, e.g., `AT&T`.

    [`since`]()
    : \
        The year the software was first released.

    [`source`]()
    : \
        The year the input files was modified.

    [`start`]()
    : \
        The year the license was first applied to the software.

    [`url`]()
    : The URL of the detailed license text, e.g.,
        `http://www.research.att.com/sw/license/open-ast.html` .

    [`urlmd5`]()
    : \
        The
        [`md5sum`](/web/20150527154245/http://www2.research.att.com/~astopen/man/man1/md5sum.html)(1)
        of the downloaded URL data. Note that the downloaded data may
        have embedded `\\r` not present in the original source.

    [`query=``text`]()
    : \
        If `text` is one of the `name`s above then its value is
        expanded, otherwise `\${``name``}` in `text` is expanded.
        The result is printed as a line on the standard output and
        `proto` exits. This should only be used via `--options`.

-`n`, --`sync`
:   Output C style line syncs to retain the original line structure.

-`o`, --`options`=`name=value,...`
:   Additional space or `,` separated `name=value`
    `--license` options.

-`p`, --`pass`
:   Pass input to output, even if not converted.

-`r`, --`replace`
:   Process the input files in place; original information is replaced
    by `proto` output.

-`s`, --`include`
:   Output `\#include &lt;prototyped.h&gt;` rather than expanding the
    equivalent inline.

-`t`, --`test`
:   Enable test code. Use at your own risk.

-`v`, --`verbose`
:   List each file as it is processed.

-`x`, --`externalize`
:   Convert `static` function attributes to `extern`. Used for
    analysis programs that only instrument `extern` functions.

-`z`, --`zap`
:   Disable conversion and remove `\#pragma prototyped`.

-`C`, --`copy`=`directory`
:   Convert each input `file` to `directory`/`file`, making intermediate
    directories as necessary.

-`L`, --`list`=`file`
:   Input file names are read one per line from `file`.

-`P|+`, --`plusplus`
:   Convert `extern()` to `extern(...)`.

-`S`, --`shell`
:   Equivalent to `--comment="\#".`

# SEE ALSO

[`cc`](/web/20150527154245/http://www2.research.att.com/~astopen/man/man1/cc.html)(1),
[`cpp`](/web/20150527154245/http://www2.research.att.com/~astopen/man/man1/cpp.html)(1)

# IMPLEMENTATION

`version`
:   proto (AT&T Research) 2012-02-20

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1990-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150527154245/http://www.eclipse.org/org/documents/epl-v10.html)


