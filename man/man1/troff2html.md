# NAME

troff2html - convert troff/groff input to html

# SYNOPSIS

`troff2html` \[ `options` \] \[ file ... \]

# DESCRIPTION

`troff2html` converts
[`troff`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/troff.html)(1)
(or
[`groff`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/groff.html)(1),
depending on the processing mode) input documents to an `html`
document on the standard output. Although a full `troff` parse is done,
many features are ignored in the mapping to `html`.
The `troff` `t` condition test evaluates `true`, the `n` condition
tests evaluates `false`, and the `groff` compatibility register
`\\\\n\[.C\]` evaluates to 0 (enable `groff` parsing) if it is
referenced before the first `groff` `.cp` (compatibility mode)
request.

The generated `html` has properly nested begin/end tags, even though
most browsers don't care.

# OPTIONS

-`i`, --`identify`=`file`
:   Reads identification options from `file`. Unknown options are
    silently ignored. See the `.xx` request below for a description of
    the options.

-`I`, --`include`=`directory`
:   Appends `directory` to the list of directories searched for
    `--macros` and `.so` request files.

-`m`, --`macros`=`package`
:   Locates and reads the macro package file `package`. In order to
    accomodate different `troff` installation styles the file search
    order is fairly involved: [`./package`]()
    [`directory/package`]()
: for all `--include` directories [`directory/tmac.package`]()
: for all `--include` directories [`../lib/tmac/tmac.package`]()
: for all directories on `\$PATH` [`../lib/html/package`]()
: for all directories on `\$PATH` [`../lib/html/mpackage.tr`]()
: for all directories on `\$PATH`
    [`../share/groff/tmac/tmac.package`]()
: for all directories on `\$PATH`
    [`../groff/share/groff/tmac/tmac.package`]()
: for all directories on `\$PATH`

-`r`, --`register`=`registerN`
:   Initializes the number `register` to `N`.

-`s`, --`script`=`script`
:   Reads `script` as if it came from a file. `--script='.nr A 123'`
    is equivalent to `-rA123`.

-`v`, --`verbose`
:   Enables verbose error and warning messages. Following `troff`
    tradition, `troff2html` by default does not warn about unknown
    requests; `--verbose` enables such warnings.

# EXTENSIONS

`.xx` `name`\[=`value`\] is a special `troff2html` request that
handles program tracing, `html` extensions and `troff` macro package
magic that went way past the author's willingness to understand.
Supported operations are:

`author=text`
:   Specifies the contact information for the document HEAD section.

`background=URL`
:   Specifies the document background URL.

`debug=level`
:   The debug trace `level`; higher levels produce more output.

`get=+-register`
:   Traces each `get` for the named number `register`. `-` turns
    tracing off.

`hot='word ...'`
:   Adds (`+`) or removes (`-`) `word` ... from the hot-word list.
    Constructs that match (`hot-word` ... `SWITCH-FONT` text
    `SWITCH-FONT` ... ) adds `text` as a hot link to another portion of
    the document. `refer` and `see` are the default hot words. Case
    is ignored when matching hot words.

`logo=URL`
:   Specifies the logo/banner image URL that is centered at the top of
    the document.

`mailto=address`
:   Sets the email `address` to send comments and suggestions.

`meta.name`
:   Emits the `html` tag `&lt;META name=`"`name`"
    `content=`"`content` "`&gt;`.

`package=text`
:   `text` is prepended to the `html` document title.

`set=+-register`
:   Traces each `set` for the named number `register`. `-` turns
    tracing off.

`title=text`
:   Sets the document title.

Local URL links are generated for all top level headings. These can be
referenced by embedding the benign (albeit convoluted) `troff` construct
\\h'0\`\\w"label"'text\\g'0', where `label` is the local link label and
`text` is the hot link text. If `label` and `text` are the same then use
\\h'0\`1'text\\h'0'.

# SEE ALSO

[`groff`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/groff.html)(1),
[`html2rtf`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/html2rtf.html)(1),
[`man`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/man.html)(1),
[`mm`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/mm.html)(1),
[`mm2html`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/mm2html.html)(1),
[`troff`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/troff.html)(1)

# IMPLEMENTATION

`version`
:   troff2html (AT&T Research) 2004-04-26

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1996-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030252/http://www.eclipse.org/org/documents/epl-v10.html)


