AC_PREREQ([2.60])
AC_INIT([pe-format], [2.1.2])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([build-aux])
AM_INIT_AUTOMAKE([1.6 foreign dist-bzip2 subdir-objects])

AC_PROG_CC
AC_PROG_SED
AC_TYPE_UINT8_T
AC_TYPE_UINT16_T
AC_TYPE_UINT32_T

AC_ARG_ENABLE([debug],
	AS_HELP_STRING([--enable-debug], [Enable stderr debug]))

AS_IF([test "x$enable_debug" = "xyes"], [
	AC_DEFINE([ENABLE_DEBUG], [1], [Enable debugging code])
])

AC_ARG_WITH([systemdsystemunitdir],
	AS_HELP_STRING([--with-systemdsystemunitdir=DIR],
		[Directory for systemd system unit files (default: queried via pkg-config)]))

case "x$with_systemdsystemunitdir" in
	xyes|x)
		PKG_CHECK_VAR([DEFAULT_SYSTEMDSYSTEMUNITDIR], [systemd], [systemdsystemunitdir],
		[
			with_systemdsystemunitdir=$DEFAULT_SYSTEMDSYSTEMUNITDIR
		], [
			AS_IF([test "x$with_systemdsystemunitdir" = "xyes"], [
				AC_MSG_ERROR([systemd support requested but pkg-config unable to find systemd, consider passing specific directory via --with-systemdsystemunitdir])
			], [
				with_systemdsystemunitdir=no
			])
		])
		;;
esac
AC_SUBST([systemdsystemunitdir], [$with_systemdsystemunitdir])
AM_CONDITIONAL([WITH_SYSTEMD_SYSTEM_UNITS], [test "x$with_systemdsystemunitdir" != "xno"])

AC_ARG_WITH([binfmtdir],
	AS_HELP_STRING([--with-binfmtdir=DIR],
		[Directory for binfmt.d files (default: queried via pkg-config or PREFIX/binfmt.d)]))

case "x$with_binfmtdir" in
	xyes|x)
		PKG_CHECK_VAR([DEFAULT_BINFMTDIR], [systemd], [binfmtdir],
		[
			with_binfmtdir=$DEFAULT_BINFMTDIR
		], [
			with_binfmtdir=$prefix/binfmt.d
		])
		;;
esac
AC_SUBST([binfmtdir], [$with_binfmtdir])
AM_CONDITIONAL([WITH_BINFMT_D], [test "x$with_binfmtdir" != "xno"])

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES([Makefile])
AC_OUTPUT
