FLAGS=-Wall -Wextra -Wpedantic -pedantic-errors -Werror -Winline
SRC=main.c
NUM_ERR=5

all: clang gcc

clang:
	clang ${FLAGS} ${SRC} -ferror-limit=${NUM_ERR}

gcc:
	gcc   ${FLAGS} ${SRC} -fmax-errors=${NUM_ERR}
