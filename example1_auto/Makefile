NAME	= my_test

SRC	=	main.c	\
		long.c

OBJ	=	$(SRC:.c=.o)

all: $(NAME)

$(NAME): $(OBJ)
	$(CC) $(LDFLAGS) $(CFLAGS) $^ -o $@

main.o: defs.h

clean:
	rm -f $(OBJ)

fclean: clean
	rm -f $(NAME)

re: fclean all

.PHONY:	all clean fclean re
