# NAME

ciaref - display selected C relationships in the CIA program database

# SYNOPSIS

`ciaref` \[ `-f` database \] \[ `-u` \] kind1 name1 kind2 name2
\[attr1&lt;op&gt;value\] ... \[attr2&lt;op&gt;value\] ...

# DESCRIPTION

`ciaref` displays relationships between C entities matching the given
two pairs of kinds and names and the optional selection clauses. Each
instance of a matched C relationship is listed on a separate line. For
descriptions on argument conventions and selection clauses, refer to
[`ciaql`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/ciaql.html)(1).
`Options`

`-f`
: Use the specified
    [`cql`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/cql.html)(1)
    virtual database instead of the standard ones (`symbol.db` and
    `reference.db`). The virtual database can also be set by exporting
    the environment variable `CIADBFILE`.

`-u`

: Output the information in unformatted form in the following order on
    a single line with the separation character "`;`" (the additional
    lines show the field numbers for easy reference):

        id1;name1;kind1;lev1;file1;dtype1;sclass1;bline1;hline1;eline1;def1;chksum1;
        1  ;2    ;3    ;4   ;5    ;6     ;7      ;8     ;9     ;10    ;11  ;12     ;
        id2;name2;kind2;lev2;file2;dtype2;sclass2;bline2;hline2;eline2;def2;chksum2;
        13 ;14   ;15   ;16  ;17   ;18    ;19     ;20    ;21    ;22    ;23  ;24     ;
        usage;
        25   ;

    Note that the formatted output shows only a subset (the popular
    ones) of attributes, while the unformatted one shows all
    the attributes.

# EXAMPLES

Find all functions that refer to the variable srcfile:

    $ ciaref func - var srcfile
    k1 file1             name1              k2 file2             name2
    == ================= ================== == ================= =================
    p  viewline.c        viewlines          v  viewline.c        srcfile
    p  viewline.c        viewline           v  viewline.c        srcfile

Find all entities in \`/stdio.h that the function main refers to:

    $ ciaref fu main - - file2='`/stdio.h'
    k1 file1             name1              k2 file2             name2
    == ================= ================== == ================= =================
    p  peekf.c           main               m  /usr/include/stdi EOF
    p  peekf.c           main               m  /usr/include/stdi stdin
    p  peekf.c           main               m  /usr/include/stdi stderr
    p  peekf.c           main               v  /usr/include/stdi _iob
    p  peekf.c           main               p  /usr/include/stdi fgets

Find all functions in viewline.c that refer to variables defined in
other files:

    $ ciaref fu - v - file1=viewline.c file2!=viewline.c
    k1 file1             name1              k2 file2             name2
    == ================= ================== == ================= =================
    p  viewline.c        viewline           v  peekf.c           FILEON
    p  viewline.c        viewline           v  peekf.c           LINEON

Find all type to type references:

    $ ciaref t - t -
    k1 file1             name1              k2 file2             name2
    == ================= ================== == ================= =================
    t  viewline.h        PAIR               t  viewline.h        struct line_pair
    t  liblist/list.h    ITEM               t  liblist/list.h    struct list_item
    t  liblist/list.h    LIST               t  liblist/list.h    struct list
    t  liblist/list.h    struct list        t  liblist/list.h    struct list_item
    t  liblist/list.h    struct list_item   t  liblist/list.h    struct list_item

Find all references to static objects in viewline.c:

    $ ciaref - - - - file2=viewline.c sclass2=static
    k1 file1             name1              k2 file2             name2
    == ================= ================== == ================= =================
    p  viewline.c        viewlines          v  viewline.c        fp
    p  viewline.c        viewlines          p  viewline.c        viewline
    p  viewline.c        viewline           v  viewline.c        fp
    p  viewline.c        viewlines          v  viewline.c        srcfile
    p  viewline.c        viewline           v  viewline.c        srcfile

# SEE ALSO

cia(1), ciaql(1), ciavref(1)

------------------------------------------------------------------------

  ------------------- ------------ -------------------
  CIA User's Manual   March 1993   February 16, 2009
  ------------------- ------------ -------------------


