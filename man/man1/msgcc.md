# NAME

msgcc - C language message catalog compiler

# SYNOPSIS

`msgcc` \[ `options` \] file ...

# DESCRIPTION

`msgcc` is a C language message catalog compiler. It accepts
[`cc`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/cc.html)(1)
style options and arguments. A
[`msgcpp`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/msgcpp.html)(1)
`.mso` file is generated for each input `.c` file. If the `-c`
option is not specified then a
[`gencat`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1)
format `.msg` file is generated from the input `.mso` and `.msg`
files. If `-c` is not specified then a `.msg` suffix is appended to
the `-o` `file` if it doesn't already have a suffix. The default
output is `a.out.msg` if `-c` and `-o` are not specified.
If `-M-new` is not specified then messages are merged with those in
the pre-existing `-o` file.

# OPTIONS

-`M` `-option`
:   Set a `msgcc` specific `option`. `option` may be:

    [`mkmsgs`]()
    : \
        The `-o` file is assumed to be in
        [`mkmsgs`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/mkmsgs.html)(1) format.

    [`new`]()
    : Create a new `-o` file.

    [`preserve`]()
    : \
        Messages in the `-o` file that are not in new `.msg` file
        arguments are preserved. The default is to either reuse the
        message numbers with new message text that is similar to the old
        or to delete the message text, leaving an unused message number.

    [`set=``number`]()
    : \
        Set the message set number to `number`. The default is `1` .

    [`similar=``number`]()
    : \
        The message text similarity measure threshold. The similarity
        measure between `old` and `new` message text is
        100\`(2\`gzip(`old`+`new`)/(gzip(`old`)+gzip( `new`))-1), where
        gzip(`x`) is the size of text `x` when compressed by
        [`gzip`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1).
        The default threshold is 30. A threshold of `0` turns off
        message replacement, but unused old messages are still deleted.
        Use `-M-preserve` to preserve all old messages.

    [`verbose`]()
    : \
        Trace similar message replacements on the standard error.

# SEE ALSO

[`cc`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/cc.html)(1),
[`cpp`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/cpp.html)(1),
[`gencat`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/gencat.html)(1),
[`msggen`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/msggen.html)(1),
[`msgcpp`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/msgcpp.html)(1),
[`msgcvt`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/msgcvt.html)(1)

# IMPLEMENTATION

`version`
:   msgcc (AT&T Labs Research) 2010-10-20

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 2000-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030247/http://www.eclipse.org/org/documents/epl-v10.html)


