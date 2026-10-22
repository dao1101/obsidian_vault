#### Type casting

Type conversion
-  Usual arithmetic conversion
	- long double>double>float
- small converted to big if different type 

Casting
syntax: `(type) expression`

#### Printing a pointer address
```c
int i = 5;
int *p = &i;
printf("%d", *p);
printf("%p", (void*) p); //pirnts address e.g.0x7fffe8049bcc
printf("%d", p);
//this will automatilaly try to cast the 
```

#### Pointer to array
You can point to an array by pointing to the address of its first element

```c
int a[5]; //let's say stored at 104
int *p;
p = &a[0];
//or
p = a // the array name is converted to the address of 
```
##### adding integer from a pointer
```c
int a[5];
int *p;

```