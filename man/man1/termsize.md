# NAME

termsize - determine terminal (window) size

# SYNOPSIS

`termsize` \[ format ... \]

# DESCRIPTION

`termsize` determines the current terminal (window) size and prints the
terminal type and the number of lines and columns on the standard
output. `format` specifies the output format in
[`printf`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man3/printf.html)(3)
style. `%c` outputs the number of lines, `%l` outputs the number of
columns, `%t` outputs the terminal name and any other character is
output as is. The default format is `"TERM=%t LINES=%l COLUMNS=%c"`.
The terminal (window) size is determined as follows. If the environment
variable `TERM` has the form `TERM=``s` `LINES=``l`
`COLUMNS=``c` then `s` is the terminal type, `l` is the number of
lines and `c` is the number of columns, otherwise the lines and columns
are determined by
[`winsize`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man3/winsize.html)(3).
The default values are taken from
[`termcap`](/web/20141128030251/http://www2.research.att.com/~astopen/man/man5/termcap.html)(5)
if the `TERM` environment variable is defined and are otherwise
`LINES=24` and `COLUMNS=80`.

# SEE ALSO

winsize(3), termcap(5)

------------------------------------------------------------------------

  -- -- -------------------
        November 07, 2006
  -- -- -------------------


