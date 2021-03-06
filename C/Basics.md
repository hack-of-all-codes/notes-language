# C Basics

## Steps to Run a C Program:
* Code
```c
/*
 * filename: hello.c
 * every C file should start with a comment explaining
 * what the code this
 */
#include <stdio.h>

//this is a one-liner comment
int main()
{
	puts("Hello World C-Style");
	return 0;
}
```
* Compile
```
> gcc hello.c -o hello
```
* Run
```
> ./hello

//combine compile and run:
> gcc hello.c -o hello && gcc hello.c -o hello
```

## The "main" function
* C programs start with the main() function
* It returns an int, 0 if successful, otherwise it failed
```c
int main() {
	return 0;
}
```
* Main can also accept parameters
```
> ./program param1 param2 param3
```
```c
int main(int argc, char *argv[]) 
{
	for (int i=1; i<argc; i++) {
		printf("%i = %s\n", i, argv[i]);
	}
	return 0;
}
```
* Named options are also accepted
```
> ./program -a -n "El Awesomo" aaa bbb ccc
```
```c
//accepts options and normal params:
//-a = boolean to enable, no argument needed
//-n = your name, needs arguments
int main(int argc, char *argv[]) 
{

	char ch;
	while ((ch = getopt(argc, argv, "an:")) != EOF) {
		switch (ch) {
			case 'a':
				printf("Awesomeness enabled!\n");
				break;
			case 'n':
				printf("Name: %s\n", optarg); //no idea where this came from
				break;
			default:
				printf("Error: Unknown Parameter\n");
				return 1;
		}
	}

	//no idea where optind came from
	argc -= optind;
	argv += optind;

	//outputs the trailing arguments
	for (int i=0; i<argc; i++) {
		printf("%i = %s\n", i, argv[i]);
	}
	return 0;
}
```

## Compile and Link Multiple Files
```
> gcc app.c helper.c -o app && ./app
```
```c
/*
 * file: app.c
 */
#include "helper.h"

int main() {
	do_something();
 	return 0;
}
```
```c
/*
 * helper.h
 */
void do_something();
```
```c
/*
 * file: helper.c
 */
#include <stdio.h>

void do_something() {
	printf("Test\n");
}
```

## Compile Individual Files
* Compile ALL source files in the directory (this will generate **.o files)
```
> gcc -c *.c
```
* Link All Compiled Files
```
> gcc *.o -o app 
```
* If you just changed one file, just compile the updated files and link them again
```
> gcc -c changed_file.c
> gcc *.o -o app 
```

## Basic I/O
```c
int main()
{
	//basic output
	puts("Enter a Positive Number:\n");

	int number;

	//basic input
	scanf("%i", &number);

	if (number < 0) {
		puts("This is not a valid number");
		return -1; //program failed
	}

	//formatted output
	printf("%i is an awesome number\n", number);
	return 0;
}
```

## Preprocessor
```c
/*
 * file: app.h
 */

//invalid if undeclared in C99, will probably work with a warning in C11 because int functions are implicit for undeclared functions
int an_int_function(); 

//required: this will not compile if removed
float a_float_function();
```
```c
/*
 * file: app.c
 */
#include <stdio.h>

//preprocessor: inserts the contents of the file before compilation
//alternative: insert the declaration HERE (same effect)
#include "app.h"

int main() 
{
	printf("Running\n");
	int my_int = an_int_function();
	float my_float = a_float_function();

	printf("%i - %f\n", my_int, my_float);
}

int an_int_function()
{
	return 222;
}

float a_float_function() {
	return 1.011111;
}
```

## Using "make" for Builds
* Source Files:
```c
/*
 * file: app.c
 */
#include "helper.h"

int main() {
	do_something();
 	return 0;
}

/*
 * helper.h
 */
void do_something();

/*
 * file: helper.c
 */
#include <stdio.h>
#include "helper.h"

void do_something() {
	printf("Test\n");
	printf("Testsss\n");
}
```
* create the file: "makefile"
```make
app.o: app.c helper.h
	gcc -c app.c

helper.o: helper.h helper.c
	gcc -c helper.c

app: app.o helper.o
	gcc app.o helper.o -o app
```
* build using the make command
```cmd
> make app
```

### References:
[Gnu C Language Reference](http://www.gnu.org/software/gnu-c-manual/gnu-c-manual.html)
