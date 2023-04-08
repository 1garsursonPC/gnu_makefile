#################################################
############ CONFIGURATION VARIABLE #############
#################################################

NAME ?= foo

SRCDIR ?= src
HDRDIR ?= hdr
OBJDIR ?= obj
DEPDIR ?= dep

LDFLAGS +=
CFLAGS += -Wall -Wextra -Werror


#################################################
################### MAKEFILE ####################
#################################################

SRCFILE := main.c greeter.c

DEPFILE := $(SRCFILE:%.c=$(DEPDIR)/%.d)
OBJFILES := $(SRCFILE:%.c=$(OBJDIR)/%.o)
SRCFILE := $(addprefix $(SRCDIR)/,$(SRCFILE))

HDRFILES := greeter.h
HDRFILES := $(HDRFILES:%.h=$(HDRDIR)/%.h)

.PHONY: clean
.DELETE_ON_ERROR:

$(NAME): $(OBJFILES) # default goal
	$(CC) $(LDFLAGS) -o $@ $^

# implicit rule
$(OBJDIR)/%.o: $(SRCDIR)/%.c
	@mkdir -p $(dir $@)
	$(CC) -c $(CFLAGS) -I $(HDRDIR)/ -o $@ $^

$(DEPDIR)/%.d: $(SRCDIR)/%.c
	@echo "Generating $@"
	@mkdir -p $(dir $@)
	@set -e; rm -f $@; \
	$(CC) -I $(HDRDIR)/ -MM $(CFLAGS) $< > $@.$$$$; \
	sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < $@.$$$$ > $@; \
	rm -f $@.$$$$
# end pattern rule

include $(DEPFILE)

clean:
	rm -rf $(OBJDIR)
	rm -rf $(DEPDIR)
	rm -f $(NAME)
