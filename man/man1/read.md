# NAME

read - read a line from standard input

# SYNOPSIS

`read` \[ `options` \] \[var?prompt\] \[var ...\]

# DESCRIPTION

`read` reads a line from standard input and breaks it into fields
using the characters in value of the `IFS` variable as separators. The
escape character, `\\`, is used to remove any special meaning for the
next character and for line continuation unless the `-r` option is
specified.

If there are more variables than fields, the remaining variables are set
to empty strings. If there are fewer variables than fields, the leftover
fields and their intervening separators are assigned to the last
variable. If no `var` is specified then the variable `REPLY` is used.

When `var` has the binary attribute and `-n` or `-N` is specified,
the bytes that are read are stored directly into `var`.

If you specify `?``prompt` after the first `var`, then `read` will
display `prompt` on standard error when standard input is a terminal or
pipe.

# OPTIONS

-`A`
: Unset `var` and then create an indexed array containing each field
    in the line starting at index 0.

-`C`
: Unset `var` and read `var` as a compound variable.

-`d` `delim`
: Read until delimiter `delim` instead of to the end of line.

-`p`
: Read from the current co-process instead of standard input. An end
    of file causes `read` to disconnect the co-process so that another
    can be created.

-`r`
: Do not treat `\\` specially when processing the input line.

-`s`
: Save a copy of the input as an entry in the shell history file.

-`u` `fd`
: Read from file descriptor number `fd` instead of standard input. The
    default value is `0`.

-`t` `timeout`
: Specify a timeout `timeout` in seconds when reading from a terminal
    or pipe.

-`n` `nchar`
: Read at most `nchar` characters. For binary fields `size` will be
    in bytes.

-`N` `nchar`
: Read exactly `nchar` characters. For binary fields `size` will be
    in bytes.

-`v`
: When reading from a terminal the value of the first variable is
    displayed and used as a default value.

# EXIT STATUS

`0`
: Successful completion.

`&gt;0`
: End of file was detected or an error occurred.

# SEE ALSO

[`print`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/print.html)(1),
[`printf`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/printf.html)(1),
[`cat`](/web/20141128030249/http://www2.research.att.com/~astopen/man/man1/cat.html)(1)

# IMPLEMENTATION

`version`
: read (AT&T Research) 2006-12-19

`author`
: David Korn

`copyright`
: Copyright © 1982-2010 AT&T Intellectual Property

`license`
: [http://www.opensource.org/licenses/cpl1.0.txt](https://web.archive.org/web/20141128030249/http://www.opensource.org/licenses/cpl1.0.txt)


