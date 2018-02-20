# NAME

htmlrefs - list html url references

# SYNOPSIS

`htmlrefs` \[ `options` \] \[ file ... \]

# DESCRIPTION

`htmlrefs` lists url references from the local closure of the input
`html` `file`s. If `file` is not specified then the top level default
user file is read. The `html` parse is rudimentary; don't use
`htmlrefs` to detect valid `html` files.
The top level references are determined in this order (the `--index`,
`--root` and `--user` options influence the order):

[`\$HOME/index.html`]()
\
Pseudo index containing `&lt;LINK href=``dir` `rel=``type` `&gt;`
references to top level directories. `type` may be one of:

`document-root`
:   The document root directory containing URL target documents. Exactly
    one `document-root` must be specified.

`program-root`
:   The program root directory containing CGI support programs
    and scripts. This type is optional. If specified then the program
    root directory should contain a pseudo index for its references.

`data-root`
:   The data root directory containing CGI support data. This type
    is optional. If specified then the data root directory should
    contain a pseudo index for its references.

`dynamic`
:   All files under `dir` are considered referenced.

`host`
: Provides a default value for the `--hosts` option.

`ignore`
:   `dir` is a
    [`ksh`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    pattern of paths to ignore.

`internal`
:   If `--external` is on then `dir` is a
    [`ksh`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    pattern of internal paths.

`secure`
:   Files under this dir are accessed by `https:` only.

[`\$HOME/wwwfiles/index.html`]()
[`\$HOME/public\_html/index.html`]()

# OPTIONS

-`a`, --`all`
:   List all references whether they exist or not.

-`c`, --`copy`=`directory`
:   Copy the selected references to `directory` which must
    already exist. If `--external` is also specified then lines
    between `&lt;!--INTERNAL--&gt;` ... `&lt;!--/INTERNAL--&gt;`
    lines are not copied. If `--unreferenced` is also specified then
    files and directories in `directory` that have not been copied are
    removed. Target file modification times are set to match source
    times so that future copies can be avoided.

-`d`, --`dependents`
:   List each selected local file followed by `:` and a list of all
    local files referring to the file.

-`e`, --`external`
:   Do not list references inside `&lt;!--INTERNAL--&gt;` ...
    `&lt;!--/INTERNAL--&gt;` lines. See
    [`mm2html`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/mm2html.html)(1)
    for an html generator that inserts these lines.

-`F`, --`force`
:   By default files are not copied if the source and target size and
    modification times match. `--force` forces all files to be copied.

-`h`, --`hosts`=`pattern`
:   Check only references matching the
    [`ksh`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/ksh.html)(1)
    pattern `http://``pattern``/`.

-`i`, --`index`=`name`
:   `name` specifies the page named by directory references. The default
    value is `index.html` .

-`k`, --`keep`=`pattern`
:   `pattern` is used to match file base names that are always
    considered referenced. The default value is `.htaccess`.

-`l`, --`limit`=`pattern`
:   Limit `--copy` and `--remove` operations to path names matching
    `pattern` .

-`m`, --`missing`
:   List missing local file references.

-`n`, --`exec`
:   Enable file modification operations. `--noexec` lists the
    operations but does not do them. On by default; -`n` means
    --`noexec`.

-`p`, --`perlwarn`
:   Check HTML files for unintentional embedded
    [`perl`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/perl.html)(1)
    constructs: a left bracket followed by one of `-+!\$\`\#`.
    Manually translating left bracket to `&\#0091;` avoids unwanted
    `perl` interactions (why didn't they use tags like everyone else?)
    [`mm2html`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/mm2html.html)(1)
    and
    [`optget`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man3/optget.html)(3)
    do the translation by default. On by default; -`p` means
    --`noperlwarn` .

-`X`, --`remove`
:   Unreferenced files are removed when `--unreferenced` and
    `--nocopy` are specified.

-`r`, --`root`=`directory`
:   The local `directory` for `--user` references. The default value
    is `\~` `user``.`

-`K`, --`skip`=`pattern`
:   `pattern` is used to match file base names that are never
    considered referenced. The default value is `00-INDEX-00`.

-`s`, --`strict`
:   By default unreferenced `--index` files and the containing
    directory are considered referenced; `--strict` considers
    unreferenced `--index` files unreferenced.

-`S`, --`symlink`
:   Instruct `--copy` to
    [`symlink`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man2/symlink.html)(2)
    files that do not contain `&lt;!--INTERNAL--&gt;` ...
    `&lt;!--/INTERNAL--&gt;` or are not in `/cgi-bin/`.

-`u`, --`user`=`name`
:   `\~``name` translates to the `--root` directory. The default
    value is `caller-uid` .

-`v`, --`verbose`
:   List files as they are copied (see `--copy`.)

-`w`, --`warn`
:   Produce a warning diagnostic for missing files.

-`x`, --`unreferenced`
:   If `--copy` is also specified then remove files and directories in
    the `--copy` `directory` that have not been copied. Otherwise list
    unreferenced files in the `--root` directory. A directory that
    contains no referenced files but does contain an `--index` file is
    considered referenced (along with the `--index` file) unless
    `--strict` is enabled.

# EXAMPLES

`htmlrefs --hosts=www.research.att.com --missing`
:   List missing references to the local host `www.research.att.com`.

`htmlrefs -n -h www.research.att.com -c \~/external/wwwfiles -e -x`
:   Copy the local hierarchy to `\~/external/wwwfiles` for external
    release, and remove unreferenced files in the copy.

# SEE ALSO

[`html2rtf`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/html2rtf.html)(1),
[`mm2html`](/web/20141128030244/http://www2.research.att.com/~astopen/man/man1/mm2html.html)(1)

# IMPLEMENTATION

`version`
:   htmlrefs (AT&T Research) 2012-01-01

`author`
:   Glenn Fowler

`copyright`
:   Copyright © 1996-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20141128030244/http://www.eclipse.org/org/documents/epl-v10.html)


