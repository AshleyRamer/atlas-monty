### STACKS, QUEUES - LIFO, FIFO - a.k.a "MONTY"
By Ashley Ramer		Due 04/08/2024 @ 11:59pm 

## Requirements
+ Allowed editors: vi, vim, emacs
+ All your files should end with a new line
+ A README.md file, at the root of the folder of the project is mandatory
+ Your code should use the Betty style. It will be checked using betty-style.pl and betty-doc.pl
+ You allowed to use a maximum of one global variable
+ No more than 5 functions per file
+ You are allowed to use the C standard library
+ The prototypes of all your functions should be included in your header file called monty.h
+ Dont forget to push your header file
+ All your header files should be include guarded
+ You are expected to do the tasks in the order shown in the project

## Compilation and Output
All your files will be compiled on Ubuntu 20.04 LTS using gcc, using the options:
``` 
$ gcc -Wall -Werror -Wextra -pedantic *.c -o monty
```
+ Any output must be printed on stdout
+ Error messages should be printed on stderr

## Data Structures
```
/**
 * struct stack_s - doubly linked list representation of a stack (or queue)
 * @n: integer
 * @prev: points to the previous element of the stack (or queue)
 * @next: points to the next element of the stack (or queue)
 *
 * Description: doubly linked list node structure
 * for stack, queues, LIFO, FIFO
 */
typedef struct stack_s
{
        int n;
        struct stack_s *prev;
        struct stack_s *next;
} stack_t;
```

```
/**
 * struct instruction_s - opcode and its function
 * @opcode: the opcode
 * @f: function to handle the opcode
 *
 * Description: opcode and its function
 * for stack, queues, LIFO, FIFO
 */
typedef struct instruction_s
{
        char *opcode;
        void (*f)(stack_t **stack, unsigned int line_number);
} instruction_t;
```

## The '.m' Extension
```
julien@ubuntu:~/monty$ cat -e bytecodes/000.m
push 0$
push 1$
push 2$
  push 3$
                   pall    $
push 4$
    push 5    $
      push    6        $
pall$
julien@ubuntu:~/monty$
```
Monty byte code files can contain blank lines (empty or made of spaces only, and any additional text after the opcode or its required argument is not taken into account:
```
julien@ubuntu:~/monty$ cat -e bytecodes/001.m
push 0 Push 0 onto the stack$
push 1 Push 1 onto the stack$
$
push 2$
  push 3$
                   pall    $
$
$
                           $
push 4$
$
    push 5    $
      push    6        $
$
pall This is the end of our program. Monty is awesome!$
julien@ubuntu:~/monty$
```

## The Monty Program
+ Usage: monty file
where file is the path to the file containing Monty byte code
+ If the user does not give any file or more than one argument to your program, print the error message USAGE: monty file, followed by a new line, and exit with the status EXIT_FAILURE
+ If, for any reason, its not possible to open the file, print the error message Error: Can't open file <file>, followed by a new line, and exit with the status EXIT_FAILURE
where <file> is the name of the file
+ If the file contains an invalid instruction, print the error message L<line_number>: unknown instruction <opcode>, followed by a new line, and exit with the status EXIT_FAILURE
where is the line number where the instruction appears.
Line numbers always start at 1
+ The monty program runs the bytecodes line by line and stop if either:
it executed properly every line of the file
it finds an error in the file
an error occured
+ If you cant malloc anymore, print the error message Error: malloc failed, followed by a new line, and exit with status EXIT_FAILURE.
+ You have to use malloc and free and are not allowed to use any other function from man malloc (realloc, calloc,etc)
