### Data in C

#### Four basic types
- char: represented as an integer(ASCII code). 8bits
- int: C specifies it as 16 bits, but on 32-bits or 64-bits machines, it usually is 32 bits.
- float: 6 digit precision, 32 bits
- double: 15 digits precision, double the size of float, 64 bits![[Screenshot 2026-10-15 at 17.38.41.png|668]]

==Note: actual sizes depend on implementation==
- compilers are only required to follow minimum sizes.
- implementations usually depend on CPU
- `sizeof()` to see the size of a type

#### All other data in C are derived from the previous basic types
- arrays: items of same type
- structures: items of different type
- pointer: address to an object in memory
- unions: items with different types but holding only one value at a time
- Strings do not have their own type. 
	- either `char *` (address to a character)
	- or `char[]` (an array of characters)

#### Variable must be declared for compiler to ==reserve memory for it==.
- you should always initialize a variable before using it
- otherwise C reserve a space for it but does not clean the *garbage data* inside of it

#### Constant
- Once initialized, values cannot be changed
- upper case
- `int const A = 1;` or `cont int A = 2;`

#### typedef
- `typedef oldtypename newtypename;` like alias

==true and false in C can be represented in 1 or non-zero and 0==


### Control Structure

##### if statement
```C
if(condition) single_statement;

if(condition){multiple_statements;}
else if{statements;}
else{statements;}
```
- Ternary/conditional operator
	- (condition) ? true_expression : false_expression;

- switch statement 
```c
switch(expression){ //expression must evaluate to an integer or chracter
	case value1:
	case value2: //match both
		 multiple_statements;
		break; //optional,if not present, automatically goes to the next case block without testing the condition
	case value3: multiple_statements;
		break;
	default: //runs if no match
		multiple_statements;
}
```

##### while loop
```c
while(condition) single_statement;

while(condition) {multiple_statements;}

//eg.
int x = 10;
while(x--); //一直循环知道x=0
```
- do-while loop: similar but condition is evaluated after running block 
```c
int i = 0;
do{
	puts("Hello World!");
	i++;
} while (i<5);
//therefore always run at least once!
```

##### for loop
for(init; condition; iteration)
```c
int x, y;
for (x=0, y=10; x*y<45; x+=2, y--) puts("Hi");
```
- the iteration part is run after each iteration
- all the parts are optional
	- `for(;;);` infinite loop
```c
int x;
for(;;){
	x=scanf("%d", &x) //reads integer from stdin
	
	if(x==5) break; //exits loop
}
```