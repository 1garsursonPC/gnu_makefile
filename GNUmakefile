#############################################################
################## CONFIGURATION VARIABLES ##################
#############################################################

NAME ?= foo

SRCDIR ?= src
HDRDIR ?= hdr
OBJDIR ?= obj
DEPDIR ?= dep

LDFLAGS +=
CFLAGS += -Wall -Wextra -Werror


#############################################################
#################### INTERNAL VARIABLES #####################
#############################################################

SRCFILE := main.c greeter.c

DEPFILE := $(SRCFILE:%.c=$(DEPDIR)/%.d)
OBJFILES := $(SRCFILE:%.c=$(OBJDIR)/%.o)
SRCFILE := $(addprefix $(SRCDIR)/,$(SRCFILE))

HDRFILES := greeter.h
HDRFILES := $(HDRFILES:%.h=$(HDRDIR)/%.h)


#############################################################
######################### TARGETS ###########################
#############################################################

.PHONY: clean
.DELETE_ON_ERROR:

$(NAME): $(OBJFILES) # default goal
	$(CC) $(LDFLAGS) -o $@ $^

clean:
	rm -rf $(OBJDIR)
	rm -rf $(DEPDIR)
	rm -f $(NAME)


#############################################################
####################### PATTERN RULE ########################
#############################################################

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


#############################################################
######################### INCLUDES ##########################
#############################################################

# if the an include contain targets of its own,
# it must be after the first target (default goal)
include $(DEPFILE)
