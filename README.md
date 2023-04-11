# OS_HW2 cimin project

## Project Name
Cimin project

## Description
This project is a project that generates input sequences and provides them to the target program, and finds input sequences in which the target program conflicts. 

1. Open the Crash.json file, load the entire file into memory
2. Adjust the length of the input sequence to generate all possible input sequences
3. Run each input sequence by providing it to the target program
4. Wait for the target program to exit and check the exit status
5. Program crashes and outputs input sequence

The code uses pipes to pass the input sequence to the target program, and reads the output of the target program to check for collisions.

It also uses fork to run the target program, and the parent process checks the termination status of the child process. 

## Run Makefile Description —> Required



## Prerequisite

https://github.com/hongshin/OperatingSystem/tree/hw2/jsmn
https://github.com/hongshin/OperatingSystem/tree/hw2/balance
https://github.com/hongshin/OperatingSystem/tree/hw2/libxml2

You can download the example code of json, balance, and libxml2 through the above address. 

- Jsmn
: open source JSON library
There is a bug in this program that causes heap-buffer overflow errors. 
1. jsmn/build.sh -> Build Program (Detect heap-buffer overflow errors using LLVM Address Sanitizer) -> Create jsondump
2. Crash when jsondump receives jsmn/testcases/crash.json (error)
3. Library files -> jsmn.c, jsmn.h 
4. Test -> jsmn_test.c
5. Build Library -> Run makefile
6. Build Successful -> libjsmn.a Library Gets (with "jsmn.h")

- Libxml2
: Parsing and manipulating formatted data in various markup languages, such as XML and HTML
1. Run libxml2/build.sh -> Build All Libraries and Utilities Programs (xmlint -> Bug with null pointer reference error) 
2. Trigger this bug by running xmlint with the option "—recover —postvalid-" and passing libxml2/testcases/crash.xml as standard input.
==> Build libxml2 library and verify the test case crash.xml file using xmlint
At this point, the error message "Address Sanitizer: SEGV on unknown address" is output as a standard error output
-> The error is a collision caused by NULL pointer reverse reference.

- Balance 
: A program to check that parentheses match correctly in a given string 
Ex) If all parentheses match correctly, such as "((()))" -> success, "(()()()" -> fail
1. balance/build.sh -> Build Program
2. balance/testcases/fail -> infinite loop —> End of test run when time limit is exceeded


## Environment


