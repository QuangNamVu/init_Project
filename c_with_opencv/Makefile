OPENMP=0
DEBUG=1

CPP=g++
LDFLAGS= `pkg-config --libs opencv`
COMMON= `pkg-config --cflags opencv`

DEPS = $(wildcard src/*.h) Makefile
VPATH=./src/
OBJDIR=./obj/

$(EXEC): $(OBJDIR)Main.o
	$(CPP) $(COMMON) $(CFLAGS) $^ -o $@ $(LDFLAGS)
ifeq ($(OPENMP), 1)
CFLAGS+= -fopenmp
LDFLAGS+= -lgomp
endif

ifeq ($(DEBUG), 1)
CFLAGS+= -O0 -g
endif

OBJ = Main.o

$(OBJDIR)%.o: src/%.cpp $(DEPS)
	$(CPP)  -std=c++11 $(COMMON) $(CFLAGS) -c $< -o $@

OBJS = $(addprefix $(OBJDIR), $(OBJ))

execute: $(OBJS)
	$(CPP) $(COMMON) $(CFLAGS) $^ -o $@ $(LDFLAGS)

obj:
	mkdir -p obj

all: obj $(EXEC)

run: $(EXEC)
	./execute < input/1.txt
