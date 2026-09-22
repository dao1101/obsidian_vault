---
create: 2026-09-08
---
### Conditional statement 

```java
if(x>0)
{
	System.println(); //executes regardless of x
}
else{} //x does not compile --> no if block attached
```

```java
public class Main {
	public static void main(String[] args){
		int x = 3;
		int y;
		String myS = "a";
		
		switch(myS) {
			case "a":
				y = 1;
				break;
			case "b":
				y = 3;
				break;
			default:
				y = 0;
			
		}
	}
}
```

### While loop

```java
int x=0;
while(x<5){
	x++;
}
```
evaluate x<5
- true: execute body
- false: skip to after loop 
- it wil execute 5 times

### For loop

```java
for (int i=0; i<5; i++){ /*(initialize; condition; increment)*/
                         /*(execute once; check before every iteration; execute                              at the end of the iteration)*/
}
```

```java
int j=0;

for (int i=0; i<10; j++){
	i++; 
	//if this statement is not there, the exit condition will never be reached
	System.out.println(j);
}
```

### Scope of a variable

 A *local* variable only  exists in side the block in which it is declared (cannot access outside block)

e.g.
==compile error==
```java
int x=5;
if(x>0){     //variable can only exists once per block
	int y=0;
} else{
	int y=2;
}
System.out.print(y); 
//==compile error== since when each block is the done, the memory of the y is erased
//we need to make sure that when we get to the print statement, y still exists
```

Correction
```java
int x=5;
int y;
if(x>0){     //variable can only exists once per block
	int y=0;
} else{
	int y=2;
}
System.out.print(y); 
```

```java
int i;
for (i=0; i<10; i++){
// can access i here
}
i=i+1 //cannot access i here
```

```java
String x = "a";
if(true) {
	x = "a";
}else{
	int x = 3;
}
```
 *Note: two ==declared ==variables cannot have the same name if they are in the same scope*
 

### Data type

1. Primitive data type
	- predefined by language
	- 8 in Java
		- byte
		- short
		- int 
		- long
			- ^integers
		- float
		- double
			- ^decimals
		- char
			- ^character
		- boolean
			- ^trueorfalse

	![[Screenshot 2026-09-08 at 14.06.57.png|578]]

Integer overflow: jumping back to the minimum intger 