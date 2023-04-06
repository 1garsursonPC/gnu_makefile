#################################################
############ CONFIGURATION VARIABLE #############
#################################################

NAME ?= foo

SRCDIR ?= src
HDRDIR ?= hdr
OBJDIR ?= obj

LDFLAGS ?=
CFLAGS ?= -Wall -Wextra -Werror


#################################################
################### MAKEFILE ####################
#################################################

OBJFILES := main.o greeter.o
OBJFILES := $(OBJFILES:%.o=$(OBJDIR)/%.o)
HDRFILES := greeter.h
HDRFILES := $(HDRFILES:%.h=$(HDRDIR)/%.h)

.PHONY: clean
.DELETE_ON_ERROR:

$(NAME): $(OBJFILES)
	$(CC) $(LDFLAGS) -o $@ $^

$(OBJDIR)/%.o: $(SRCDIR)/%.c $(HDRFILES)
	@mkdir -p $(dir $@)
	$(CC) -c $(CFLAGS) -I $(HDRDIR)/ -o $@ $<

clean:
	rm -rf $(OBJDIR)
	rm -f $(NAME)
