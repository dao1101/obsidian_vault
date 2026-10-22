#### Interfaces

Recall: abstract method 
	A class must contain a certain method's signature but implementation is left to subclass.
interfaces:
	Specify a set of methods a class must implement
```java
public abstract class Shape{
	public abstract double getArea();
	//or 
	public double getArea(){
		//implementation
	}
}
```

```java
public interface Shape{ //public abstract by default so can neglect public 
	public double getArea(); //only signature
}

public class Circle implements Shape{
	public double getArea(){
		//implementation must
	}
}
```
Just like abstract class, interfaces cannot be instantiated
```java
Shape s = new Shape(); //wrong
Shape s = new Circle(); //right
```
##### Abstract Class(description of a type) vs. interface(what can it do)
1. Abstract classes have fields
2. Classes only extend 1 class, but can implement multiple interfaces不允许两个父类但允许实现多个接口
3. An interface can extend multiple interfaces
```java
public interface Shape{
	public double getArea();
}

public interface Colour{
	public String getColour();
}
//2.
public class Circle implements Shape, Colour{
	public double getArea(){
		//implementation
	}
	public String getColour(){
		//implementation
	}
	//两个接口的方法都得实现
}

//3.
public interface A {
	public void mA();
}

public interface B extends A{ //interface A's sub interface, can extend multiple
	public void mB();
}
//Any class implementing B must provide an implementation for mA and mB
```

##### Interfaces can also contain:
- static constants (final)
```java
public interface Shape{
	public static final double PI = 3.14159; 
	//public static final by default in interfaces, can neglect
	//Shape.PI
}
```
- default methods: methods with implementation
```java
public default void log(String str){
	System.out.print("Logging " + str);
}
//in interface
//can be overriden 
```
- static methods: helper methods
```java
public interface Shape{
	static double sqaure(double x){
		return x*x;
	}
}
//属于接口本身,通过 `Shape.square(3)` 调用。
//不会被实现类继承,`Circle` 对象不能调用它,只能写 `Shape.square(...)`。
//用来放和这个接口相关的辅助方法。
```
##### Override
```java
public interface A{
	public default void log(){
		System.out.print("Log from A");
	}
}

public interface B{
	public default void log(){
		System.out.print("Log from B");
	}
}

public class C implements A, B{
	//C同时从A和B继承了log()，编译器不知道用哪个所以强制C自己重写
	//must override log()
	//重写时也可以选一个来调用
	@override
	public void log(){
		A.super.log(); //明确调用A的版本
	}
}
```
##### Overload
```java
public interface A{
	public void log();
}

public interface B{
	public void log(String s);
}

//C must implement log() and log(String s)
//Overloading
public class C implements A, B {
	public void log(){
		//implementation
	}
	public void log(String s){
		//implementation
	}
} 
//这里两个方法参数不同，不冲突，C把两个都实现就行
```

![[Screenshot 2026-10-21 at 14.41.46.png]]

![[Screenshot 2026-10-10 at 18.01.45.png|495]]

###### List of Student:
`Student[] s = new Student[0]`

find first element: `public Student getFirst();`

```java
public interface List{
	public Student getFirst(); //Student写死了
	public Student getLast();
	public void addLast(Student s);
	
	//problem: only works for Students
}

public class StudentList implements List{
	private Student[] students;
	pulic StudentList(int nRStudents){
		students = new Student[nRStudents];
	}
	public Student getFirst(){
		return students[0];
	} 
}
```
Solution - Generic type:
```java
public interface List<T>{
	public T getFirst();
	public T getLast();
	public void addLast(T t); //T is generic type
}

public class StudentList implements List<Student>{
	public void addLast(Student s){
		//implementation
	}
}

List<Student> s = new StudentList();
//s的类型是List（接口），意思s可以指向任何实现了List的对象

public class Home<T> {
	private T occupant;
	public void moveIn(T animal){
		occupant = animal;
	}
}

Home<Dog> dogHouse = new Home<Dog>(); //Dog extends animal
Dog snoopy = new Dog();
dogHouse.moveIn(snoopy);
```
![[Screenshot 2026-10-10 at 18.11.25.png]]