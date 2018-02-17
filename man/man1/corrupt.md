# NAME

corrupt - corrupt file by modifying bytes in-place

# SYNOPSIS

`corrupt` \[ `options` \] file offset,length,character ...

# DESCRIPTION

`corrupt` modifies byte ranges of the named `file` operand in place
according to the 3-tuple operands `offset` ,`length`,`character`, where
`offset` is the file offset, `length` is the length in bytes of the
segment to corrupt, and `character` is the value of the newly corrupted
bytes. One or more 3-tuples may be specified. The calling process must
have read/write/seek access to `file`.

# IMPLEMENTATION

`version`
:   corrupt (AT&T Labs Research) 2003-09-30

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030241/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1986-2010 AT&T Intellectual Property

`license`
:   [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030241/http://www.opensource.org/licenses/cpl1.0.txt)


