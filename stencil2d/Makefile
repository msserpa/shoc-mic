# Basics
CC	 = icpc
CPP      = icc
LD	 = icc
CXX      = icc
SHOCROOT =..

# Related folders
BINDIR		= $(SHOCROOT)/bin
COMMON_DIR	= ../common
VPATH		= $(COMMON_DIR)

# Object files
COMMON_SHOC_OBJS = main.o Option.o OptionParser.o ResultDatabase.o Timer.o ProgressBar.o
COMMON_OBJS	 = InvalidArgValue.o CommonMICStencilFactory.o MICStencilKernel.o MICStencilFactory.o MICStencil.o
BENCH_OBJS 	 = Stencil2Dmain.o COMMON_OBJS COMMON_SHOC_OBJS
BENCHMARKPROG 	 = $(patsubst %.o,$(BINDIR)/%,$(BENCH_OBJS))

# Compilation Flags
CFLAGS  = -O2 -openmp -I./ -I$(COMMON_DIR) -opt-assume-safe-padding -no-opt-prefetch -opt-threads-per-core=4 -restrict -opt-streaming-stores always -opt-streaming-cache-evict=0
LDFLAGS = -openmp

%.o: %.cpp
	$(CC) -c $< $(CFLAGS) $(CXXFLAGS)

$(BINDIR)/%: %.o
	$(CC) -o $@ $(CFLAGS) $(CXXFLAGS) $(LDFLAGS) $(COMMON_SHOC_OBJS) $(COMMON_OBJS) $< $(LIBS)

all : $(BENCHMARKPROG)

$(BENCHMARKPROG) : $(COMMON_OBJS) $(COMMON_SHOC_OBJS)

clean :
	rm *.o -f
	rm ../bin/Stencil2Dmain -f

# Individual targets

stencil2d : $(BINDIR)/Stencil2D

$(BINDIR)/Stencil2D : $(COMMON_OBJS)
