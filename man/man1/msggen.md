# NAME

msggen - generate a machine independent formatted message catalog

# SYNOPSIS

`msggen` \[ `options` \] catfile \[ msgfile \]

# DESCRIPTION

`msggen` merges the message text source files `msgfile` into a machine
independent formatted message catalog `catfile` . The file `catfile`
will be created if it does not already exist. If `catfile` does exist,
its messages will be included in the new `catfile`. If set and message
numbers collide, the new message text defined in `msgfile` will replace
the old message text currently contained in `catfile`. Non-ASCII
characters must be UTF-8 encoded.
[`iconv`](/web/20150528150201/http://www2.research.att.com/~astopen/man/man1/iconv.html)(1)
can be used to convert to/from UTF-8.

# OPTIONS

-`f`, --`format`
\
List the
[`printf`](/web/20150528150201/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
format signature for each message in `catfile`. A format signature is
one line containing one character per format specification:
[`c`]()
char
[`d`]()
double
[`D`]()
long double
[`f`]()
float
[`h`]()
short
[`i`]()
int
[`j`]()
long long
[`l`]()
long
[`p`]()
void\`
[`s`]()
string
[`t`]()
ptrdiff\_t
[`z`]()
size\_t
[`?unknown`]()
-`l`, --`list`
\
List `catfile` in UTF-8 `msgfile` form.
-`s`, --`set`
\
Convert the `catfile` operand to a message set number and print the
number on the standard output.

# EXTENDED DESCRIPTION

Message text source files are in
[`gencat`](/web/20150528150201/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1)
format, defined as follows. Note that the fields of a message text
source line are separated by a single blank character. Any other blank
characters are considered as being part of the subsequent field. The
`NL\_\`` constants are defined in one or both of `&lt;limits.h&gt;`
and `&lt;nl\_types.h&gt;` .

`\$` `comment`
:   A line beginning with `\$` followed by a blank character is
    treated as a comment.

`\$delset` `n` `comment`
:   This line deletes message set `n` from an existing message catalog.
    `n` denotes the set number \[1, `NL\_SETMAX`\]. Any text following
    the set number is treated as a comment.

`\$quote` `c`
:   This line specifies an optional quote character `c`, which can be
    used to surround `message-text` so that trailing spaces or empty
    messages are visible in a message source line. By default, or if an
    empty `\$quote` directive is supplied, no quoting of
    `message-text` will be recognized.

`\$set` `n` `comment`
:   This line specifies the set identifier of the following messages
    until the next `\$set` or end-of-file appears. `n` denotes the set
    identifier, which is defined as a number in the range \[1, `NL\_SETMAX`\]. Set numbers need not be contiguous. Any text
    following the set identifier is treated as a comment. If no
    `\$set` directive is specified in a message text source file, all
    messages will be located in message set `1`.

`\$translation` `identification` `YYYY-MM-DD`\[,...\]
:   Append translation info to the message catalog header. Only the
    newest date for a given `identification` is retained in the catalog.
    Multiple translation lines are combined into a single `,`
    separated list.

`m` `message-text`
:   `m` denotes the message identifier, which is defined as a number in
    the range \[1, `NL\_MSGMAX`\]. The message-text is stored in the
    message catalogue with the set identifier specified by the last
    `\$set` directive, and with message identifier `m`. If the
    `message-text` is empty, and a blank character field separator is
    present, an empty string is stored in the message catalogue. If a
    message source line has a message number, but neither a field
    separator nor `message-text`, the existing message with that number
    (if any) is deleted from the catalogue. Message identifiers need not
    be contiguous. There are no `message-text` length restrictions.

# SEE ALSO

[`gencat`](/web/20150528150201/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1),
[`iconv`](/web/20150528150201/http://www2.research.att.com/~astopen/man/man1/iconv.html)(1),
[`msgcc`](/web/20150528150201/http://www2.research.att.com/~astopen/man/man1/msgcc.html)(1),
[`translate`](/web/20150528150201/http://www2.research.att.com/~astopen/man/man1/translate.html)(1),
[`fmtfmt`](/web/20150528150201/http://www2.research.att.com/~astopen/man/man3/fmtfmt.html)(3)

# IMPLEMENTATION

`version`
:   msggen (AT&T Research) 2002-03-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150528150201/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 2000-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150528150201/http://www.eclipse.org/org/documents/epl-v10.html)


