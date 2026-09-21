```java
int[][] numbers = {{1},{1,2},{1,2,3}};

int[]n = numbers[2];
//copying address in new variable
//n = {1,2,3}

numbers[2][0] = 4;
//--> n[0]=4
//n={4,2,3}

numbers[2] = new int[3];
//{4,2,3} will not be garbage collected since it still refers to n
```

### Primitive vs. Reference

- Primitive holds values: `int a =3` a holds 3
- Reference holds a reference to memory `String s = "hi"` s content is 0xFF (an address)

```java
int[] x = new int[5];
	system.print(x);
	//x = {0,0,0,0,0} as default
	//but it prints out a hexadecimal address
```

```java
public static void main(String[] args){
	int x = 5;
	int y = x;
	x++;
	System.out.println(x + " " + y);
	//x=6, y=5
}
```

```java
public static void main(String[] args){
	int[] x = {1,2,3};
	int[] y = x;
	y[0] = 4;
	System.out.println(x[0] + " " + y[0]);
	//x[0]=y[0]=4
}
```

### Types of errors
1. Compile-time errors
	- code cannot run
	- syntax

2. Run-time errors
	- during execution
	- detected by JVM
	- e.g. /0, index out of bounds
```java
int[] x = null;

//x is declared but contains no address

int y = x.length
//error
//it went to look for where x is in memory and give its length
```

3. Null Pointer Exception 
	- Try to access info of variable with value null
	- Exceptions thrown in case of runtime error before crash
```java
int[]x = {1,2,3};
int y = x[5];
//ArrayIndexOutOfBoundsException
```

***You can prevent the code from crashing upon exception using try/catch blocks***
```java
try{
	//code that might throw an exception
} catch(Exception e){ //exceptions are variables and objects in java
	//code that JVM should execute 
} 
//continue your code 
```

```java
//Nested catch block
try{
} catch(NullPointerExceptione){
} catch(ArithmeticException e){
}
//the second there is an exception that is caught the code move on
```

```java
public static void main(String[] args){
	int[]x = new int[5];
	try{
		System.out.println(x[5]);
	} catch (NullPointerEzception e){
		System.out.println(e.getMessage());
		//error message printed
	}
	System.out.println(x[0]);
	//0
}
```

```java
//something crazy
public static void main(String[] args){
	int[]x = new int[5];
	try{
		System.out.println(x[5]);
	} catch (NullPointerEzception e){
		System.out.println(e.getMessage());
		//error message printed
		try{
			int y = 2/0;
		
		} catch(ArithmeticException otherE){
			System.out.println(otherE.getMEssage());
		}
	}
	System.out.println(x[0]);
}

//result
//error messages
//0
```


### OOP


