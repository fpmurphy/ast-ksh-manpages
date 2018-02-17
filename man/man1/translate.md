# NAME

translate - english language/dialect translation filter harness

# SYNOPSIS

`translate` \[ `options` \] \[ dialect,... \[ file ... \] \]

# DESCRIPTION

`translate` is a language/dialect translation filter harness. English
text is read from each `file`, or the standard input if `file` is
omitted, and is translated to the specified `dialect` on the standard
output. The dialect name is the value that may be assigned to the
`LC\_\`` or `LANG` environment variables.
A `,` separated dialect list may be specified. Each `file` is
translated into each `dialect`. The `dialect` `-` names all available
dialects.

If no arguments are specified then the available dialect names are
listed on the standard output and `translate` exits.

Dialects translated via the WWW may require staging files outside the
firewall; this is done by
[`wwwstage`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/wwwstage.html)(1),
which requires either an interactive password prompt or a properly
initialized `\$HOME/.wwwstage` control file.
[`lynx`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/lynx.html)(1)
is used to access external sites.

WWW translation services may have a daily translation quota. No more
submissions are made to a service once the quota is exceeded.

Some of the dialects are `for fun` filters swiped from the net. The
available dialects are:

`bg`
: Bulgarian ..... tranexp

`chef`
: Swedish\_Chef .. filter

`cs`
: Czech ......... tranexp

`cy`
: Welsh ......... tranexp

`da`
: Danish ........ tranexp

`de`
: German ........ babelfish

`el`
: Greek ......... tranexp

`es`
: Spanish ....... babelfish

`fi`
: Finnish ....... tranexp

`fr`
: French ........ babelfish

`fudd`
: Elmer\_Fudd .... filter

`hr`
: Croatian ...... tranexp

`hu`
: Hungarian ..... tranexp

`is`
: Icelandic ..... tranexp

`it`
: Italian ....... babelfish

`nl`
: Dutch ......... tranexp

`no`
: Norwegian ..... tranexp

`piglatin`
:   Pig\_Latin ..... filter

`pl`
: Polish ........ tranexp

`pt`
: Portuguese .... babelfish

`ro`
: Romanian ...... tranexp

`ru`
: Russian ....... tranexp

`sl`
: Slovenian ..... tranexp

`sr`
: Serbian ....... tranexp

`sv`
: Swedish ....... tranexp

`valley`
:   Valley\_Girl ... filter

# OPTIONS

-`a`, --`all`
:   Translate all messages. By default only messages added since the
    last translation are translated.

-`D`, --`debug`
:   Enable debug tracing.

-`c`, --`cached`
:   Update from cached WWW service output files only. These files are
    named `www/\`.www` . Only cached files newer than the
    corresponding message file are checked.

-`f`, --`force`
:   Force translation even if translated files appear to be up to date.

-`i`, --`inverse`
:   Only one `dialect` may be specified; the input file in this dialect
    is translated to English. `filter` dialects do not support
    inverse translation.

-`l`, --`local`
:   Place all WWW work files in the directory `./www`. This directory
    is not removed when `translate` exits.

-`m`, --`message|msg`
:   Input `file` arguments must be specified and the standard input is
    ignored. Each `file` is in
    [`gencat`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1)
    message format, and the file structure is preserved
    after translation. Only messages added since the last translation
    are translated; previous translations are preserved. All messages
    must be encoded with `\$quote "`.

-`n`, --`show`
:   Show the underlying the translation commands but do not execute. The
    temporary work directory is still created if it doesn't
    already exist.

-`o`, --`omit`=`pattern`
:   Omit translation methods matching the shell `pattern`.

-`u`, --`url`=`url`
:   `url` is the `URL` for the directory containing the `translate/`
    `dialect``/``chunk``.html` files to be translated.

-`v`, --`verbose`
:   List each file name on the standard output as it is translated.

# FILES

`lib/translate/DIALECTS`
:   Default dialects file on `\$PATH`. Each line contains a dialect
    `filter`, `name` and `method`.

`lib/translate/``filter`
:   Translation filter for the `filter` dialect.

# SEE ALSO

[`msgcvt`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/msgcvt.html)(1),
[`lynx`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/lynx.html)(1)

# IMPLEMENTATION

`version`
:   translate (AT&T Labs Research) 2001-01-31

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030252/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 2000-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030252/http://www.eclipse.org/org/documents/epl-v10.html)


