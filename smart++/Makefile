NAME	=	autobin

SRC	=	main.c	\
		long.c

OBJ	=	$(SRC:.c=.o)
DEPFILES = $(SRC:.c=.d)

all: $(NAME)

$(NAME): $(OBJ) | $(DEPFILES)
	$(LINK.c) $^ $(OUTPUT_OPTION)

clean:
	$(RM) $(OBJ)

fclean: clean
	$(RM) $(NAME)

re: fclean all

.PHONY: all clean fclean re


comma:=,
empty:=
space:=$(empty) $(empty)

## @brief Function to comma-separate a list of words
##
## @param $1 The list of words to comma-separate
define commasep
$(subst $(space),$(comma)$(space),$1)
endef

## @brief function to produce colour output from a base name
##
## @param $1 The base name of the file
define COLNAMES
\e[1;4;37m$1.o\e[0m and \e[1;4;37m$1.d\e[0m
endef

## @brief Function to generate a message describing why a rule is run
##
## @param $1 The base name of source file
## @param $2 The list of changed files
define UPDATMSG
Updating $(call COLNAMES,$1) because {\e[1;36m$2\e[0m} changed
endef

## @brief Function to generate a message describing why a rule is run
##
## @param $1 The base name of source file
## @param $2 The list of changed files
define BUILDMSG
Building $(call COLNAMES,$1) from \e[1;36m$<\e[0m
endef

box	?=	[]

gbox	:=	\e[1;32m$(box)\e[0m
ybox	:=	\e[1;33m$(box)\e[0m


CPPFLAGS += -MMD -MF $*.d -MT '$*.o $*.d' -MP

%.o %.d &: %.c
	@if [ ! -f "$@" ]; then											\
	 	echo -e '$(gbox) $(call BUILDMSG,$*)';						\
	 else															\
	 	echo -e '$(ybox) $(call UPDATMSG,$*,$(call commasep,$?))';	\
	 fi
	@$(COMPILE.c) $< -o $*.o

include $(DEPFILES)
