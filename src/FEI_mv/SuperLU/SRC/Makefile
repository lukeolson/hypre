# makefile for sparse supernodal LU, implemented in ANSI C
include ../make.inc

#######################################################################
#  This is the makefile to create a library for SuperLU.
#  The files are organized as follows:
#
#       ALLAUX -- Auxiliary routines called from all precisions of SuperLU
#	LAAUX  -- LAPACK auxiliary routines called from all precisions
#	SLASRC -- LAPACK single precision real routines
#	DLASRC -- LAPACK double precision real routines
#	CLASRC -- LAPACK single precision complex routines
#	ZLASRC -- LAPACK double precision complex routines
#       SCLAUX -- LAPACK Auxiliary routines called from both real and complex
#       DZLAUX -- LAPACK Auxiliary routines called from both double precision
#                 and complex*16
#	SLUSRC -- Single precision real SuperLU routines
#       DLUSRC -- Double precision real SuperLU routines
#	CLUSRC -- Single precision complex SuperLU routines
#       ZLUSRC -- Double precision complex SuperLU routines
#
#  The library can be set up to include routines for any combination
#  of the four precisions.  To create or add to the library, enter make
#  followed by one or more of the precisions desired.  Some examples:
#       make single
#       make single double
#       make single double complex complex16
#  Alternatively, the command
#       make
#  without any arguments creates a library of all four precisions.
#  The library is called
#       superlu.a
#  and is created at the next higher directory level.
#
#  To remove the object files after the library is created, enter
#       make clean
#
#######################################################################

#######################################
### added for hypre
#######################################
include ../../../config/Makefile.config
CINCLUDES = ${INCLUDES} ${MPIINCLUDE}
C_COMPILE_FLAGS = \
 -I$(srcdir)\
 -I$(srcdir)/../../../\
 -I$(srcdir)/../../../utilities\
 ${CINCLUDES}

HEADERS =\
 colamd.h\
 slu_ddefs.h\
 slu_util.h\
 supermatrix.h
#######################################

### LAPACK 
LAAUX 	= lsame.o xerbla.o
SLASRC 	= slacon.o 
DLASRC	= dlacon.o
CLASRC	= clacon.o scsum1.o icmax1.o
ZLASRC	= zlacon.o dzsum1.o izmax1.o
SCLAUX 	= slamch.o
DZLAUX 	= dlamch.o

### SuperLU 
ALLAUX 	= superlu_timer.o util.o memory.o get_perm_c.o mmd.o \
	  sp_coletree.o sp_preorder.o sp_ienv.o relax_snode.o \
	  heap_relax_snode.o colamd.o

SLUSRC = \
	sgssv.o sgssvx.o \
	ssp_blas2.o ssp_blas3.o sgscon.o  \
	slangs.o sgsequ.o slaqgs.o spivotgrowth.o \
	sgsrfs.o sgstrf.o sgstrs.o scopy_to_ucol.o \
	ssnode_dfs.o ssnode_bmod.o \
	spanel_dfs.o spanel_bmod.o sreadhb.o \
	scolumn_dfs.o scolumn_bmod.o spivotL.o spruneL.o \
	smemory.o sutil.o smyblas2.o

DLUSRC = \
	dgssv.o dgssvx.o \
	dsp_blas2.o dsp_blas3.o dgscon.o \
	dlangs.o dgsequ.o dlaqgs.o dpivotgrowth.o  \
	dgsrfs.o dgstrf.o dgstrs.o dcopy_to_ucol.o \
	dsnode_dfs.o dsnode_bmod.o \
	dpanel_dfs.o dpanel_bmod.o dreadhb.o \
	dcolumn_dfs.o dcolumn_bmod.o dpivotL.o dpruneL.o \
	dmemory.o dutil.o dmyblas2.o

CLUSRC = \
	scomplex.o cgssv.o cgssvx.o csp_blas2.o csp_blas3.o cgscon.o \
	clangs.o cgsequ.o claqgs.o cpivotgrowth.o  \
	cgsrfs.o cgstrf.o cgstrs.o ccopy_to_ucol.o \
	csnode_dfs.o csnode_bmod.o \
	cpanel_dfs.o cpanel_bmod.o creadhb.o \
	ccolumn_dfs.o ccolumn_bmod.o cpivotL.o cpruneL.o \
	cmemory.o cutil.o cmyblas2.o

ZLUSRC = \
	dcomplex.o zgssv.o zgssvx.o zsp_blas2.o zsp_blas3.o zgscon.o \
	zlangs.o zgsequ.o zlaqgs.o zpivotgrowth.o  \
	zgsrfs.o zgstrf.o zgstrs.o zcopy_to_ucol.o \
	zsnode_dfs.o zsnode_bmod.o \
	zpanel_dfs.o zpanel_bmod.o zreadhb.o \
	zcolumn_dfs.o zcolumn_bmod.o zpivotL.o zpruneL.o \
	zmemory.o zutil.o zmyblas2.o

#######################################
### changed for hypre
#######################################

FILES =\
 colamd.c \
 dcolumn_bmod.c \
 dcolumn_dfs.c \
 dcopy_to_ucol.c \
 dgscon.c \
 dgsequ.c \
 dgsrfs.c \
 dgssv.c \
 dgssvx.c \
 dgstrf.c \
 dgstrs.c \
 dlacon.c \
 dlangs.c \
 dlaqgs.c \
 dmemory.c \
 dpanel_bmod.c \
 dpanel_dfs.c \
 dpivotgrowth.c \
 dpivotL.c \
 dpruneL.c \
 dreadhb.c \
 dsnode_bmod.c \
 dsnode_dfs.c \
 dsp_blas2.c \
 dsp_blas3.c \
 dutil.c \
 get_perm_c.c \
 heap_relax_snode.o \
 memory.o \
 mmd.c \
 relax_snode.c \
 sp_coletree.c \
 sp_ienv.c \
 sp_preorder.c \
 superlu_timer.c \
 slu_util.c

OBJS = ${FILES:.c=.o}

all: libHYPRE_superlu${HYPRE_LIB_SUFFIX}
	cp -fp *.h $(HYPRE_BUILD_DIR)/include
#	cp -fp libHYPRE* $(HYPRE_BUILD_DIR)/lib

install: libHYPRE_superlu${HYPRE_LIB_SUFFIX}
	cp -f *.h $(HYPRE_INC_INSTALL)
#	cp -f libHYPRE* $(HYPRE_LIB_INSTALL)
	@echo  " "

clean:
	rm -f *.o libHYPRE*
	rm -rf pchdir tca.map *inslog*
distclean: clean

libHYPRE_superlu.a: ${OBJS}
	@echo  "Building $@ ... "
	${AR} $@ ${OBJS}
	${RANLIB} $@

libHYPRE_superlu.so: ${OBJS}
	@echo  "Building $@ ... "
	${BUILD_CC_SHARED} -o $@ ${OBJS}

${OBJS}: ${HEADERS}

#######################################

all4:    single double complex complex16

single: $(SLUSRC) $(ALLAUX) $(LAAUX) $(SLASRC) $(SCLAUX)
	$(ARCH) $(ARCHFLAGS) ../$(SUPERLULIB) \
		$(SLUSRC) $(ALLAUX) $(LAAUX) $(SLASRC) $(SCLAUX)
	$(RANLIB) ../$(SUPERLULIB)

double: $(DLUSRC) $(ALLAUX) $(LAAUX) $(DLASRC) $(DZLAUX)
	$(ARCH) $(ARCHFLAGS) ../$(SUPERLULIB) \
                $(DLUSRC) $(ALLAUX) $(LAAUX) $(DLASRC) $(DZLAUX)
	$(RANLIB) ../$(SUPERLULIB)

complex: $(CLUSRC) $(ALLAUX) $(LAAUX) $(CLASRC) $(SCLAUX)
	$(ARCH) $(ARCHFLAGS) ../$(SUPERLULIB) \
		$(CLUSRC) $(ALLAUX) $(LAAUX) $(CLASRC) $(SCLAUX)
	$(RANLIB) ../$(SUPERLULIB)

complex16: $(ZLUSRC) $(ALLAUX) $(LAAUX) $(ZLASRC) $(DZLAUX)
	$(ARCH) $(ARCHFLAGS) ../$(SUPERLULIB) \
		$(ZLUSRC) $(ALLAUX) $(LAAUX) $(ZLASRC) $(DZLAUX)
	$(RANLIB) ../$(SUPERLULIB)


##################################
# Do not optimize these routines #
##################################
slamch.o: slamch.c ; $(CC) -g -c ${SHARED_COMPILE_FLAG} $<
dlamch.o: dlamch.c ; $(CC) -g -c ${SHARED_COMPILE_FLAG} $<
superlu_timer.o:  superlu_timer.c ; $(CC) -g -c -DNO_TIMER ${SHARED_COMPILE_FLAG} $<
##################################

#.c.o:
#	$(CC) $(CFLAGS) $(CDEFS) $(BLASDEF) -c $< $(VERBOSE)

#clean:	
#	rm -f *.o ../libsuperlu_3.0.a
