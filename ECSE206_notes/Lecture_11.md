### Introduction to C 
- Systems programming language
	- machine-level concepts
	- operations close to computer instructions
	- easier than assembly
	- used for OS, database engines, game engines, embedded systems, interpreters
	- small, fast, permissive and portable
#### How is C run?
source code --> gcc compiler --> a.out (default) containing machine code (execute directly on CPU)

Use `gcc` command to execute .c file
- syntax: `gcc FLAGS FILES`
- without a flag, it compiles to the default file
- `-o` replace the a.out name with your own
	- `gcc helloworld.c -o hello`
- a.out is executed this same way as bash script

```c
/* 
Hello 
world 
Program 
*/

#include<stdio.h> 
//standard io library
//two functions from it: getc(), puts()

int main (void){
	puts("Hello world!");
	return 0 //error code
}
```
- puts(): print a string to stdout
- getc(): reads a character from stdin
	- returns ascii code
#### Basic structure of C
```c 
#include <stdio.h>
int main(void){ //main is where an application starts its execution
char c;

puts("Freshman: ");
c = getc(stdin)

if (c == 'Y' || c == 'y') //no {} no :
	puts("Welcome\n");
else
	puts("Sorry, try again.\n");
	
return 0;
}
```


C compilation process
![[Screenshot 2026-10-09 at 12.37.33.png]]

```c
int main(int argc, char *argv[]){
//main函数的标准写法
//argc is like %#
//argv[1] is like $1
//argv[2] is like $2, etc.
//char * means string in C
	int n;
	for (n=0; n<argc; n++)
		printf("%\n", argv[n])
		
	return 0;
}

```