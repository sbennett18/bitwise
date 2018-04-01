TARGET = a.out

CC = clang
NR_ERR = 5

CFLAGS  = -I$(IDIR) -Wall -Wextra -Wpedantic -pedantic-errors -Werror
CFLAGS += -Winline -Wmissing-prototypes -Wstrict-prototypes

DEFS =
LIBS = -lm

IDIR = ../include
ODIR = obj
LDIR = ../lib

_HDRS = $(wildcard $(IDIR)/*.h)
#HDRS  = $(patsubst $(IDIR)/%, %, $(_HDRS))

SRCS = $(wildcard *.c)
OBJS = $(patsubst %, $(ODIR)/%, $(SRCS:.c=.o))

ifeq ($(CC),gcc)
	CFLAGS += -fmax-errors=$(NR_ERR)
else
	CFLAGS += -ferror-limit=$(NR_ERR)
endif

V := 1
AT_0 := @
AT_1 :=
AT = $(AT_$(V))

#$(warning A top-level warning $(OBJECTS))
.PHONY: all
all: $(TARGET)


$(ODIR)/%.o: %.c $(_HDRS)
	$(AT)echo $<
	$(AT)$(CC) $(CFLAGS) -c $< -o $@


$(TARGET): $(OBJS)
	$(AT)$(CC) -o $@ $^ $(CFLAGS) $(LIBS)


.PHONY: clean
clean:
	$(AT)rm -rf $(ODIR) core


$(OBJS): | $(ODIR)


$(ODIR):
	$(AT)mkdir -p $@


.PHONY: ctags
ctags:
	# make requires escaping $ as $$
	$(AT)$(CC) -M -I$(IDIR) $(SRCS) \
		| sed -e 's/[\\ ]/\n/g' \
		| sed -e '/^$$/d' -e '/\.o:[ \t]*$$/d' \
		| ctags -L - --c++-kinds=+p --fields=+iaS --extra=+q
