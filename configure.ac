#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([performance], [0.1], [thomas_lynn.marcus@tu-dresden.de])
AC_CONFIG_SRCDIR([src])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_HEADERS([config.h])


# Checks for programs.
AC_PROG_CC
AC_LANG(C)
dnl AC_REQUIRE_CC

# Checks for libraries.

# Checks for header files.
AC_CHECK_HEADERS([inttypes.h], [], [
                  AC_MSG_ERROR([unable to find header inttypes.h])
                  ])
AC_CHECK_HEADERS([stdlib.h], [], [
                  AC_MSG_ERROR([unable to find header stdlib.h])
                  ])
AC_CHECK_HEADERS([string.h], [], [
                  AC_MSG_ERROR([unable to find header string.h])
                  ])
AC_CHECK_HEADERS([stdio.h], [], [
                  AC_MSG_ERROR([unable to find header stdio.h])
                  ])
AC_CHECK_HEADERS([time.h], [], [
                  AC_MSG_ERROR([unable to find header time.h])
                  ])

# Checks for typedefs, structures, and compiler characteristics.

# Check for OpenMP

AC_OPENMP

HAVE_OPENMP=no
if test -n "${OPENMP_CFLAGS}"; then
  AC_MSG_CHECKING([whether OpenMP will work in a package])
  AC_LANG_CONFTEST(
    [AC_LANG_PROGRAM([[#include "omp.h"]], [[ return omp_get_num_threads (); ]])]
                   )
  PKG_CFLAGS="${OPENMP_CFLAGS}" PKG_LIBS="${OPENMP_CFLAGS}" 
  HAVE_OPENMP=yes
  AC_MSG_RESULT([${HAVE_OPENMP}])
fi

if test "${ac_pkg_openmp}" = "no"; then
  OPENMP_CFLAGS=''
  AC_MSG_ERROR([OpenMP required but not found])
fi

AC_SUBST(OPENMP_CFLAGS)
AC_SUBST(HAVE_OPENMP)

# Checks for library functions.


# Use automake

AM_INIT_AUTOMAKE([-Wall -Werror foreign subdir-objects])


# set up test suite

AC_CONFIG_TESTDIR([.], [.:tests])
AC_CONFIG_FILES(atlocal)

AC_CONFIG_FILES([Makefile
                 ])
AC_OUTPUT
