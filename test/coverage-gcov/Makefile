ACEUNIT_HOME:=../../
vpath %.c $(ACEUNIT_HOME)/lib/
include $(ACEUNIT_HOME)/lib/Makefile
CFLAGS+=--coverage -ftest-coverage -fprofile-arcs
LOADLIBES+=-lgcov

all: coverage-report

.PHONY: coverage-report
coverage-report: test/AceUnit_SimpleRunner.c.gcov test/AceUnit_SetJmpRunner.c.gcov test/AceUnit_AbortRunner.c.gcov test/AceUnit_ForkRunner.c.gcov
	lcov -c -d . -o coverage.info
	genhtml coverage.info -o coverage-report

%.gcov:
	gcov $*

clean::
	$(RM) *.gcno *.gcov *.gcda coverage.info
	$(RM) -r test/ coverage-report
