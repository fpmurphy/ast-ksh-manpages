# NAME

uniq - Report or filter out repeated lines in a file

# SYNOPSIS

`uniq` \[ `options` \] \[infile \[outfile\]\]

# DESCRIPTION

`uniq` reads the input, compares adjacent lines, and writes one copy
of each input line on the output. The second and succeeding copies of
the repeated adjacent lines are not written.
If the output file, `outfile`, is not specified, `uniq` writes to
standard output. If no `infile` is given, or if the `infile` is `-`,
`uniq` reads from standard input with the start of the file defined as
the current offset.

# OPTIONS

-`c`, --`count`
:   Output the number of times each line occurred along with the line.

-`d`, --`repeated|duplicates`
:   Output the first of each duplicate line.

-`D`, --`all-repeated`\[=`delimit`\]
:   Output all duplicate lines as a group with an empty line delimiter
    specified by `delimit`:

    [`none`]()
    : Do not delimit duplicate groups.

    [`prepend`]()
    : \
        Prepend an empty line before each group.

    [`separate`]()
    : \
        Separate each group with an empty line.

The option value may be omitted. The default value is `none`.\
-`f`, --`skip-fields`=`fields`
:   `fields` is the number of fields to skip over before checking
    for uniqueness. A field is the minimal string matching the BRE
    `\[\[:blank:\]\]\`\[\^\[:blank:\]\]\``. -`number` is equivalent to
    `--skip-fields` =`number`.

-`i`, --`ignore-case`
:   Ignore case in comparisons.

-`s`, --`skip-chars`=`chars`
:   `chars` is the number of characters to skip over before checking
    for uniqueness. If specified along with `-f`, the first `chars`
    after the first `fields` are ignored. If the `chars` specifies more
    characters than are on the line, an empty string will be used
    for comparison. +`number` is equivalent to `--skip-chars`
    =`number`.

-`u`, --`unique`
:   Output unique lines.

-`w`, --`check-chars`=`chars`
:   `chars` is the number of characters to compare after skipping any
    specified fields and characters.

# EXIT STATUS

`0`
: The input file was successfully processed.

`&gt;0`
:   An error occurred.

# SEE ALSO

[`sort`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/sort.html)(1),
[`grep`](/web/20141128030252/http://www2.research.att.com/~astopen/man/man1/grep.html)(1)

# IMPLEMENTATION

`version`
:   uniq (AT&T Research) 2009-11-28

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20141128030252/mailto:glenn.s.fowler@gmail.com)&gt;

`author`
:   David Korn
    &lt;[dgkorn@gmail.com](https://web.archive.org/web/20141128030252/mailto:dgkorn@gmail.com)&gt;

`copyright`
:   Copyright © 1992-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030252/http://www.eclipse.org/org/documents/epl-v10.html)


