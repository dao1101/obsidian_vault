
default floating point --> double

```java
double d = 1.0;
double e = 1; //converted to 1.0
int f = 1.0 //error
```

*note: if all operands are integers, the result is an integer*
```java
int a = 1/4 //a=0
double b = 1/4 //0.0 since both operands are integers
double c = 1.0/4 //0.25
```
- char: to represent a characer
	- `char c = 'a'` single quotes are for char variables, double for strings
	- Characters are stored as binary numbers (16 bits)
	- Every character has its own unique code (ASCII)
		- ASCII is an extension of unicode
	```java
	char x = 'a';
	//only one character allowed
	char y = 97; //prints 'a'
	char y = y + 1 //y='b'
	
	char d = '!'; //33
	char e = '"'; //34
	char f = d + e; 
	//Not compiled
	//note: 加减乘除mod对字符能用
	//d+e is considered an integer operation
	//result is type `int` --> can't put that back into char
	```

	
```java
char x = 'a';

char b = 'a' + 1; 
//compiled
//operatoins between 2 constants --> compile knows that it fits in a char

char b = x + 1; 
//error, not compiled
//compiler cannot know whether the result is in the range of char
//在编译器的眼中，x的值在运行时是可能会改变的（比如后面可能会被修改）编译器不会去赌 `x` 里的值到底是多少
//Java 的算术提升规则：Java 规定，任何 `char`、`byte`、`short` 只要参与算术运算，它们的值都会自动提升（Promote）为 `int` 类型
//因此，`x + 1` 的表达式结果类型是 `int`（占用 32 位）
//Java 不允许将一个 `int` 隐式赋值给 `char`（占用 16 位），因为这可能导致高位截断（数据丢失）。所以编译器直接阻断并报错
```

Typecasting
- convert between types
- telling the compilers to treat a variable as if it were a different type
```java
char f = 'a';
char g = (char)(f+1);
```
*Need explicit casting if result might not fit*

Is `char g = (char)(f) + 1` enough?
- no, the integer operation is outside the casting, so it still treats it as integers

```java
double x = 1; //implicit casting
int a = (int)3.0;
int b = (int)3.5; //always rounded down 
```
`

```java
public class L04b {
	
	public static void main(String[] args){
		addTwoNumbers(1, 2); //can execute since java is compiled
		int x = 1;
		int y = 2;
		addTwoNumber(x, y) 
	}
	public static int addTwoNumbers(int n1, int n2){
		//at beginning, with above code, n1=1, n2=2
		int x = n1 + n2;
		n1++; //n1 = 2
		return x;
	}
}
```
