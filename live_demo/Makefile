NAME	=	autobin

SRC	=	main.c	\
		long.c

OBJ	=	$(SRC:.c=.o)

DEPFILES	=	$(SRC:.c=.d)

all: $(NAME)

$(NAME): $(OBJ)
	$(CC) $(LDFLAGS) $(CFLAGS) $^ -o $@

clean:
	rm -f $(OBJ)

fclean: clean
	rm -f $(NAME)

re: fclean all

.PHONY:	all clean fclean re

$(DEPFILES):

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@ -MMD -MF $*.d -MT $@

include $(DEPFILES)
