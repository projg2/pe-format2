AC_INIT([pe-format], [2.0.3])
AM_INIT_AUTOMAKE([-Wall foreign dist-bzip2])

# Define only include macros we're going to use.
AC_DEFUN([AC_INCLUDES_DEFAULT], [
m4_ifval([$1], [$1
], [dnl
#ifdef HAVE_STDINT_H
#	include <stdint.h>
#endif
])])

AC_PROG_CC
AC_CHECK_HEADERS([stdint.h])
AC_TYPE_UINT8_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T

AC_CONFIG_FILES([Makefile])
AC_OUTPUT