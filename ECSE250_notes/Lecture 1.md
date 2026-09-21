*How to do well*
1. lectures
2. tutorials
3. problem sets
4. ask questions

## Java

*compiled and interpreted*

Compile: write code, then compiler converts into machine language. (eg. C)

Interpreted: interpreter runs through the code line by line and executes immediately. (eg. Python)
```python
x = 5
print(x)
print(y)
```
print out x
never executes `print y`
if compiled language, the compiler would detect the error before executing

Java code --> compiler --> byte code --> Java virtual machine (reads line by line) --> output

#### Code example
```python
print("HelloWorld")
```

```java
public class HelloWorld {
	public static void main (String[] args){
		system.out.println("HelloWorld");
	}
}
```

1. Class name must match file name ==H==ello==W==orld.java
	- all code inside class
	- at most 1 public class
2. name of method (function) (99% of executable code)
	- void = return type 
3. statements should end  with ";"

*Every Java program must have a* `public static void main(String[] args)`
	- if you have multiple classes, you only need to have one of them to have this.