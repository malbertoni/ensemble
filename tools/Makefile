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
# MAKEFILE: tools Makefile
#*************************************************************#
ENSROOT = ..
include $(ENSROOT)/mk/preamble.mk
include $(ENSROOT)/mk/config.mk
#*************************************************************#

all : \
	$(ENSBIN)/$(EMRG)

$(ENSBIN)/$(EMRG): 
	ocamlc -c emrg.ml 
	ocamlc -o $(ENSBIN)/$(EMRG) emrg.cmo

clean : 
	$(RM) *.cm*

realclean : clean
#*************************************************************#