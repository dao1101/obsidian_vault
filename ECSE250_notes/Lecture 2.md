```java
/*multi 
line
comment
*/
public class HellowWorld{            //block definition
	public static void main (String[]args){
		System.out.println("hello"); //statement
	}
}
```

Indentation does not matter in java as long as there are brakckets

### Variable
1. Declaration `int number` (type_name; reserved a space in the memory called number)
2. Initialization `number = 5` (the RHS much match the data type)

### Operators
1. Arithmetic operator
	- / : 
		- 3 / 2 =1; (if both operands are integers --> integer devision)
	- % : 
		- Remainder of division, ==modulus work both with integers and floating points==
		- 3 % 1.5 = 0; (0 is floating point)
		- 3 % 2 = 1;  `int % int = int`
	- + : 
		- 3 + 1.5 = 4.5;
		- "a" + "b" = "ab"; (concatenation)
		- 2 + 3 + "5" = "55" (addition until seeing a string)
		- "2" + 3 + 5 = "235";
		- "2" + (3 + 5) = "28";

2. Relation operators
	- 5 == 5 --> true
	- `boolean result = 5 == 5;` (declaration assignment)
	- boolean variable is default to be false

3. logical operators (between boolean variables)
	- NOT(!), AND(&&), OR(||)

4. Compound assignment and increment/decrement operators

x += 5 <--> x = x + 5
```java
int x = 2;
x += "5" //cannot be compiled since x date type is int
```

```java
int x = 1;
x++; //x = x + 1
x--; //x = x - 1
```

```java
int x = 5;
int y = 2*x++; //use the stored value of x first then increment on x
x = x + 2
```
```text
output
y=10, x=8
```

```java
int x = 5;
int y = 2*x++ +x; //execute from left to right 括弧另说
```

```java
int x = 1;
int y = 2* ++x + x; //increment before using the x value
```

5. Conditional statements
```java
if (x>0) {
} else if {
} else {
}
```
- **`if`**: Evaluates first. If its condition is **true**, its block runs, and the rest of the chain (`else if` / `else`) is completely skipped.
    
- **`else if`**: Only executes if the previous `if` condition was **false** **AND** its own condition is **true**
	
- **`else`**: Only executes if **ALL** preceding `if` and `else if` conditions were **false**.