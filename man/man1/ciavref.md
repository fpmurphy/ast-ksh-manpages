# NAME

ciavref - display the source text of selected C relationships in the CIA
program database

# SYNOPSIS

`ciavref` \[ `-f` database \] \[ `-g` \] \[ `-n` \] kind1 name1
kind2 name2 \[attr1&lt;op&gt;value\] ... \[attr2&lt;op&gt;value\] ...

# DESCRIPTION

`ciavref` displays the source text of reference relationships between C
entities matching the given two pairs of kinds and names and the
optional selection clauses. For descriptions on argument conventions and
selection clauses, refer to
[`ciaql`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/ciaql.html)(1).
`Options`

`-f`
: Use the specified
    [`cql`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/cql.html)(1)
    virtual database instead of the standard ones (`symbol.db` and
    `reference.db`). The virtual database can also be set by exporting
    the environment variable `CIADBFILE`.

`-g`
: Output the source file name in angle brackets before the text of
    each relationship occurrence.

`-n`

: Output the source line number with a separation character "`;`"
    before each source line.

# EXAMPLES

Show all references from functions to the macro \_\_PROTO\_\_ with file
names and line numbers:

    $ ciavref -g -n fu - m __PROTO__
    <file: liblist/list.h>
    000029;extern void walk_list __PROTO__(( LIST `list, void (`proc)() ));
    <file: xmalloc.h>
    000007;extern char `xrealloc __PROTO__ (( char `, unsigned int ));
    <file: liblist/list.h>
    000030;extern void free_list __PROTO__(( LIST `list, void (`freel)() ));
    <file: liblist/list.h>
    000028;extern void insert_list __PROTO__(( LIST `list, VOID `data ));
    <file: xmalloc.h>
    000006;extern char `xmalloc __PROTO__ (( unsigned int ));
    <file: xmalloc.c>
    000022;void static mt_stamp __PROTO__ (( char `, int ));

Show all references (with line numbers) to the function xmalloc from C
entities in peekf.c; note that allocate is a macro defined as a call to
xmalloc:

    $ ciavdef macro allocate
    #define allocate(t) (t`)xmalloc(sizeof(t))
    $ ciavref -n - - fu xmalloc file1=peekf.c
    000160; line=(char `) xmalloc(MAXLINE);
    000096; p=allocate(PAIR);
    000104; p=allocate(PAIR);
    000112; p=allocate(PAIR);
    000048; argv=(char `) xmalloc ( sizeof(char `)
    000049; `argvlen);
    000050; argv[1]=xmalloc(MAXPATH);
    000062; p=argv[i]=xmalloc(MAXNUMLEN);

Create an alias "usage" and then show all references to the symbol FILE
using "usage EOF":

    $ alias usage='ciavref -g -n - - -'
    $ usage FILE
    <file: /usr/include/stdio.h>
    000056;extern FILE  `popen();
    <file: /usr/include/stdio.h>
    000054;extern FILE  `fdopen();
    <file: /usr/include/stdio.h>
    000055;extern FILE  `freopen();
    <file: /usr/include/stdio.h>
    000053;extern FILE  `fopen();
    <file: /usr/include/stdio.h>
    000003;# ifndef FILE
    <file: /usr/include/stdio.h>
    000057;extern FILE  `tmpfile();
    <file: viewline.c>
    000013;static FILE `fp;

# SEE ALSO

cia(1), ciaql(1), ciaref(1)

------------------------------------------------------------------------

  ------------------- ------------ -------------------
  CIA User's Manual   March 1993   February 16, 2009
  ------------------- ------------ -------------------


