# NAME

pr - print files

# SYNOPSIS

`pr` \[ `options` \] \[ file ... \]

# DESCRIPTION

`pr` formats and prints files to the standard output. If `file` is
`-` or if no files are specified then the standard input is read.

# OPTIONS

-`a`, --`across`
:   Print columns across rather than down; `-``columns` must be &gt;1.

-`c`, --`control`
:   Print control characters in hat (\^G) and octal form.

-`C`, --`columns|cols`=`columns`
:   Print `columns` columns of output. Can also be entered as
    -`columns` . May not be used with `-m`. The default value is
    `1`.

-`d`, --`double-space`
:   Double space the output.

-`e`, --`expand`\[=`char\[width\]`\]
:   Expand `char` to `width`. The option value may be omitted. The
    default value is `\\t8`.

-`f`, --`formfeed`
:   Use formfeeds instead of newlines to separate pages with a 3 line
    page header.

-`F`, --`bigformfeed`
:   Use formfeeds instead of newlines to separate pages with a 5 line
    page header and trailer.

-`h`, --`header`=`header`
:   Use `header` instead of the file name in header text.

-`i`, --`replace`\[=`char\[width\]`\]
:   Replace spaces with `char`s to tab `width`. The option value may
    be omitted. The default value is `\\t8`.

-`j`, --`join`
:   Merge full lines.

-`l`, --`lines`=`lines`
:   The page length in lines. 10 lines are reserved for the header
    and trailer. The default value is `66`.

-`m`, --`multiple`
:   Print the input files one per column, truncating lines to fit.

-`n`, --`number`\[=`sep\[digits\]`\]
:   Number lines with `digits` digits followed by `sep`. The option
    value may be omitted. The default value is `\\t5`.

-`o`, --`indent|margin|offset`=`indent`
:   Indent each line with `indent` spaces. The default value is `0` .

-`p`, --`pause`
:   Pause before printing each page if the output is to a terminal. `pr`
    prinst a BEL on the terminal and reads one line of input
    before continuing. (Not implemented.)

-`P`, --`page`=`page`
:   Start printing with page `page`. Can also be entered as +`page`. The
    default value is `1`.

-`r`, --`warn`
:   Warn about unreadable input files. On by default; -`r` means
    --`nowarn`.

-`s`, --`separate`\[=`string`\]
:   Separate columns with `string`. The option value may be omitted.

-`t|T`, --`headers`
:   Generate headers and trailers and pass form feeds in the input to
    the output. On by default; -`t` means --`noheaders`.

-`w`, --`width`=`width`
:   The page width in characters. The default value is `72`.

-`v`, --`literal`
:   Print control characters in C-style form.

-`X`, --`test`
:   Canonicalize output for testing.

# SEE ALSO

[`cat`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/cat.html)(1),
[`fold`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/fold.html)(1),
[`less`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/less.html)(1),
[`more`](/web/20141128030248/http://www2.research.att.com/~astopen/man/man1/more.html)(1)

# IMPLEMENTATION

`version`
:   pr (AT&T Research) 2004-07-01

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030248/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030248/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030248/http://www.eclipse.org/org/documents/epl-v10.html)


