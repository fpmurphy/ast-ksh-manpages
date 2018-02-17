# NAME

hurl - copy http url data

# SYNOPSIS

`hurl` \[ `options` \] url

# DESCRIPTION

`hurl` copies the data for the `http` `url` operand to the standard
output. The `url` must be of the form `\[http://\]`
`host`\[`:``port`\]`/``path`. The default `port` is `80`.
`hurl` is a shell script that attempts to access the `url` by these
methods:

[`/dev/tcp/``host``/80`]()
\
Supported by
[`ksh`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
and recent
[`bash`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/bash.html)(1).
[`wget -nv -O -` `url`]()
[`lynx -source` `url`]()
[`curl -s -L -o -` `url`]()

# OPTIONS

-`a`, --`authorize`=`user:password`
:   The url authorization user name and password, separated by `:`
    (one colon character.)

-`s`, --`size`=`bytes`
:   Terminate the data transmission after `bytes` have been transferred.

-`v`, --`verbose`
:   Verbose trace.

# SEE ALSO

[`curl`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/curl.html)(1),
[`lynx`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/lynx.html)(1),
[`wget`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/wget.html)(1)

# IMPLEMENTATION

`version`
:   hurl (AT&T Research) 2009-01-20

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030244/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 2003-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030244/http://www.eclipse.org/org/documents/epl-v10.html)


