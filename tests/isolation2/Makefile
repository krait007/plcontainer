#------------------------------------------------------------------------------
# 
# Copyright (c) 2016-Present Pivotal Software, Inc
#
#------------------------------------------------------------------------------

PGXS := $(shell pg_config --pgxs)
include $(PGXS)

PSQLDIR = $(bindir)

.PHONY: default
default: all

.PHONY: all
all: tests

gpstringsubs.pl:
	rm -f $@ && ln -s $(top_builddir)/src/test/regress/gpstringsubs.pl
gpdiff.pl: atmsort.pm explain.pm
	rm -f $@ && ln -s $(top_builddir)/src/test/regress/gpdiff.pl

atmsort.pm:
	rm -f $@ && ln -s $(top_builddir)/src/test/regress/atmsort.pm
explain.pm:
	rm -f $@ && ln -s $(top_builddir)/src/test/regress/explain.pm


.PHONY: resgroup
resgroup: gpdiff.pl gpstringsubs.pl
	@echo "Tests require three runtime configurations. Will check the three"
	$(top_builddir)/src/test/regress/pg_isolation2_regress --init-file=../init_file --psqldir='$(PSQLDIR)' --inputdir=$(srcdir) --resgroup-dir=resgroup --dbname=isolation2resgrouptest --schedule=isolation2_resgroup_schedule
