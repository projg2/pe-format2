bin_PROGRAMS = pe-exec
sbin_SCRIPTS = pe-format2-conf.sh
noinst_SCRIPTS = pe-format.init
noinst_DATA = pe-format.conf

DISTCLEANFILES = $(noinst_SCRIPTS) $(noinst_DATA) $(sbin_SCRIPTS)
EXTRA_DIST = pe-format2-conf.sh.in pe-format.init.in pe-format.conf.in

pkgstatedir = $(localstatedir)/lib
pkgstatefile = $(pkgstatedir)/pe-format2

pe_exec_SOURCES = pe-exec.c pe-recog.c pe-recog.h pe-config.c pe-config.h cil-coff.h
pe_exec_CPPFLAGS = -DSTATEFILE=\"$(pkgstatefile)\"

$(sbin_SCRIPTS) $(noinst_SCRIPTS) $(noinst_DATA): config.status
	rm -f $@ $@.tmp
	$(SED) \
		-e "s|@sysconfdir[@]|$(sysconfdir)|" \
		-e "s|@sbindir[@]|$(sbindir)|" \
		-e "s|@pkgstatefile[@]|$(pkgstatefile)|" \
		${srcdir}/$@.in > $@.tmp
	chmod a-w $@.tmp
	mv $@.tmp $@
