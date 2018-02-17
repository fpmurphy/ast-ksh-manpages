# NAME

ciadef - display attributes of selected C entities in the CIA program
database

# SYNOPSIS

`ciadef` \[ `-f` database \] \[ `-u` \] kind name
\[attr&lt;op&gt;value\]

# DESCRIPTION

`ciadef` displays attributes of C entities matching the given kind,
name, and the optional selection clauses. Each declaration instance of a
matched C entity is listed on a separate line. For descriptions on
argument conventions and selection clauses, refer to
[`ciaql`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/ciaql.html)(1).
`Options`

`-f`
: Use the specified
    [`cql`](/web/20141128030240/http://www2.research.att.com/~astopen/man/man1/cql.html)(1)
    virtual database instead of the standard ones (`symbol.db` and
    `reference.db`). The virtual database can also be set by exporting
    the environment variable `CIADBFILE`.

`-u`

: Output the information in unformatted form in the following order
    with the separation character "`;`" (the second line shows the
    field numbers for easy reference):

        id;name;kind;lev;file;dtype;sclass;bline;hline;eline;def;chksum;reserved
        1 ;2   ;3   ;4  ;5   ;6    ;7     ;8    ;9    ;10   ;11 ;12    ;13

    Note that the formatted output shows only a subset (the popular
    ones) of attributes, while the unformatted one shows all
    the attributes.

# EXAMPLES

List all the types and their attributes.

    $ ciadef type -
    file                                         type sclass  bline eline
    =========================== ===================== ======= ===== =====
    liblist/list.h                        struct list none    22    25
    /usr/include/stdio.h                struct _iobuf none    6     13
    liblist/list.h                   struct list_item none    17    20
    liblist/list.h                               LIST typedef 22    25
    viewline.h                       struct line_pair none    1     4
    liblist/list.h                               ITEM typedef 17    20
    viewline.h                                   PAIR typedef 1     4

List attributes of the type 'struct \_iobuf'

    $ ciadef type 'struct _iobuf'
    file                                         type sclass  bline eline
    =========================== ===================== ======= ===== =====
    /usr/include/stdio.h                struct _iobuf none    6     13

Where is FILE defined and what is it ?

    $ ciadef - FILE
    file                                  kind                           name
    ===================================== ===== =============================
    /usr/include/stdio.h                  macro                          FILE

What are the variables defined in file "viewline.c"?

    $ ciadef var - file=viewline.c
    file                           name sclass dtype          def     bline eline
    ====================== ============ ====== ============== ======= ===== =====
    viewline.c                   LINEON extern int            dec     17    17
    viewline.c                   FILEON extern int            dec     16    16
    viewline.c                       fp static struct _iobuf  def     13    13
    viewline.c                  srcfile static char `         def     14    14

List all static functions definitions.

    $ ciadef func - sclass=static def=def
    file                           name sclass dtype          def     bline eline
    ====================== ============ ====== ============== ======= ===== =====
    viewline.c                 viewline static void           def     28    45
    xmalloc.c                  mt_stamp static void           def     66    72

List all macros that start with "L\_" followed by lower case letters.

    $ ciadef macro 'L_[a-z]`'
    file                                                macro def     bline eline
    =========================== ============================= ======= ===== =====
    /usr/include/stdio.h                             L_tmpnam def     70    70
    /usr/include/stdio.h                            L_ctermid def     67    67
    /usr/include/stdio.h                            L_cuserid def     68    68

List attributes of the function viewpairs in unformatted from

    $ ciadef -u p viewpairs
    60;viewpairs;function;0;peekf.c;void;global;128;132;141;def;f3880ddd;

Count the number of static functions.

    $ ciadef -u func - sclass=static | wc -l
                3

List all header files using the single-file virtual database peek.db
(created with `cia -o peek`).

    $ cia -o peek peekf.A viewline.A xmalloc.A
    $ ciadef -f peek.db file '`.h'
    filename                                        length cpplen
    =============================================== ====== ======
    /usr/include/stdio.h                            71     71
    liblist/list.h                                  32     32
    viewfile.h                                      17     97
    viewline.h                                      8      8
    xmalloc.h                                       18     18
    common.h                                        22     40

Display all function definitions not defined in peekf.c; again, use the
virtual database by setting the environment variable CIADBFILE.

    $ export CIADBFILE=peek.db
    $ ciadef p - file!=peekf.c def=def
    file                           name sclass dtype          def     bline eline
    ====================== ============ ====== ============== ======= ===== =====
    viewline.c                 viewline static void           def     28    45
    viewline.c                viewlines global int            def     54    78
    xmalloc.c                  xrealloc global char `         def     46    64
    xmalloc.c                  mt_stamp static void           def     66    72
    xmalloc.c                   xmalloc global char `         def     27    44

# SEE ALSO

cia(1), ciaql(1), ciavdef(1)

------------------------------------------------------------------------

  ------------------- ------------ -------------------
  CIA User's Manual   March 1993   February 16, 2009
  ------------------- ------------ -------------------


