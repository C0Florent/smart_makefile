NAME	=	autobin

SRC	=	main.c	\
		long.c

OBJ	=	$(SRC:.c=.o)

all: $(NAME)

$(NAME): $(OBJ) $(DEPFILES)
	$(CC) $(CFLAGS) $(LDFLAGS) $^ -o $@

DEPFILES = $(SRC:.c=.d)

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

## @brief Function to generate a message describing why a rule is run
##
## @param $1 The name of the output file
## @param $2 The list of changed files
define REMAKE_MSG
Remaking \e[1;31m$1\e[0m because {\e[1;34m$2\e[0m} changed.
endef

%.o %.d &: %.c
	@echo -e '$(call REMAKE_MSG,$@,$(call commasep,$?))'
	@$(CC) -c $< -o $*.o -MMD -MF $*.d -MT '$*.o $*.d'

include $(DEPFILES)
