#### The Object Class
- every class is a subclass of Object

| Object    |
| --------- |
| ^         |
| Student   |
| ^         |
| FTStudent |

#### Methods
- `equals() 01==02` (compare ref)
	- String overrides equals()
- `toString()`: create a string representation of the object
	- output example: ca.mcgill.ecse.registration.Student@h2b6
	- package.Class.id(hashcode in hex)
- `hashCode()`: returns the internal address of the object
- We typically overrides these methods
- Getters/Setters: access or change value of field, since all fields are generally private.

#### Immutable type 
Recall

|        | create new object to  a variable | change object field content   |
| ------ | -------------------------------- | ----------------------------- |
| array  | yes                              | yes                           |
| String | yes                              | no (class has no such method) |

- Type where all fields are private and no setters
```java
public class Student(){
	private String name;
	private int id;
	private int[] grades;
	...
}
```
![[Screenshot 2026-10-10 at 10.57.29.png|276]]
```java
public void main(){
	Student s1 = new Student("KP", 1, new int[10]);
	String name = s1.getName();
	name = "KS"; //does not change the field in s1, string is immutable
				 //fieldname `name` stilll points to "KP"
				 //creates antoher local variable `name` containing "KS"
	int[] sGrades = s1.getGrades(); //`sGrades` 和 `s1.grades` 指向的是同一个数组
	sGrades[0] = 1; //s1.grades[0] get modified
	
}
```
光是"所有字段 private + 没有 setter"并不足以保证不可变。String 字段安全是因为 String 本身不可变,但数组字段会通过 getter 泄漏内部引用

To avoid access to private field
Solution: create a copy
```java
public int[] getGrades(){
	return this.grade // nooo
	
	//create a copy
	int[] copy = new int[this.grades.length]; 
	for (int i = 0; i < grades.length; i++) { 
		copy[i] = this.grades[i]; 
	} 
	return copy;
	
	//or
	
	return this.grades.clone();
}
```
**构造函数也要做同样的事**,否则外面还握着原数组的引用:
```java
public Student(String name, int id, int[] grades) {
    this.name = name;
    this.id = id;
    this.grades = grades.clone()); // 防御性拷贝存在字段里
}
public int[] getGrades(){
	return this.grades.clone();
}
```

#### Abstract Classes
当一组类有共同的状态和行为,但"父类本身不该被单独创建",且有些行为必须由子类各自决定时,用抽象类。
![[Screenshot 2026-10-10 at 11.23.15.png|661]]

```java
public abstract class Student{
	//cannot be instantiated
	//can only be created with subclass
	//still has fields, methods, constructors
	private String name;
	
	public String getName(){
		//implementation
	}
	
	public void setName(){
		//implementation
	}
	//子类不用重复这些方法和字段直接继承
}
```
##### Abstract methods
- implementation must be in subclass
- only signature, no body
- **实现抽象方法(也是 override)**:父类只有签名,没有方法体,子类**必须**写。不然编译器报错
```java 
public abstract class Student{
	public abstract void study();
	//if theres `abstract` keyword in a method, any subclass must implement it
}

public class FTStudent extends Student{
	public void study(){
		System.out.print("I am studying");
	}
}
```