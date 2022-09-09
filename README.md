The Monty language

Monty 0.98 is a scripting language that is first compiled into Monty byte codes (Just like Python). It relies on a unique stack, with specific instructions to manipulate it. The goal of this project is to create an interpreter for Monty ByteCodes files.

Monty byte code files

Files containing Monty byte codes usually have the .m extension. Most of the industry uses this standard but it is not required by the specification of the language. There is not more than one instruction per line. There can be any number of spaces before or after the opcode and its argument:

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

Monty byte code files can contain blank lines (empty or made of spaces only, and any additional text after the opcode or its required argument is not taken into account:

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

The monty program

    Usage: monty file
        where file is the path to the file containing Monty byte code
    If the user does not give any file or more than one argument to your program, print the error message USAGE: monty file, followed by a new line, and exit with the status EXIT_FAILURE
    If, for any reason, it’s not possible to open the file, print the error message Error: Can't open file <file>, followed by a new line, and exit with the status EXIT_FAILURE
        where <file> is the name of the file
    If the file contains an invalid instruction, print the error message L<line_number>: unknown instruction <opcode>, followed by a new line, and exit with the status EXIT_FAILURE
        where is the line number where the instruction appears.
        Line numbers always start at 1
    The monty program runs the bytecodes line by line and stop if either:
        it executed properly every line of the file
        it finds an error in the file
        an error occured
    If you can’t malloc anymore, print the error message Error: malloc failed, followed by a new line, and exit with status EXIT_FAILURE.
    You have to use malloc and free and are not allowed to use any other function from man malloc (realloc, calloc, …)


Tasks
0. push, pall

Implement the push and pall opcodes.

The push opcode

The opcode push pushes an element to the stack.

    Usage: push <int>
        where <int> is an integer
    if <int> is not an integer or if there is no argument given to push, print the error message L<line_number>: usage: push integer, followed by a new line, and exit with the status EXIT_FAILURE
        where is the line number in the file
    You won’t have to deal with overflows. Use the atoi function

The pall opcode

The opcode pall prints all the values on the stack, starting from the top of the stack.

    Usage pall
    Format: see example
    If the stack is empty, don’t print anything



1. pint

Implement the pint opcode.

The pint opcode

The opcode pint prints the value at the top of the stack, followed by a new line.

    Usage: pint
    If the stack is empty, print the error message L<line_number>: can't pint, stack empty, followed by a new line, and exit with the status EXIT_FAILURE



2. pop

Implement the pop opcode.

The pop opcode

The opcode pop removes the top element of the stack.

    Usage: pop
    If the stack is empty, print the error message L<line_number>: can't pop an empty stack, followed by a new line, and exit with the status EXIT_FAILURE



3. swap

Implement the swap opcode.

The swap opcode

The opcode swap swaps the top two elements of the stack.

    Usage: swap
    If the stack contains less than two elements, print the error message L<line_number>: can't swap, stack too short, followed by a new line, and exit with the status EXIT_FAILURE



4. add

Implement the add opcode.

The add opcode

The opcode add adds the top two elements of the stack.

    Usage: add
    If the stack contains less than two elements, print the error message L<line_number>: can't add, stack too short, followed by a new line, and exit with the status EXIT_FAILURE
    The result is stored in the second top element of the stack, and the top element is removed, so that at the end:
        The top element of the stack contains the result
        The stack is one element shorter



5. nop

Implement the nop opcode.

The nop opcode

The opcode nop doesn’t do anything.

    Usage: nop


