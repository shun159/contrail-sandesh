.PHONY: protocol transport
SUBDIRS := protocol transport

CFLAGS := -I.
SRC := $(wildcard *.c)
OBJ := $(patsubst %.c,%.o,$(SRC))
DEP := $(patsubst %.c,%.d,$(SRC))
PROG := $(patsubst %.c,%,$(SRC))

all: $(DEP)
	@$(MAKE) $(OBJ)
	@$(MAKE) -C protocol
	@$(MAKE) -C transport

clean:
	@$(RM) $(DEP) $(OBJ) $(PROG)
	@$(MAKE) clean -C protocol
	@$(MAKE) clean -C transport

ifneq ($(filter clean,$(MAKECMDGOALS)),clean)
-include $(DEP)
endif

%.d: %.c
	$(info GEN $@)
	@$(CC) -MM $(CFLAGS) $< | sed 's/\($*\)\.o[ :]*/\1.o $@ : /g' > $@

%: %.d
