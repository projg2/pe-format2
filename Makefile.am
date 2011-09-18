bin_PROGRAMS = pe-exec
sbin_SCRIPTS = pe-format2-conf.sh
binfmt_DATA = binfmt.d/pe-format2.conf

DISTCLEANFILES = $(noinst_SCRIPTS) $(noinst_DATA) $(sbin_SCRIPTS) $(binfmt_DATA)
EXTRA_DIST = pe-format2-conf.sh.in \
	binfmt.d/pe-format2.conf.in

pkgstatefile = $(localstatedir)/pe-format2

pe_exec_SOURCES = \
	src/pe-exec.c src/cil-coff.h \
	src/pe-recog.c src/pe-recog.h \
	src/pe-config.c src/pe-config.h
pe_exec_CPPFLAGS = -DSTATEFILE=\"$(pkgstatefile)\"

$(sbin_SCRIPTS) $(binfmt_DATA): config.status
	rm -f $@ $@.tmp
	$(SED) \
		-e "s|@sysconfdir[@]|$(sysconfdir)|" \
		-e "s|@bindir[@]|$(bindir)|" \
		-e "s|@sbindir[@]|$(sbindir)|" \
		-e "s|@pkgstatefile[@]|$(pkgstatefile)|" \
		${srcdir}/$@.in > $@.tmp
	chmod a-w $@.tmp
	mv $@.tmp $@

pe-format2-conf.sh: pe-format2-conf.sh.in
binfmt.d/pe-format2.conf: binfmt.d/pe-format2.conf.in

install-exec-local:
	test -z "$(localstatedir)" || $(MKDIR_P) "$(DESTDIR)$(localstatedir)"
