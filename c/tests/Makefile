CC = gcc
CFLAGS = -std=c99 -pedantic -Wall -D_XOPEN_SOURCE=500 -D_BSD_SOURCE -g -DENDEBUG
LFLAGS =
OBJECTS = test.c

all: clean test

test :
	$(CC) $(LFLAGS) $(CFLAGS) $(OBJECTS) -o test 

clean:
	rm -f test

.PHONY: clean
