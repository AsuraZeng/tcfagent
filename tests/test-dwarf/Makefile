TCF_AGENT_DIR=../../agent

include $(TCF_AGENT_DIR)/Makefile.inc

override CFLAGS += $(foreach dir,$(INCDIRS),-I$(dir)) $(OPTS)

HFILES := $(foreach dir,$(SRCDIRS) tcf/backend,$(wildcard $(dir)/*.h)) $(HFILES)
CFILES := $(sort $(foreach dir,$(SRCDIRS) tcf/backend,$(wildcard $(dir)/*.c)) $(CFILES))

EXECS = $(BINDIR)/dwarf-test$(EXTEXE)

all:    $(EXECS)

$(BINDIR)/libtcf$(EXTLIB) : $(OFILES)
	$(AR) $(AR_FLAGS) $@ $^
	$(RANLIB)

$(BINDIR)/dwarf-test$(EXTEXE): $(BINDIR)/tcf/main/main$(EXTOBJ) $(BINDIR)/libtcf$(EXTLIB)
	$(CC) $(CFLAGS) -o $@ $(BINDIR)/tcf/main/main$(EXTOBJ) $(BINDIR)/libtcf$(EXTLIB) $(LIBS)

$(BINDIR)/%$(EXTOBJ): %.c $(HFILES) Makefile
	@$(call MKDIR,$(dir $@))
	$(CC) $(CFLAGS) -c -o $@ $<

$(BINDIR)/%$(EXTOBJ): $(TCF_AGENT_DIR)/%.c $(HFILES) Makefile
	@$(call MKDIR,$(dir $@))
	$(CC) $(CFLAGS) -c -o $@ $<

clean:
	$(call RMDIR,$(BINDIR))
