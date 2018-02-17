# NAME

expr - evaluate arguments as an expression

# SYNOPSIS

`expr` \[ `options` \] operand ...

# DESCRIPTION

`expr` evaluates an expression given as arguments and writes the
result to standard output. The character `0` will be written to
indicate a zero value and nothing will be written to indicate an empty
string.
Most of the functionality of `expr` is provided in a more natural way
by the shell,
[`sh`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/sh.html)(1),
and `expr` is provided primarily for backward compatibility.

Terms of the expression must be separate arguments. A string argument is
one that can not be identified as an integer. Integer-valued arguments
may be preceded by a unary plus or minus sign. Because many of the
operators use characters that have special meaning to the shell, they
must be quoted when entered from the shell.

Expressions are formed from the operators listed below in order of
increasing precedence within groups. All of the operators are left
associative. The symbols `expr1` and `expr2` represent expressions
formed from strings and integers and the following operators:

`expr1` `|` `expr2`
:   Returns the evaluation of `expr1` if it is neither null nor 0,
    otherwise returns the evaluation of expr2.

`expr1` `&` `expr2`
:   Returns the evaluation of `expr1` if neither expression evaluates to
    null or 0, otherwise returns 0.

`expr1` `op` `expr2`
:   Returns the result of a decimal integer comparison if both arguments
    are integers; otherwise, returns the result of a string comparison
    using the locale-specific collation sequence. The result of each
    comparison will be 1 if the specified relationship is true, or 0 if
    the relationship is false. `op` can be one of the following:

    [`=`]()
    : Equal.

    [`==`]()
    : Equal.

    [`&gt;`]()
    : Greater than.

    [`&gt;=`]()
    : \
        Greater than or equal to.

    [`&lt;`]()
    : Less than.

    [`&lt;=`]()
    : \
        Less than or equal to.

    [`!=`]()
    : Not equal to.

`expr1` `op` `expr2`
:   Where `op` is `+` or `-`; addition or subtraction of decimal
    integer-valued arguments.

`expr1` `op` `expr2`
:   Where `op` is `\``, `/` or `%`; multiplication, division, or
    remainder of the decimal integer-valued arguments.

`expr1` `:` `expr2`
:   The matching operator : compares `expr1` with `expr2` , which must
    be a BRE. Normally, the matching operator returns the number of
    bytes matched and 0 on failure. However, if the pattern contains at
    least one sub-expression \[\\( . . .\\)\], the string corresponding
    to \\1 will be returned.

``( `expr1` )
:   Grouping symbols. An expression can be placed within parenthesis to
    change precedence.

`match` `string` `expr`
:   Equivalent to `string` `:` `expr`.

`substr` `string` `pos` `length`
:   `length` character substring of `string` starting at `pos` (counting
    from 1).

`index` `string` `chars`
:   The position in `string` (counting from 1) of the leftmost
    occurrence of any character in `chars`.

`length` `string`
:   The number of characters in `string`.

`quote` `token`
:   Treat `token` as a string operand.

For backwards compatibility, unrecognized options beginning with a `-`
will be treated as operands. Portable applications should use `--` to
indicate end of options.

# EXIT STATUS

`0`
: The expression is neither null nor 0.

`1`
: The expression is null or 0.

`2`
: Invalid expressions.

`&gt;2`
:   An error occurred.

# SEE ALSO

[`regcomp`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man5/regcomp.html)(5),
[`grep`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/grep.html)(1),
[`sh`](/web/20141128030243/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)

# IMPLEMENTATION

`version`
:   expr (AT&T Research) 2010-08-11

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030243/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030243/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030243/http://www.eclipse.org/org/documents/epl-v10.html)


