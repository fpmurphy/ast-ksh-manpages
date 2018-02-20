# NAME

locale - get locale-specific information

# SYNOPSIS

`locale` \[ `options` \] \[ name | name=value ... \]

# DESCRIPTION

`locale` writes information about the current locale to the standard
output. If no options or operands are specified then the environment for
each locale category is summarized. If operands are spcified then
information is written about each operand: a locale category name
operand (categories) selects all keywords in that category; other
operands name keywords within a category. Keyword names are unique
across all categories, so there is no ambiguity. `category=value`
operands set the corresponding locale `category` to `value` by a call to
[`setlocale`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man3/setlocale.html)(3).
A `value` of `-` is interpreted as `NULL`, allowing `category` to be
queried. The `TEST` category converts the `value` locale name to a
canonical form and lists the converted name on the standard output.
If the `--all` or `--undefined` options are specified and no
operands are specified then the names of all defined locales are listed
on the standard output. A `defined` locale name should work as an
argument to
[`setlocale`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man3/setlocale.html)(3).
An `undefined` name is valid but not supported on the local system.
Locale names have the general form
`language`\_`territory`.`charset`@`attribute`\[,`attribute`\]\` At least
one of `language` or `territory` is always specified, the other parts
are optional. The `--abbreviated`, `--qualified` , `--verbose` and
`--local` options determine the locale name listing style. The default
is `--abbreviated`. If multiple styles are specified then the names
are listed in columns in this order: `abbreviated`, `qualified`,
`verbose` and `local`.

# OPTIONS

-`a`, --`all`
:   List all defined locale names on the standard output.

-`b`, --`abbreviated`
:   List abbreviated locale names: `language` and `territory` as the two
    character ISO codes; non-default `charset` and `attributes`. This is
    the default.

-`c`, --`category`
:   List the category names for each operand on the standard output.

-`e`, --`element`
:   The operands are interpreted as collation elements. Each element
    name is listed on the standard output followed by a `tab`
    character and the space separated list of
    [`strxfrm`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man3/strxfrm.html)(3)
    collation weights.

-`i`, --`indent`
:   Indent keyword output lines for readability.

-`k`, --`keyword`
:   List the keyword name for each operand on the standard output.

-`l`, --`local`
:   List the locale names returned by the local system
    [`setlocale`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man3/setlocale.html)(3).
    NOTE: these names may contain embedded space.

-`m`, --`charmaps`
:   List the names of available charmaps.

-`q`, --`qualified`
:   List qualified locale names: `language` and `territory` as the two
    character ISO codes; default and non-default `charset` and
    `attributes`.

-`t`, --`composite`
:   List the composite value of LC\_ALL on the standard output.

-`u`, --`undefined`
:   List all undefined locale names on the standard output.

-`v`, --`verbose`
:   List verbose locale names: `language` and `territory` as the long
    English strings; non-default `charset` and `attributes`.

-`x`, --`transform`
:   The operands are interpreted as strings. Each string is listed on
    the standard output followed by a `tab` character and the space
    separated list of
    [`strxfrm`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man3/strxfrm.html)(3)
    collation weights.

# SEE ALSO

[`localeconv`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man3/localeconv.html)(3),
[`nl\_langinfo`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man3/nl_langinfo.html)(3),
[`setlocale`](/web/20141128030245/http://www2.research.att.com/~astopen/man/man3/setlocale.html)(3)

# IMPLEMENTATION

`version`
:   locale (AT&T Research) 2009-10-21

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1989-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030245/http://www.eclipse.org/org/documents/epl-v10.html)


