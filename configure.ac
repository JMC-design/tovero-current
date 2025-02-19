dnl -*- Autoconf -*-

dnl configure.ac

dnl Copyright 2018 Kavalogic, Inc.
dnl
dnl This file is part of Tovero.
dnl
dnl Tovero is free software; you can redistribute it and/or modify it
dnl under the terms of the GNU General Public License as published by
dnl the Free Software Foundation; either version 2 of the License, or
dnl (at your option) any later version.
dnl
dnl Tovero is distributed in the hope that it will be useful, but
dnl WITHOUT ANY WARRANTY; without even the implied warranty of
dnl MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
dnl General Public License for more details.  You should have received a
dnl copy of the GNU General Public License along with Tovero. If not,
dnl see <http://www.gnu.org/licenses/>.

dnl *** Process this file with autoconf to produce a configure script. ***

dnl Variables output with AC_SUBST are prefixed by CFG_ to signify
dnl that they are determined by configure.

dnl Save *FLAGS first, so they don't get changed by macros.
EXTERN_CFLAGS="$CFLAGS"
EXTERN_CPPFLAGS="$CPPFLAGS"
EXTERN_CXXFLAGS="$CXXFLAGS"
EXTERN_LDFLAGS="$LDFLAGS"

AC_INIT([Tovero], [0.0.0],, [Tovero], [http://www.kavalogic.com/tovero])

dnl Generate config.h, containing HAVE_ defines
AC_CONFIG_HEADERS([config.h])

AC_COPYRIGHT([Copyright 2018 Kavalogic, Inc.  See the file COPYING for licensing and distribution terms.])
AH_TOP([/* Copyright 2018 Kavalogic, Inc.  See the file COPYING for licensing and distribution terms. */])

AM_INIT_AUTOMAKE([-Wall -Werror])
m4_ifdef([AM_PROG_AR], [AM_PROG_AR])
m4_ifdef([AM_PROG_RANLIB], [AM_PROG_RANLIB])

dnl AC_CONFIG_SRCDIR is a file found in the source tree as a check
AC_CONFIG_SRCDIR([src/tovero/library/tovero.h])

dnl Get host type
AC_CANONICAL_HOST

dnl Set up default compiler flags
CPPFLAGS="${CPPFLAGS:=}"
CXXFLAGS="${CXXFLAGS:=}"
LDFLAGS="${LDFLAGS:=}"

dnl Setup Makefile conditionals from configure options
dnl   debug
AC_ARG_ENABLE(debug, AC_HELP_STRING([--enable-debug], [enable debugging [default=no]]))
AM_CONDITIONAL([CFG_COND_DEBUG], [test "x$enable_debug" = xyes])
dnl   parallel installation
AC_ARG_ENABLE([parallel-install],
              AC_HELP_STRING([--enable-parallel-install],
                             [allow parallel library versions to coexist at the same installation prefix] [default=no]]))
AM_CONDITIONAL([CFG_COND_PARALLEL_INSTALL], [test "x$enable_parallel_install" = xyes])
AS_IF([test "x$enable_parallel_install" = xyes],
      [CFG_TOVERO_LIBRARY_PARALLEL="/Tovero-0"],
      [CFG_TOVERO_LIBRARY_PARALLEL=""])

dnl Setup for libraries
AC_PROG_LIBTOOL
AC_CONFIG_MACRO_DIR([m4])

dnl Checks for programs.
AC_PROG_CXX
AC_PROG_INSTALL

dnl Library checks
dnl (N/A)

dnl Package checks
PKG_PROG_PKG_CONFIG
dnl   libfive
PKG_CHECK_MODULES([CFG_LIBFIVE], [libfive >= 0.0.0])
dnl Installation directory for Common Lisp files
AC_ARG_WITH([lisp-install-dir],
  [AS_HELP_STRING([--with-lisp-install-dir],
    [installation directory for Common Lisp files, defaults to ${HOME}/common-lisp])],
  [CFG_LISP_INSTALL_DIR="$withval"],
  [CFG_LISP_INSTALL_DIR="${HOME}/common-lisp"])

dnl Output variables
dnl   Parallel Installation
AC_SUBST(CFG_TOVERO_LIBRARY_PARALLEL)
dnl   Common Lisp installation directory
AC_SUBST(CFG_LISP_INSTALL_DIR)

dnl Create makefiles and other files generated by the configure script (".in")
AC_CONFIG_FILES([                                   \
                  scripts/tovero                    \
                  scripts/Makefile                  \
                  src/tovero/Makefile               \
                  src/tovero/library/Makefile       \
                  src/tovero/library/libTovero-0.pc \
                  src/tovero-viewer/Makefile        \
                ])
AC_OUTPUT(Makefile)
