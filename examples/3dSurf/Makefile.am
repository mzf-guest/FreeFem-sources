############################################################################
# This file is part of FreeFEM.                                            #
#                                                                          #
# FreeFEM is free software: you can redistribute it and/or modify          #
# it under the terms of the GNU Lesser General Public License as           #
# published by the Free Software Foundation, either version 3 of           #
# the License, or (at your option) any later version.                      #
#                                                                          #
# FreeFEM is distributed in the hope that it will be useful,               #
# but WITHOUT ANY WARRANTY; without even the implied warranty of           #
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the            #
# GNU Lesser General Public License for more details.                      #
#                                                                          #
# You should have received a copy of the GNU Lesser General Public License #
# along with FreeFEM. If not, see <http://www.gnu.org/licenses/>.          #
############################################################################
# SUMMARY : Makefile for FreeFEM
# LICENSE : LGPLv3
# ORG     : LJLL Universite Pierre et Marie Curie, Paris, FRANCE
# AUTHORS : ...
# E-MAIL  : ...

LOG_DRIVER = $(SHELL) $(top_srcdir)/bin/test-driver-ff
TESTS_ENVIRONMENT = TEST_FFPP=$(TEST_FFPP) FLAGS_FFPP=-nw LIST_CONDITIONAL="$(LIST_CONDITIONAL)"

all-local: all.edp freefem++.pref

TESTS_OTHER = buildMeshSfromMesh3.edp \
	glu3DSurf.edp \
	Laplace3dSP2.edp \
	LaplacianSurf.edp \
	operatorsOnMeshS.edp \
	extractSurfFromMesh3.edp \
	testvtk.edp \
	LapP1withflux.edp \
	cauchyproblem.edp \
	periodicS.edp Connectivite-S.edp \
	LaplaceRT1Surf.edp


TESTS_TETGEN = HeatTorus.edp

TESTS_MMG = Pinocchio.edp

if TETGEN
CONDITIONAL_TETGEN = $(TESTS_TETGEN)
endif

if MMG
CONDITIONAL_MMG = $(TESTS_MMG)
endif

TESTS = $(TESTS_OTHER) \
	$(TESTS_TETGEN) \
	$(TESTS_MMG)

LIST_CONDITIONAL = $(TESTS_OTHER) \
	$(CONDITIONAL_TETGEN) \
	$(CONDITIONAL_MMG)

XFAIL_TESTS = buildMeshSfromMesh3.edp \
	Laplace3dSP2.edp

EXTRA_DIST = *.edp all.edp

all.edp: Makefile
	(echo "NoGraphicWindow=true;NoUseOfWait=true;int verbosityy=verbosity;int MEM1234=storageused();"; \
	for i in *`ls *.edp|grep -v -E '^(all|regtests|makeref|ref)\.edp$$'` ; do \
		echo ' cout << "--------- file : '$$i' --------------------------------------------------------" << endl;' ;\
		echo "verbosity=verbosityy;searchMethod=0;" ; \
		echo \{ include \"$$i\"\;\}\; ;\
		echo ' cout << " mem leak = " <<storageused() - MEM1234 << endl << "------------------------------------------------------------------------------ " << endl;' ;\
	done) > $@


freefem++.pref:Makefile
	echo includepath = \"../../idp/\" > freefem++.pref
	echo loadpath = \"../../plugin/seq/\" >> freefem++.pref

FORCE:
