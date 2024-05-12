ACEUNIT_HOME:=../../
vpath %.c $(ACEUNIT_HOME)/lib/
include $(ACEUNIT_HOME)/lib/Makefile
CC=clang
LD=clang
CFLAGS+=-fprofile-instr-generate -fcoverage-mapping
LDFLAGS+=-fprofile-instr-generate -fcoverage-mapping
test: export LLVM_PROFILE_FILE=$^.profraw

all: coverage-report

coverage-report: test/AceUnit_SimpleRunner_Test.profdata test/AceUnit_SetJmpRunner_Test.profdata test/AceUnit_AbortRunner_Test.profdata test/AceUnit_ForkRunner_Test.profdata
	llvm-cov show test/AceUnit_SimpleRunner_Test -instr-profile=test/AceUnit_SimpleRunner_Test.profdata
	llvm-cov show test/AceUnit_SetJmpRunner_Test -instr-profile=test/AceUnit_SetJmpRunner_Test.profdata
	llvm-cov show test/AceUnit_AbortRunner_Test -instr-profile=test/AceUnit_AbortRunner_Test.profdata
	llvm-cov show test/AceUnit_ForkRunner_Test -instr-profile=test/AceUnit_ForkRunner_Test.profdata

%.profdata: %.profraw
	llvm-profdata merge -sparse $^ -o $@

%.profraw: %
	LLVM_PROFILE_FILE=$@ ./$*

clean::
	$(RM) *.profraw *.profdata
	$(RM) -r test/
