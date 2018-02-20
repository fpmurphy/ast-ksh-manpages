# NAME

nl - line numbering filter

# SYNOPSIS

`nl` \[ `options` \] \[file\]

# DESCRIPTION

`nl` reads lines from the file `file` or from standard input if `file`
is omitted or is `-`, and writes the lines to standard output with
possible line numbering preceding each line.
The `nl` utility treats its input in terms of logical pages and resets
numbering on each logical page. A logical page consists of a header, a
body, and a footer any of which can be empty, and each can use their own
line numbering options.

The start of logical page sections consist of input lines containing
only the two delimiter characters whose defaults are `\\` and `:` as
follows:

`d1d2d1d2d1d2`
:   Header.

`d1d2d1d2`
:   Body.

`d1d2`
: Footer.

`nl` assumes that the first section is a logical body until it
encounters one of the section delimiters.

# OPTIONS

-`b`, --`body-numbering`=`type`
:   `type` can be one of the following:

    [`a`]()
    : Number all lines.

    [`t`]()
    : Number only non-empty lines.

    [`n`]()
    : No line numbering.

    [`p``string`]()
    : \
        Number only lines that contain the basic regular expression
        `string`.

The default value is `t`.\
-`d`, --`section-delimiter`=`delim`
:   `delim` specifies the two delimiter characters that indicate start
    of a section. If only one character is specified, the second
    character remains unchanged. The default value is `\\:`.

-`f`, --`footer-numbering`=`type`
:   `type` is the same as for the `b` option. The default value is
    `n` .

-`h`, --`header-numbering`=`type`
:   `type` is the same as for the `b` option. The default value is
    `n` .

-`i`, --`page-increment`=`incr`
:   `incr` is the increment used to number logical page lines. The
    default value is `1`.

-`l`, --`join-blank-lines`=`num`
:   `num` is the number of blank lines to be treated as one The default
    value is `1`.

-`n`, --`number-format`=`format`
:   `format` specifies the line numbering format. It must be one of the
    following:

    [`ln`]()
    : left justified, leading zeros supressed.

    [`rn`]()
    : right justified, leading zeros supressed.

    [`rz`]()
    : right justified, leading zeros kept.

-`p`, --`no-renumber`
:   Start renumbering at logical page delimiters.

-`s`, --`number-separator`=`sep`
:   `sep` is the string that is used to separate the line number and the
    corresponding text line. The default value is `\\t`.

-`v`, --`starting-line-number`=`startnum`
:   `startnum` is the initial value to number logical pages. The default
    value is `1`.

-`w`, --`number-width`=`width`
:   `width` is the number of characters to be used for line numbering.
    The default value is `6`.

# EXIT STATUS

`0`
: Success.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`pr`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/pr.html)(1),
[`regex`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man3/regex.html)(3)

# IMPLEMENTATION

`version`
:   nl (AT&T Research) 2003-03-24

`author`
:   David Korn

`copyright`
:   Copyright © 2003-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030247/http://www.eclipse.org/org/documents/epl-v10.html)


