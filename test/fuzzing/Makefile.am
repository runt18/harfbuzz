# Process this file with automake to produce Makefile.in

NULL =
EXTRA_DIST =
CLEANFILES =
DISTCLEANFILES =
MAINTAINERCLEANFILES =

# Convenience targets:
lib:
	@$(MAKE) $(AM_MAKEFLAGS) -C $(top_builddir)/src fuzzing

$(top_builddir)/src/libharfbuzz-fuzzing.la: lib

EXTRA_DIST += \
	README \
	$(NULL)

check_PROGRAMS = \
	hb-fuzzer \
	$(NULL)

AM_CPPFLAGS = \
	-DHB_DISABLE_DEPRECATED \
	-I$(top_srcdir)/src/ \
	-I$(top_builddir)/src/ \
	$(NULL)
LDADD = \
	$(top_builddir)/src/libharfbuzz-fuzzing.la \
	$(NULL)

hb_fuzzer_SOURCES = \
	hb-fuzzer.cc \
	$(NULL)
hb_fuzzer_LDADD = \
	$(LDADD) \
	$(NULL)
hb_fuzzer_CPPFLAGS = \
	$(AM_CPPFLAGS) \
	-DMAIN \
	$(NULL)

check:
	cat $(top_srcdir)/test/shaping/tests/fuzzed.tests | \
	cut -d: -f1 | xargs ./hb-fuzzer

-include $(top_srcdir)/git.mk
