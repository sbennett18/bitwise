TARGET = ion

CC = clang
NR_ERR = 5

CFLAGS  = -I$(INCDIR) -Wall -Wextra -Wpedantic -pedantic-errors -Werror
CFLAGS += -Winline -Wmissing-prototypes -Wstrict-prototypes

DEFS =
LIBS = -lm

SRCS = $(wildcard *.c)
OBJS = $(addprefix $(OBJDIR)/, $(SRCS:.c=.o))
HDRS = $(wildcard $(INCDIR)/*.h)
#HDRS  = $(patsubst $(INCDIR)/%, %, $(_HDRS))

OBJDIR = ../obj
INCDIR = ../include
LIBDIR = ../lib

ifeq ($(CC),gcc)
	CFLAGS += -fmax-errors=$(NR_ERR)
else
	CFLAGS += -ferror-limit=$(NR_ERR)
endif

V    := 0
AT_0 := @
AT_1 :=
AT    = $(AT_$(V))

#$(warning A top-level warning $(OBJECTS))
.PHONY: all
all: $(TARGET)


$(OBJDIR)/%.o: %.c $(HDRS)
	@echo $<
	$(AT)$(CC) $(CFLAGS) -c $< -o $@


$(TARGET): $(OBJS)
	$(AT)$(CC) -o $@ $^ $(CFLAGS) $(LIBS)


.PHONY: clean
clean:
	$(AT)rm -rf $(OBJDIR) core


$(OBJS): | $(OBJDIR)


$(OBJDIR):
	$(AT)mkdir -p $@


.PHONY: TAGS
TAGS: $(SRCS)
# make requires escaping $ as $$
	$(AT)$(CC) -M -I$(INCDIR) $(SRCS) \
		| sed -e 's/[\\ ]/\n/g' \
		| sed -e '/^$$/d' -e '/\.o:[ \t]*$$/d' \
		| ctags -f ../tags -L - --c++-kinds=+p --fields=+iaS --extra=+fq --tag-relative=yes
