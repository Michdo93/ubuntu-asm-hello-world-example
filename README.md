# ubuntu-asm-hello-world-example
A simple example for Hello World in assembler on Ubuntu.

## Installation

At first you have to install [NASM](https://www.nasm.us/):

```
sudo apt update
sudo apt install nasm
```

This is the project webpage for the Netwide Assembler (NASM), an asssembler for the x86 CPU architecture portable to nearly every modern platform, and with code generation for many platforms old and new.

## Create your code:

Then we have to write our code. You can create it with `nano hello.asm`

```
section .data
    hello db 'Hello, World!', 0

section .text
    global _start

_start:
    ; Schreiben von "Hello, World!" auf die Konsole
    mov     rax, 1                  ; SYS_WRITE
    mov     rdi, 1                  ; fd (Standardausgabe)
    lea     rsi, [hello]            ; Zeiger auf den String
    mov     rdx, 13                 ; Länge des Strings
    syscall

    ; Beenden des Programms
    mov     rax, 60                 ; SYS_EXIT
    xor     rdi, rdi                ; Exit-Code 0
    syscall
```

## Build the executable:

At least you have to build the executable:

```
nasm -f elf64 hello.asm -o hello.o
ld hello.o -o hello
```

You can run it with:

```
./hello
Hello, World!
```
