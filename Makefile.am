# set up non-recursive autotools

AM_CFLAGS = -g -Wall -fPIC
bin_PROGRAMS = pi
pi_SOURCES = src/pi.c

# build-aux

dist_doc_DATA = README.md
EXTRA_DIST = autogen.sh testsuite.at $(srcdir)/package.m4 $(TESTSUITE) atlocal.in

# set up test suite
#
TESTSUITE = $(srcdir)/testsuite

check-local: atconfig atlocal $(TESTSUITE)
	$(SHELL) ’$(TESTSUITE)’ $(TESTSUITEFLAGS)
	
installcheck-local: atconfig atlocal $(TESTSUITE)
	$(SHELL) ’$(TESTSUITE)’ AUTOTEST_PATH=’$(bindir)’ \
	$(TESTSUITEFLAGS)

clean-local:
	test ! -f ’$(TESTSUITE)’ || \
	$(SHELL) ’$(TESTSUITE)’ --clean

AUTOM4TE = $(SHELL) $(srcdir)/build-aux/missing --run autom4te
AUTOTEST = $(AUTOM4TE) --language=autotest
$(TESTSUITE): $(srcdir)/testsuite.at $(srcdir)/package.m4
	$(AUTOTEST) -I ’$(srcdir)’ -o $@.tmp $@.at
	mv $@.tmp $@
