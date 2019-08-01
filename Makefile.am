# set up non-recursive autotools

AM_CFLAGS = -g -Wall -fPIC
bin_PROGRAMS = pi ## correct
pi_SOURCES = src/pi.c ## correct

# build-aux

dist_doc_DATA = README.md ## unsure
EXTRA_DIST = autogen.sh testsuite.at $(srcdir)/package.m4 $(TESTSUITE) atlocal.in ## unsure

# set up test suite
#
TESTSUITE = $(srcdir)/tests

check: atconfig atlocal $(TESTSUITE)
	$(SHELL) ## not finished TODO

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
$(TESTSUITE): $(srcdir)/testsuite.at
# $(TESTSUITE): $(srcdir)/testsuite.at $(srcdir)/package.m4
	$(AUTOTEST) -I ’$(srcdir)’ -o $@.tmp $@.at
	mv $@.tmp $@
