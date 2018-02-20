# NAME

msgget - get a message from a message catalog

# SYNOPSIS

`msgget` \[ `options` \] locale \[command:\]catalog \[set.\]number \[ text \]

# DESCRIPTION

`msgget` gets the message corresponding to the parameters. If `locale`
is `-` then the current locale is used. `command` may be specified for
command specific messages. `catalog` specifies the message catalog name.
\[`set`.\]`number` identifies the message by message `number` and an
optional message `set`; if specified as `-` then the message set and
number are determined by looking up `text` in the corresponding `C`
locale message catalog.

# SEE ALSO

[`iconv`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/iconv.html)(1),
[`msgcc`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/msgcc.html)(1),
[`msggen`](/web/20141128030247/http://www2.research.att.com/~astopen/man/man1/msggen.html)(1)

# IMPLEMENTATION

`version`
:   msgget (AT&T Research) 2001-04-21

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 2000-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030247/http://www.eclipse.org/org/documents/epl-v10.html)


