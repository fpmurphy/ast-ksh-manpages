# NAME

mm2html - convert mm/man/mandoc subset to html

# SYNOPSIS

`mm2html` \[ `options` \] \[ \[ dir | file \] ... \]

# DESCRIPTION

`mm2html` is a
[`sed`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/sed.html)(1)/[`ksh`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
script (yes!) that converts input
[`mm`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/mm.html)(1)
or
[`man`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/man.html)(1)
documents to an `html` document on the standard output. If `file` is
omitted then the standard input is read.
[`troff2html`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/troff2html.html)(1)
is similar but does a full
[`troff`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/troff.html)(1)
parse. `dir` operands and directory components of `file` operands are
added to the included file search list.

# OPTIONS

-`f`, --`frame`=`name`
:   Generate framed HTML files in: [`man documents`]()

    [`name``.html`]()
    : \
        The parent frame page.

    [`name``-toc.html`]()
    : \
        The table of contents (link) frame.

    [`name``-man.html`]()
    : \
        The (also standalone) man page frame.

    [`other documents`]()

    [`name``.html`]()
    : \
        The main body.

    [`name``-index.html`]()
    : \
        The frame index (if `--index` specified).

    [`name``-temp.html`]()
    : \
        Temporary frame goto labels.

-`g`, --`global-index`
:   Generate a standalone `index.html` for framed HTML.

-`h`, --`html`=`file\[?name=value;...\]`
:   Read html options from `file`. Unknown options are silently ignored.
    See the `.xx` request below for a description of the options. The
    file pathname may be followed by URL style `name=value` pairs that
    are evaluated as if they came from `file.`

-`l`, --`license`=`file\[?name=value;...\]`
:   Read license identification options from `file`. Unknown options are
    silently ignored. See the `.xx` request below for a description of
    the options. The file pathname may be followed by URL style
    `name=value` pairs that are evaluated as if they came from `file`.

-`o`, --`option`=`\[no\]name=value`
:   Sets a space or `,` separated list of `--license` options.
    Option values with embedded spaces must be quoted.

-`t`, --`top`
:   Open non-local urls in the top frame.

-`x`, --`index`
:   Generate a standalone `name``-index.html` for framed HTML where
    `name` is specified by `--frame`.

# EXTENSIONS

`.xx` `name`\[=`value`\] is a special `mm2html` request that handles
program tracing, `html` extensions and `troff` macro package magic.
Supported operations are:

`author=text`
:   Specifies the contact information for the document HEAD section.

`background=URL`
:   Specifies the document background URL.

`logo=URL`
:   Specifies the logo/banner image URL that is centered at the top of
    the document.

`mailto=address`
:   Sets the email `address` to send comments and suggestions.

`meta.name`
:   Emits the `html` tag `&lt;META name=``name` `content=`
    `content``&gt;`.

`package=text`
:   `text` is prepended to the `html` document title.

`title=text`
:   Sets the document title.

Local URL links are generated for all top level headings. These can be
referenced by embedding the benign (albeit convoluted) `troff` construct
\\h'0\`\\w"label"'text\\h'0', where `label` is the local link label and
`text` is the hot link text. If `label` and `text` are the same then use
\\h'0\`1'text\\h'0'.
[`man`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/man.html)(1)
links are generated for bold or italic identifiers that are immediately
followed by a parenthesized number.

# FILES

`\$HOME/.2html`
:   Default rendering info.

# SEE ALSO

[`troff2html`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/troff2html.html)(1),
[`html2rtf`](/web/20141128030246/http://www2.research.att.com/~astopen/man/man1/html2rtf.html)(1)

# IMPLEMENTATION

`version`
:   mm2html (AT&T Research) 2012-02-29

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030246/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1996-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030246/http://www.eclipse.org/org/documents/epl-v10.html)


