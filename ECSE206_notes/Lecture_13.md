#### Libraries
- A collection of functions
- Header files contain declarations and macros for C programs
	- located in /usr/include
	- For example, stdio.h contains the prototype for printf
	- linker will link the code for printf from the libc.so file

printf
- % format specifier
	- c: character
	- d or i: signed decimal integer
	- f: float
	- s: string
- flags
	-: left justify the width (default is right)
	+: ensure the positive number is prefixed with + sign
- %5.1: width 5, 1 decimal place

#### Array
declaration syntax: `int a[10]` (items of the same type)
when declaring an array inside a function, the default values are undefined
![[Screenshot 2026-10-20 at 20.01.43.png|595]]

##### Accessing uninitialized values (no compiling error)
声明后**默认不会自动初始化为 0**（为追求执行效率），里面存的是原本残留在内存里的随机旧数据（垃圾值）
**正确做法：** 永远要在使用变量/数组之前进行初始化，例如：
```C
int a[5] = {0}; // 将数组所有元素初始化为 0
```

##### Accessing out-of-bounds values (no compiling error)An example of a confusing mistake
```c
int a[5];
int i;
for (i=1;i<=5;i++) a[i]=0;
```
if i's location is next to `a[4]` in memory, then `a[5]=0` will set i to 0 and cause infinite loop
##### sizeof
Can be used for arrays
```c
int i[5];
printf("The array itself hs size %zu bytes\n", sizeof(i));
//20bytes
printf("Its elements have size %zu/n", sizeof(i[0]));
//整数型为4bytes
printf("The length of the array is %zu\n", sizeof(i)/sizeof(i[0]));
```
==sizeof() format specifier is %zu==

##### Multi-dimensional arrays
In reality, in memory the elements are stored continuously in row order

#### Pointers

Memory is divided into bytes
Each bytes has an address
for example: 4bytes integer i located at address 200
![[Screenshot 2026-10-20 at 21.01.18.png|263]]
The address of the first byte is the address of the variable

A pointer variable stores the address of a variable
e.g. pointer variable p stores the address to i
![[Screenshot 2026-10-20 at 21.05.11.png|179]]

##### Syntax: `type *variable`
`int *p` means that p is a pointer variable that can point to an object of type int

##### Address-of operator(&)
Returns the address of a variable
```c
int i;
int *p=&i;
```

##### Dereference operator(\*)
```c
int i;
int *p=&i; //points to i's memory address
i = 5;
printf("%d", i); //pirnts 5
printf("%d", *p); //pirnts 5 instead of the address stored in p
*p = 2; //通过解引用将 p 所指向的内存空间的值改为了 2
printf("%d", i); //pirnts 2
printf("%d", *p); //pirnts 2
```

Note:
- `int *p` and `int* p` are equivalent (one is the dereferenced value of p is int and another is type of p is a pointer-to-int)
- `int* p, q` p is a pointer q is an int here
-  So it's better to write in this way `int *p, *q`
-  Can make p = q so they point to the same object