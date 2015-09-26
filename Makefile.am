bin_PROGRAMS = pe-exec
sbin_SCRIPTS = pe-format2-setup
sysconf_DATA = pe-format2.conf
application_DATA = pe-exec.desktop

applicationdir = $(datarootdir)/applications

#if WITH_BINFMT_D
binfmt_DATA = binfmt.d/pe-format2.conf
#endif

if WITH_SYSTEMD_SYSTEM_UNITS
systemdsystemunit_DATA = systemd/pe-format2.service systemd/pe-format2.path
endif

DISTCLEANFILES = $(sbin_SCRIPTS) $(binfmt_DATA) $(sysconf_DATA) \
	$(systemdsystemunit_DATA) $(application_DATA)
EXTRA_DIST = pe-format2-setup.in \
	pe-format2.conf.in \
	binfmt.d/pe-format2.conf.in \
	systemd/pe-format2.service.in \
	systemd/pe-format2.path.in \
	pe-exec.desktop.in
DISTCHECK_CONFIGURE_FLAGS = \
	--with-systemdsystemunitdir=\$${libdir}/systemd/system

pkgstatefile = $(localstatedir)/pe-format2

pe_exec_SOURCES = \
	src/pe-exec.c src/cil-coff.h \
	src/pe-recog.c src/pe-recog.h \
	src/pe-config.c src/pe-config.h
pe_exec_CPPFLAGS = -DSTATEFILE=\"$(pkgstatefile)\"

$(sbin_SCRIPTS) $(binfmt_DATA) $(sysconf_DATA) $(systemdsystemunit_DATA) $(application_DATA): config.status
	$(MKDIR_P) binfmt.d systemd
	rm -f $@ $@.tmp
	$(SED) \
		-e "s|@sysconfdir[@]|$(sysconfdir)|" \
		-e "s|@bindir[@]|$(bindir)|" \
		-e "s|@sbindir[@]|$(sbindir)|" \
		-e "s|@pkgstatefile[@]|$(pkgstatefile)|" \
		${srcdir}/$@.in > $@.tmp
	chmod a-w $@.tmp
	mv $@.tmp $@

pe-format2-setup: pe-format2-setup.in
binfmt.d/pe-format2.conf: binfmt.d/pe-format2.conf.in
pe-format2.conf: pe-format2.conf.in
pe-exec.desktop: pe-exec.desktop.in
systemd/pe-format2.service: systemd/pe-format2.service.in
systemd/pe-format2.path: systemd/pe-format2.path.in

install-exec-local:
	test -z "$(localstatedir)" || $(MKDIR_P) "$(DESTDIR)$(localstatedir)"

EXTRA_DIST += NEWS
NEWS: configure.ac Makefile.am
	git for-each-ref refs/tags --sort '-*committerdate' \
		--format '# %(tag) (%(*committerdate:short))%0a%(contents:body)' \
		> NEWS
