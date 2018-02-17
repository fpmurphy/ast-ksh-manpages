# NAME

tr - translate, squeeze, and/or delete characters

# SYNOPSIS

`tr` \[ `options` \] \[ set1 \[ set2 \] \]

# DESCRIPTION

`tr` copies the standard input to the standard output with
substitution or deletion of selected characters. Input characters in
`set1` are mapped to corresponding characters in `set2`.

# OPTIONS

-`c`, --`complement`
\
Complement `set1`.
-`d`, --`delete`
\
Delete characters in `set1` but do not translate.
-`s`, --`squeeze-repeats`
\
Replace sequences of the same character with one.
-`t`, --`truncate-set1`
\
Truncate `set1` to the length of `set2`.
`sets` are specified as strings of characters. Most represent
themselves. Interpreted sequences are:

`\\nnn`
: character with octal value `nnn`

`\\xnn`
: character with hexadecimal value `nn`

`\\\\`
: backslash

`\\a`
: alert

`\\b`
: backpace

`\\f`
: form feed

`\\r`
: return

`\\t`
: horizontal tab

`\\v`
: vertical tab

`\\E`
: escape

`c1-c2`
:   all characters from `c1` to `c2` in ascending order

`\[c1-c2\]`
:   same as `c1-c2` if both `sets` use this form

`\[\[c\`\]\]`
:   in `set2`, copies of \\ac\\a until length of `set1`

`\[\[c\`n\]\]`
:   \\an\\a copies of \\ac\\a

`\[\[:alnum:\]\]`
:   all letters and digits

`\[\[:alpha:\]\]`
:   all letters

`\[\[:blank:\]\]`
:   all horizontal whitespace

`\[\[:cntrl:\]\]`
:   all control characters

`\[\[:digit:\]\]`
:   all digits

`\[\[:graph:\]\]`
:   all printable characters, not including space

`\[\[:lower:\]\]`
:   all lower case letters

`\[\[:print:\]\]`
:   all printable characters, including space

`\[\[:punct:\]\]`
:   all punctuation characters

`\[\[:space:\]\]`
:   all horizontal or vertical whitespace

`\[\[:upper:\]\]`
:   all upper case letters

`\[\[:xdigit:\]\]`
:   all hexadecimal digits

`\[\[=c=\]\]`
:   all characters which are equivalent to \\ac\\a

Translation occurs if `-d` is not given and both `set1` and `set2`
appear. `-t` may be used only when translating. `set2` is extended to
the length of `set1` by repeating its last character as necessary.
Excess characters in `set2` are ignored. Only \[:lower:\] and
\[:upper:\] are guaranteed to expand in ascending order. They may only
be used in pairs to specify case conversion. `-s` uses `set1` if
neither translating nor deleting, otherwise squeeze uses `set2` and
occurs after translation or deletion.

# SEE ALSO

[`sed`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man1/sed.html)(1),
[`ascii`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man5/ascii.html)(5)

# IMPLEMENTATION

`version`
:   tr (AT&T Research) 2012-05-31

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030251/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030251/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030251/http://www.eclipse.org/org/documents/epl-v10.html)


