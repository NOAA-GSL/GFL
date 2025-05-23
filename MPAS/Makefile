.SUFFIXES: .F .o

all: dummy GFL_physics

dummy:
	echo "****** compiling GFL_physics ******"

OBJS = \
	module_cu_gfl_mpas.o       \
	module_cu_gfl_deep.o \
	module_cu_gfl_sh.o

# DEPENDENCIES:
module_cu_gfl_mpas.o: \
	module_cu_gfl_deep.o \
	module_cu_gfl_sh.o

module_cu_gfl_sh.o: \
	module_cu_gfl_deep.o

GFL_physics: $(OBJS)
	ar -ru ./../../libphys.a $(OBJS)

clean:
	$(RM) *.f90 *.o *.mod
	@# Certain systems with intel compilers generate *.i files
	@# This removes them during the clean process
	$(RM) *.i

.F.o:
ifeq "$(GEN_F90)" "true"
	$(CPP) $(CPPFLAGS) $(COREDEF) $(CPPINCLUDES) $< > $*.f90
	$(FC) $(FFLAGS) -c $*.f90 $(FCINCLUDES) -I../.. -I../../../../framework -I../../../../external/esmf_time_f90
else
	$(FC) $(CPPFLAGS) $(COREDEF) $(FFLAGS) -c $*.F $(CPPINCLUDES) $(FCINCLUDES) -I../.. -I../../../../framework -I../../../../external/esmf_time_f90
endif
