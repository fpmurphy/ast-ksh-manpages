# NAME

package - source and binary package control

# SYNOPSIS

`package` \[ `options` \] \[ qualifier ... \] \[ action \] \[ arg ... \] \[ n=v ... \]

# DESCRIPTION

The `package` command controls source and binary packages. It is a
[`sh`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
script coded for maximal portability. All package files are in the
`\$PACKAGEROOT` directory tree. `\$PACKAGEROOT` must at minumum
contain a `bin/package` command or a `lib/package` directory. Binary
package files are in the `\$INSTALLROOT`
(`\$PACKAGEROOT/arch/``hosttype`) tree, where
`hosttpe`=\``package`\`. All `actions` but `host` and `use`
require the current directory to be under `\$PACKAGEROOT`. See
`DETAILS` for more information.
Note that no environment variables need be set by the user; `package`
determines the environment based on the current working directory. The
`use` action starts a
[`sh`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
with the environment initialized. `CC`, `CCFLAGS`, `HOSTTYPE` and
`SHELL` may be set by explicit command argument assignments to
override the defaults.

Packages are composed of components. Each component is built and
installed by an `ast`
[`nmake`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
makefile. Each package is also described by an `nmake` makefile that
lists its components and provides a content description. The package
makefile and component makefiles provide all the information required to
read, write, build and install packages.

Package recipients only need
[`sh`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
and
[`cc`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/cc.html)(1)
to build and install source packages, and `sh` to install binary
packages. `nmake` and `ksh93` are required to write new packages. An
`\$INSTALLROOT/bin/cc` script may be supplied for some architectures.
This script supplies a reasonable set of default options for compilers
that accept multiple dialects or generate multiple object/executable
formats.

The command arguments are composed of a sequence of words: zero or more
`qualifiers`, one `action`, and zero or more action-specific
`arguments`, and zero or more `name=value` definitions. `package` names
a particular package. The naming scheme is a `-` separated hierarchy;
the leftmost parts describe ownership, e.g., `gnu-fileutils`,
`ast-base`. If no packages are specified then all packages are
operated on.
[`optget`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man3/optget.html)(3)
documentation options are also supported. The default with no arguments
is `host type`.

The qualifiers are:

`authorize` `name`
:   Remote authorization user name or license acceptance phrase.

`debug|environment`
:   Show environment and actions but do not execute.

`flat`
: Collapse `\$INSTALLROOT` { bin fun include lib } onto
    `\$PACKAGEROOT`.

`force`
:   Force the action to override saved state.

`never`
:   Run make -N and show other actions.

`only`
: Only operate on the specified packages.

`password` `password`
:   Remote authorization or license acceptance password.

`quiet`
:   Do not list captured action output.

`show`
: Run make -n and show other actions.

`verbose`
:   Provide detailed action output.

`DEBUG`
:   Trace the package script actions in detail.

The actions are:
[`admin` \[`all`\] \[`db` `file`\] \[`on` `pattern`\]\[ `action` ...\]]()
\
Apply `action` ... to the hosts listed in `file`. If `file` is omitted
then `admin.db` is assumed. The caller must have
[`rcp`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/rcp.html)(1)
and
[`rsh`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/rsh.html)(1)
or
[`scp`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/scp.html)(1)
and
[`ssh`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/ssh.html)(1)
access to the hosts. Output for `action` is saved per-host in the file
`action``.log/``host`. Logs can be viewed by `package admin`
\[`on` `host`\] `results` \[`action` \]. By default only local
PACKAGEROOT hosts are selected from `file`; `all` selects all hosts.
`on` `pattern` selects only hosts matching the `|` separated
`pattern`. `file` contains four types of lines. Blank lines and lines
beginning with `\#` are ignored. Lines starting with `id`=`value` are
variable assignments. Set admin\_ping to local conventions if "ping -c 1
-w 5" fails. If a package list is not specified on the command line the
`action` applies to all packages; a variable assigment
`package`="`list`" applies `action` to the packages in `list` for
subsequent hosts in `file`. The remaining line type is a host
description consisting of 6 tab separated fields. The first 3 are
mandatory; the remaining 3 are updated by the `admin` action. `file`
is saved in `file``.old` before update. The fields are:

`hosttype`
:   The host type as reported by "`package`".

`\[user@\]host`
:   The host name and optionally user name for
    [`rcp`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/rcp.html)(1)
    and
    [`rsh`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/rsh.html)(1) access.

`\[remote:\[\[master\]:\]\]PACKAGEROOT`
:   The absolute remote package root directory and optionally the remote
    protocol (rsh or ssh) if the directory is on a different server than
    the master package root directory. If
    `lib/package/admin/admin.env` exists under this directory then it
    is sourced by
    [`sh`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/sh.html)(1)
    before `action` is done. If this field begins with `-` then the
    host is ignored. If this field contains `:` then
    [`ditto`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/ditto.html)(1)
    is used to sync the remote `src` directory hierarchy to the
    local one. If \[`master`\]: is specified then the sync is deferred
    to the `master` host. If `master` is omitted (two :) then the sync
    is disabled. These directories must exist on the remote side:
    `lib/package` , `src/cmd`, `src/lib`.

`date`
: `YYMMDD` of the last action.

`time`
: Elapsed wall time for the last action.

`M T W`
:   The `admin` action `make`, `test` and `write` action
    error counts. A non-numeric value in any of these fields disables
    the corresponding action.

`owner`
:   The owner contact information.

`attributes`
:   `name=value` attributes. Should at least contain
    `cc`=`compiler-version` .

[`clean | clobber`]()
\
Delete the `arch/``HOSTTYPE` hierarchy; this deletes all generated
files and directories for `HOSTTYPE`. The heirarchy can be rebuilt by
`package make`.
[`contents` \[ `package` ... \]]()
\
List description and components for `package` on the standard output.
[`copyright` \[ `package` ... \]]()
\
List the general copyright notice(s) for `package` on the standard
output. Note that individual components in `package` may contain
additional or replacement notices.
[`export` \[ `variable` ...\]]()
\
List `name`=`value` for `variable`, one per line. If the `only`
attribute is specified then only the variable values are listed. If no
variables are specified then `HOSTTYPE NPROC PACKAGEROOT INSTALLROOT
PATH` are assumed.
[`help` \[ `action` \]]()
\
Display help text on the standard error (standard output for `action` ).
[`host` \[ `attribute` ... \]]()
\
List architecture/implementation dependent host information on the
standard output. `type` is listed if no attributes are specified.
Information is listed on a single line in `attribute` order. The
attributes are:

`canon` `name`
:   An external host type name to be converted to `package` syntax.

`cpu`
: The number of cpus; 1 if the host is not a multiprocessor.

`name`
: The host name.

`rating`
:   The cpu rating in pseudo mips; the value is useful useful only in
    comparisons with rating values of other hosts. Other than a vax
    rating (mercifully) fixed at 1, ratings can vary wildly but
    consistently from vendor mips ratings.
    [`cc`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/cc.html)(1)
    may be required to determine the rating.

`type`
: The host type, usually in the form `vendor`.`architecture`, with an
    optional trailing -`version`. The main theme is that type names
    within a family of architectures are named in a similar,
    predictable style. OS point release information is avoided as much
    as possible, but vendor resistance to release incompatibilities has
    for the most part been futile.

[`html` \[ `action` \]]()
\
Display html help text on the standard error (standard output for
`action`).
[`install` \[ `architecture` ... \] `directory` \[ `package` ... \]]()
\
Copy the package binary hierarchy to `directory`. If `architecture` is
omitted then all architectures are installed. If `flat` is specified
then exactly one `architecture` must be specified; this architecture
will be installed in `directory` without the `arch/``HOSTTYPE`
directory prefixes. Otherwise each architecture will be installed in a
separate `arch/``HOSTTYPE` subdirectory of `directory`. The
`architecture` `-` names the current architecture. `directory` must be
an existing directory. If `package` is omitted then all binary packages
are installed. This action requires `nmake`.
[`license` \[ `package` ... \]]()
\
List the source license(s) for `package` on the standard output. Note
that individual components in `package` may contain additional or
replacement licenses.
[`list` \[ `package` ... \]]()
\
List the name, version and prerequisites for `package` on the standard
output.
[`make` \[ `package` \] \[ `option` ... \] \[ `target` ... \]]()
\
Build and install. The default `target` is `install`, which makes and
installs `package`. If the standard output is a terminal then the output
is also captured in `\$INSTALLROOT/lib/package/gen/make.out`. The
build is done in the `\$INSTALLROOT` directory tree viewpathed on top
of the `\$PACKAGEROOT` directory tree. If `flat` is specified then
the `\$INSTALLROOT` { bin fun include lib } directories are linked to
the same directories in the package root. Only one architecture may be
`flat`. Leaf directory names matching the `|`-separated shell
pattern `\$MAKESKIP` are ignored. The `view` action is done before
making. `option` operands are passed to the underlying make command.
[`read` \[ `package` ... | `archive` ... \]]()
\
Read the named package or archive(s). Must be run from the package root
directory. Archives are searched for in `.` and `lib/package/tgz`.
Each package archive is read only once. The file
`lib/package/tgz/``package`\[.`type`\]`.tim` tracks the read time.
See the `write` action for archive naming conventions. Text file
archive member are assumed to be ASCII or UTF-8 encoded.
[`regress`]()
\
[`diff`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/diff.html)(1)
the current and previous `package test` results.
[`release` \[ \[`CC`\]`YY-MM-DD` \[ \[`cc`\]`yy-mm-dd` \]\] \[ `package` \]]()
\
Display recent changes for the date range \[`CC`\]`YY-MM-DD` (up to
\[`cc`\]`yy-mm-dd` .), where `-` means lowest (or highest.) If no
dates are specified then changes for the last 4 months are listed.
`package` may be a package or component name.
[`remove` \[ `package` \]]()
\
Remove files installed for `package`.
[`results` \[ `failed` \] \[ `path` \] \[ `old` \] \[`make` | `test` | `write` \]]()
\
List results and interesting messages captured by the most recent
`make` (default), `test` or `write` action. `old` specifies the
previous results, if any (current and previous results are retained.)
`\$HOME/.pkgresults`, if it exists, must contain an
[`egrep`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/egrep.html)(1)
expression of result lines to be ignored. `failed` lists failures only
and `path` lists the results file path name only.
[`setup` \[ beta \] \[ binary \] \[ source \] \[ `architecture` ... \]
\[ `url` \] \[ `package` ... \]]()
\
This action initializes the current directory as a package root, runs
the `update` action to download new or out of date packages, and runs
the `read` action on those packages. If `flat` is specified then the
`\$INSTALLROOT` { bin fun include lib } directories are linked to the
same directories in the package root. Only one architecture may be
`flat`. See the `update` and `read` action descriptions for
argument details.
[`test` \[ `package` \]]()
\
Run the regression tests for `package`. If the standard output is a
terminal then the output is also captured in
`\$INSTALLROOT/lib/package/gen/test.out`. In general a package must be
made before it can be tested. Components tested with the
[`regress`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/regress.html)(1)
command require `ksh93`. If `only` is also specified then only the
listed package components are tested, otherwise the closure of the
components is tested.
[`update` \[ beta \] \[ binary \] \[ source \] \[`architecture` ... \]
\[ `url` \] \[ `package` ... \]]()
\
Download the latest release of the selected and required packages from
`url` (e.g., `http://www.research.att.com/sw/download`) into the
directory `\$PACKAGEROOT/lib/package/tgz` . `beta` acesses beta
packages; download these at your own risk. If `architecture` is omitted
then only architectures already present in the `tgz` directory will be
downloaded. If `architecture` is `-` then all posted architectures
will be downloaded. If `url` matches `\`.url` then it is interpreted
as a file containing shell variable assignments for `url`,
`authorize` and `password`. If `url` is omitted then the definitions
for `url`, `authorize` and `password` in
`\$PACKAGEROOT/lib/package/tgz/default.url`, if it exists, are used.
If `\$PACKAGEROOT/lib/package/tgz/default.url` does not exist then it
is initialized with the current `url`, `authorize` and `password`
values and read permission for the current user only. If `package` is
omitted then only packages already present in the tgz directory will be
downloaded. If `package` is `-` then all posted packages will be
downloaded. If `source` and `binary` are omitted then both source
and binary packages will be downloaded. If `only` is specified then
only the named packages are updated; otherwise the closure of required
packages is updated. This action requires
[`wget`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/wget.html)(1),
[`lynx`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/lynx.html)(1),
[`curl`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/curl.html)(1)
or a shell that supports io to `/dev/tcp/``host`/`port`.
[`use` \[ `uid` | `package` | . \[ 32 | 64 \] | 32 | 64 | - \] \[ command ...\]]()
\
Run `command`, or an interactive shell if `command` is omitted, with the
environment initialized for using the package (can you say `shared`
`library` or `dll` without cussing?) If `uid` or `package` or `.` is
specified then it is used to determine a `\$PACKAGEROOT`, possibly
different from the current directory. For example, to try out bozo\`s
package: `package use bozo`. The `use` action may be run from any
directory. If the file `\$INSTALLROOT/lib/package/profile` is readable
then it is sourced to initialize the environment. 32 or 64 implies
`\$PACKAGEROOT` of . and specifies the target architecture word size
(which may be silently ignored.)
[`verify` \[ `package` \]]()
\
Verify installed binary files against the checksum files in
`\$INSTALLROOT/lib/``package``/gen/\`.sum`. The checksum files
contain mode, user and group information. If the checksum matches for a
given file then the mode, user and group are changed as necessary to
match the checksum entry. A warning is printed on the standard error for
each mismatch. Requires the `ast` package
[`cksum`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/cksum.html)(1)
command.
[`view`]()
Initialize the architecture specific viewpath hierarchy. If `flat` is
specified then the `\$INSTALLROOT` { bin fun include lib } directories
are linked to the same directories in the package root. Only one
architecture may be `flat` . The `make` action implicitly calls this
action.
[`write` \[`format`\] `type` ... \[ `package` ...\]]()
\
Write a package archive for `package`. All work is done in the
`\$PACKAGEROOT/lib/package` directory. `format`-specific files are
placed in the `format` subdirectory. A `package`\[.`type`\]`.tim` file
in this directory tracks the write time and prevents a package from
being read in the same root it was written. If more than one file is
generated for a particular `format` then those files are placed in the
`format`/`package` subdirectory. File names in the `format` subdirectory
will contain the package name, a `yyyy-mm-dd` date, and for binary
packages, `HOSTTYPE`. If `package` is omitted then an ordered list of
previously written packages is generated. If `only` is specified then
only the named packages will be written; otherwise prerequisite packages
are written first. Package components must be listed in
`package``.pkg` . `format` may be one of:

`cyg`
: Generate a `cygwin` package.

`exp`
: Generate an `exptools` maintainer source archive and `NPD` file,
    suitable for
    [`expmake`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/expmake.html)(1)

`lcl`
: Generate a package archive suitable for restoration into the local
    source tree (i.e., the source is not annotated for licencing.)

`pkg`
: Generate a
    [`pkgmk`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/pkgmk.html)(1)
    package suitable for
    [`pkgadd`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/pkgadd.html)(1).

`rpm`
: Generate an
    [`rpm`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/rpm.html)(1) package.

`tgz`
: Generate a
    [`gzip`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1)
    [`tar`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/tar.html)(1)
    package archive. This is the default.

`tst`
: Generate a `tgz` format package archive in the
    `tst` subdirectory. Version state files are not updated.

`type` specifies the package type which must be one of `source`,
`binary` or `runtime`. A source package contains the source needed
to build the corresponding binary package. A binary package includes the
libraries and headers needed for compiling and linking against the
public interfaces. A runtime package contains the commands and required
dynamic libraries. A package may be either a `base` or `delta`. A
base package contains a complete copy of all components. A delta package
contains only changes from a previous base package. Delta recipients
must have the `ast`
[`pax`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/pax.html)(1)
command (in the `ast-base` package.) If neither `base` nor `delta`
is specified, then the current base is overwritten if there are no
deltas referring to the current base. Only the `tgz` and `lcl`
formats support `delta`. If `base` is specified then a new base and
two delta archives are generated: one delta to generate the new base
from the old, and one delta to generate the old base from the new; the
old base is then removed. If `delta` is specified then a new delta
referring to the current base is written. `package``.pkg` may
reference other packages. By default a pointer to those packages is
written. The recipient `package read` will then check that all
required packages have been downloaded. If `closure` is specified then
the components for all package references are included in the generated
package. This may be useful for `lcl` and versioning. All formats but
`lcl` annotate each `source` file (not already annotated) with a
license comment as it is written to the package archive using
[`proto`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/proto.html)(1).

# DETAILS

The package directory hierarchy is rooted at `\$PACKAGEROOT`. All
source and binaries reside under this tree. A two level viewpath is used
to separate source and binaries. The top view is architecture specific,
the bottom view is shared source. All building is done in the
architecture specific view; no source view files are intentionally
changed. This means that many different binary architectures can be made
from a single copy of the source.
Independent `\$PACKAGEROOT` hierarchies can be combined by appending
`\$INSTALLROOT:\$PACKAGEROOT` pairs to `VPATH`. The `VPATH`
viewing order is from left to right. Each `\$PACKAGEROOT` must have a
`\$PACKAGEROOT/lib/package` directory.

Each package contains one or more components. Component source for the
`foo` command is in `\$PACKAGEROOT/src/cmd/``foo` , and source for the
`bar` library is in `\$PACKAGEROOT/src/lib/lib``bar`. This naming is
for convenience only; the underlying makefiles handle inter-component
build order. The `INIT` component, which contains generic package
support files, is always made first, then the components named
`INIT`\`, then the component order determined by the closure of
component makefile dependencies.

`\$PACKAGEROOT/lib/package` contains package specific files. The
package naming convention is `group`\[-`part`\]; e.g., `ast-base`,
`gnu-fileutils`. The \``.pkg` files are ast
[`nmake`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
makefiles that contain the package name, package components, references
to other packages, and a short package description. \``.pkg` files are
used by `package write` to generate new source and binary packages.

`\$PACKAGEROOT/lib/package/``group``.lic` files contain license
information that is used by the `ast`
[`proto`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/proto.html)(1)
and
[`nmake`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
commands to generate source and binary license strings. `group` is
determined by the first `:PACKAGE:` operator name listed in the
component `nmake` makefile. `group``.lic` files are part of the
licensing documentation. Each component may have its own `LICENSE`
file that overrides the `group``.lic` file. The full text of the
licenses are in the `\$PACKAGEROOT/lib/package/LICENSES` and
`\$INSTALLROOT/lib/package/LICENSES` directories.

A few files are generated in `\$PACKAGEROOT/lib/package/gen` and
`\$INSTALLROOT/lib/package/gen`. `package``.ver` contains one line
consisting of `package version release` `1` for the most recent
instance of `package` read into `\$PACKAGEROOT` , where `package` is
the package name, `version` is the `YYYY-MM-DD` base version, and
`release` is `version` for the base release or `YYYY-MM-DD` for delta
releases. `package``.req` contains \``.ver` entries for the packages
required by `package`, except that the fourth field is `0` instead of
`1`. All packages except `INIT` require the `INIT` package. A
simple sort of `package``.pkg` and \``.ver` determines if the
required package have been read in. Finally, `package``.README` and
`package.html` `contain the README text for` `package` and all its
components. Included are all changes added to the component `RELEASE`,
`CHANGES` or `ChangeLog` files dated since the two most recent base
releases. Component `RELEASE` files contain tag lines of the form
\[`YY`\]`YY-MM-DD` \[ `text` \] (or
[`date`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/date.html)(1)
format dates) followed by README text, in reverse chronological order
(newer entries at the top of the file.) `package release` lists this
information, and `package contents ...` lists the descriptions and
components.

`\$HOSTYPE` names the current binary architecture and is determined by
the output of `package` (no arguments.) The `\$HOSTTYPE` naming
scheme is used to separate incompatible executable and object formats.
All architecture specific binaries are placed under `\$INSTALLROOT`
(`\$PACKAGEROOT/arch/\$HOSTTYPE`.) There are a few places that match
against `\$HOSTTYPE` when making binaries; these are limited to
makefile compiler workarounds, e.g., if `\$HOSTTYPE` matches `hp.\``
then turn off the optimizer for these objects. All other architecture
dependent logic is handled either by the `ast`
[`iffe`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/iffe.html)(1)
command or by component specific configure scripts. Explicit
`\$HOSTYPE` values matching \`,\`cc\`\[,-\`,...\] optionally set the
default `CC` and `CCFLAGS`. This is handy for build farms that
support different compilers on the same architecture.

Each component contains an `ast`
[`nmake`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1)
makefile (either `Nmakefile` or `Makefile`) and a `MAM` (make
abstract machine) file (`Mamfile`.) A Mamfile contains a portable
makefile description that is used by
[`mamake`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/mamake.html)(1)
to simulate `nmake`. Currently there is no support for
old-make/gnu-make makefiles; if the binaries are just being built then
`mamake` will suffice; if source or makefile modifications are
anticipated then `nmake` (in the `ast-base` package) should be used.
Mamfiles are automatically generated by `package write`.

Most component C source is prototyped. If `\$CC` (default value
`cc`) is not a prototyping C compiler then `package make` runs
[`proto`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/proto.html)(1)
on portions of the `\$PACKAGEROOT/src` tree and places the converted
output files in the `\$PACKAGEROOT/proto/src` tree. Converted files
are then viewpathed over the original source.
[`proto`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/proto.html)(1)
converts an ANSI C subset to code that is compatible with K&R, ANSI, and
C++ dialects.

All scripts and commands under `\$PACKAGEROOT` use `\$PATH` relative
pathnames (via the `ast`
[`pathpath`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man3/pathpath.html)(3)
function); there are no imbedded absolute pathnames. This means that
binaries generated under `\$PACKAGEROOT` may be copied to a different
root; users need only change their `\$PATH` variable to reference the
new installation root `bin` directory. `package install` installs
binary packages in a new `\$INSTALLROOT` .

# SEE ALSO

[`autoconfig`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/autoconfig.html)(1),
[`cksum`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/cksum.html)(1),
[`execrate`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/execrate.html)(1),
[`expmake`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/expmake.html)(1),
[`gzip`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/gzip.html)(1),
[`make`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/make.html)(1),
[`mamake`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/mamake.html)(1),
[`nmake`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/nmake.html)(1),
[`pax`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/pax.html)(1),
[`pkgadd`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/pkgadd.html)(1),
[`pkgmk`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/pkgmk.html)(1),
[`proto`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/proto.html)(1),
[`ratz`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/ratz.html)(1),
[`rpm`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/rpm.html)(1),
[`sh`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/sh.html)(1),
[`tar`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man1/tar.html)(1),
[`optget`](/web/20150527152311/http://www2.research.att.com/~astopen/man/man3/optget.html)(3)

# IMPLEMENTATION

`version`
:   package (AT&T Research) 2012-06-20

`author`
:   Glenn Fowler
    &lt;[glenn.s.fowler@gmail.com](https://web.archive.org/web/20150527152311/mailto:glenn.s.fowler@gmail.com)&gt;

`copyright`
:   Copyright © 1994-2012 AT&T Intellectual Property

`license`
:   [http://www.eclipse.org/org/documents/epl-v10.html](https://web.archive.org/web/20150527152311/http://www.eclipse.org/org/documents/epl-v10.html)


