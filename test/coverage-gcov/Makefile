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

test/AceUnit_SimpleRunner_Test.o test/AceUnit_SetJmpRunner_Test.o test/AceUnit_AbortRunner_Test.o test/AceUnit_ForkRunner_Test.o: | test/

test/:
	mkdir -p test/

clean::
	$(RM) *.gcno *.gcov *.gcda coverage.info
	$(RM) -r test/ coverage-report
