#*************************************************************#
#
#   Ensemble, 2_00
#   Copyright 2004 Cornell University, Hebrew University
#           IBM Israel Science and Technology
#   All rights reserved.
#
#   See ensemble/doc/license.txt for further information.
#
#*************************************************************#
#*************************************************************#
#
# DEMO directory base Makefile
#
# Author: Mark Hayden, 8/96
# Massive changes, Ohad Rodeh 12/2001
#*************************************************************#
ENSROOT = ../..
include $(ENSROOT)/mk/config.mk
include $(ENSROOT)/mk/preamble.mk
#*************************************************************#
# Choose whether to use the optimizing compiler or not.
#

ifdef OPT
include $(ENSROOT)/mk/ocamlopt.mk
else
include $(ENSROOT)/mk/ocaml.mk
endif

#*************************************************************#
PROGS = \
	$(ENSBIN)/mtalk$(EXE) \
	$(ENSBIN)/gossip$(EXE) \
	$(ENSBIN)/ensembled$(EXE)

TESTS = \
	$(ENSBIN)/rand$(EXE) \
	$(ENSBIN)/fifo$(EXE) \
	$(ENSBIN)/socktest$(EXE) \
	$(ENSBIN)/perf$(EXE) \
	$(ENSBIN)/armadillo$(EXE) 

PROG_OBJS= mtalk$(CMO) gossip$(CMO) ensembled$(CMO)
TEST_OBJS= rand$(CMO) fifo$(CMO) perf$(CMO) socktest$(CMO) armadillo$(CMO)

PROG_EXEC= _exec_prog-$(PLATFORM)$(EXE)
TEST_EXEC= _exec_test-$(PLATFORM)$(EXE)
#*************************************************************#

.SUFFIXES: .ml .cmo .cmx .mli .cmi
.mli.cmi:
	ocamlc $(MLFLAGS) -I $(ENSLIB) -c $<
.ml.cmo:
	ocamlc $(MLFLAGS) -I $(ENSLIB) -c $<
.ml.cmx:
	ocamlopt $(MLFLAGS) -I $(ENSLIB) -c $<

#*************************************************************#

all: $(PROGS)

opt: 
	$(MAKE) OPT=1 all

tests: all $(TESTS)

$(PROG_EXEC): $(PROG_OBJS) $(ENSCONFDEP)
	$(MLLINK) $(MLLINKFLAGS) -o $(PROG_EXEC) $(LIBSYS) $(ENSCONF) $(CRYPTO_LINK) $(PROG_OBJS) 

$(TEST_EXEC): $(TEST_OBJS) $(ENSCONFDEP)
	$(MLLINK) $(MLLINKFLAGS) -o $(TEST_EXEC) $(LIBSYS) $(ENSCONF) $(CRYPTO_LINK) $(TEST_OBJS) 

#*************************************************************#
# Standard demos.  We link/copy the _exec program to the names
# of the various demos.  It's all the same executable, which
# does different things depending on its name.  This is a
# hack, but worth the savings in link time.

$(ENSBIN)/gossip$(EXE): $(PROG_EXEC)
	$(CP) $(PROG_EXEC) $(ENSBIN)/gossip$(EXE)

$(ENSBIN)/mtalk$(EXE): $(PROG_EXEC)
	$(CP) $(PROG_EXEC) $(ENSBIN)/mtalk$(EXE)

$(ENSBIN)/ensembled$(EXE): $(PROG_EXEC)
	$(CP) $(PROG_EXEC) $(ENSBIN)/ensembled$(EXE)

#*************************************************************#
#internal tests

$(ENSBIN)/rand$(EXE): $(TEST_EXEC)
	$(CP) $(TEST_EXEC) $(ENSBIN)/rand$(EXE)

$(ENSBIN)/fifo$(EXE): $(TEST_EXEC)
	$(CP) $(TEST_EXEC) $(ENSBIN)/fifo$(EXE)

$(ENSBIN)/perf$(EXE): $(TEST_EXEC)
	$(CP) $(TEST_EXEC) $(ENSBIN)/perf$(EXE)

$(ENSBIN)/armadillo$(EXE): $(TEST_EXEC)
	$(CP) $(TEST_EXEC) $(ENSBIN)/armadillo$(EXE)

$(ENSBIN)/socktest$(EXE): $(TEST_EXEC)
	$(CP) $(TEST_EXEC) $(ENSBIN)/socktest$(EXE)

#*************************************************************#

clean:
	$(CLEANDIR)
	$(RM) _exec* 

realclean: clean

#depend:
#	ocamldep -I $(ENSLIB) *.ml *.mli > $(DEPEND)

#include $(DEPEND)

#*************************************************************#



