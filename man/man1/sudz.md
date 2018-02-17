---
# vim: nu et tw=130 ts=8 sts=4 sw=4 ff=unix fo-=l fo+=tcroq2 fdm=marker fmr=@{,@} spell spelllang=en_gb
revision            : none yet
title               :
author              :
language            : en
lang                : en_UK
---

    NAME
      sudz - 3x3 sudoku minlex solution grid compressor

    SYNOPSIS
      sudz [ options ] [ file ... ]

    DESCRIPTION
      sudz is a 3x3 sudoku minlex solution grid compressor. If no file operands
      are specified, or if a file is -, then the standard input is read.

    OPTIONS
      -aN  List grids with >= N automorphisms.
      -fF  Format output according to F (default '%03b %3a %g') for each grid.
           printf(3) style width and fill apply. The formats are:
            %a  The number of automorphisms in the range 1..648 inclusive.
            %b  The band index in the range 1..416 inclusive.
            %g  The grid in 81 char row order form.
            %i  The grid index in the range 1..5472730538 inclusive.
            %w  The number of grids in the current window.
      -i   List the window information using the default format '%10i %03b %6w %g'.
           Grid information is for the first grid in the window.
      -oF  Write output to the file F instead of the standard output.
      -u   Uncompress the input to the standard output. This is the default.
      -w   Compress the input to the output. The input must be lines containing
           the space separated fields: band index, number of automorphisms, and
           the 81 char row order minlex-solution-grid. The input must be sorted
           by the minlex-solution-grid field in ascending order (or the compression
           rate will deteriorate).

    DETAILS
      A minlex solution grid (a.k.a. row order minlex canonical solution grid)
      is a solution grid with values, rows and columns permuted to yield the
      smallest lexicographic row order value. Grids are organized by the top band
      (top 3 rows). There are 416 essentially different minlex bands and 5472730538
      essentially different grids. A byproduct of minlex ordering is that earlier
      bands tend to account for more grids than later bands. For example, band 001
      contains 1007170 grids, band 006 (the largest) contains 96229042 grids, and
      bands 395,397,398,400,402,403,404,406,408,409,410,412,413,414,415 contain no
      grids.

      The compression format stores the number of grids and initial band index for
      each window. Each grid has the band index (if different from the previous
      grid), the number of automorphisms (if > 1), the number of cells that differ
      from the previous grid, and the list of differing cell values encoded using a
      basic singles constraint solver. The data is compressed using a combination
      of Burrows-Wheeler, move-to-front, run-length, and huffman encoding.

    PERFORMANCE
      The entire catalog of 5472730538 essentially different grids, in minlex
      order, compresses to 5.34GiB, or 8.38 bits/grid. Uncompress rate is
      ~100K grids/sec/Ghz, or ~5 hours minimum to stream through the entire
      catalog on a 2.8Ghz processor.

    SEE ALSO
      sudoku(1), bzlib(3)

    CONTRIBUTORS
      Subgrid (multiple solution) row order minlex canonicalizer by Michael Deverin.

    IMPLEMENTATION
      version     sudz (AT&T; Research) 2007-02-14
      author      Glenn Fowler <glenn.s.fowler@gmail.com>
      copyright   Copyright (c) 2007-2009 AT&T; Knowledge Ventures
      license     http://www.opensource.org/licenses/cpl1.0.txt
