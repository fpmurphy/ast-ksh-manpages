# NAME

ciavdef - display the source text of selected C entities in the CIA
program database

# SYNOPSIS

`ciavdef` \[ `-f` database \] \[ `-g` \] \[ `-n` \] kind name
\[attr&lt;op&gt;value\]

# DESCRIPTION

`ciavdef` displays source text of C entity declarations matching the
given kind, name, and the optional selection clauses. For descriptions
on argument conventions and selection clauses, refer to
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
    each entity.

`-n`

: Output the source line number with a separation character "`;`"
    before each source line.

# EXAMPLES

Show the values of all macros that start with MAX and defined in
viewfile.h:

    $ ciavdef macro 'MAX`' file=viewfile.h
    #define MAXLINENO 100000
    #define MAXNUMLEN 8
    #define MAXPAIRS 8                /` realloc when necessary `/

Show all static variable declarations in viewline.c with line numbers:

    $ ciavdef -n v - file=viewline.c sclass=static
    000013;static FILE `fp;
    000014;static char `srcfile;

Show the definition of the type 'struct list' with file name and line
numbers:

    $ ciavdef -g -n type 'struct list'
    <file: liblist/list.h>
    000022;typedef struct list {
    000023; struct list_item `head;
    000024; struct list_item `current;
    000025;} LIST;

Show the source file viewline.h:

    $ ciavdef file viewline.h
    typedef struct line_pair {
           int bline;
           int eline;

} PAIR;
extern int viewlines(/\` char \`file, LIST \`line\_pairs \`/);

\#define CIASRCDIR "CIASRCDIR"

# SEE ALSO

cia(1), ciaql(1), ciadef(1)

------------------------------------------------------------------------

  ------------------- ------------ -------------------
  CIA User's Manual   March 1993   February 16, 2009
  ------------------- ------------ -------------------


