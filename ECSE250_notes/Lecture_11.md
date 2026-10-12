#### Interfaces

abstract method: 
	A class must contain a certain method but implementation is left to subclass.
interfaces:
	Specify a set of methods a class must implement
```java
public abstract class Shape{
	public double getArea();
}

public interface Shape{
	public double getArea();
}

public class Circle implements Shape{
	public double getArea(){
		//implementation
	}
}
```
Just like abstract class, interfaces cannot be instantiated
```java
Shape s = new Shape(); //wrong
Shape s = new Circle(); //right
```
##### Abstract Class vs. interface
1. Abstract classes have fields
2. Classes only extend 1 class, but can implement multiple interfaces
3. An interface can extend multiple interfaces
```java
public interface Shape{
	public double getArea();
}

//2.
public interface Colour{
	public String getColour();
}

public class Circle implements Shape, Colour{
	public double getArea(){
		//implementation
	}
	public String getColour(){
		//implementation
	}
}

//3.
pulic interface A{
	public void mA;
}

public interface B extends A{
	public void mB();
}
//Any class implementing B must provide an implementation for mA and mB
```

##### Interfaces can also contain:
- static constants (final)
```java
public interface Shape{
	public static final double PI = 3.14159;
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
	//must override log()
}
```

```java
public interface A{
	public void log()
}

public interface B{
	public void log(String s);
}

//C must implement log() and log(String s)
//Overloading
}
```
![[Screenshot 2026-10-10 at 18.01.45.png|495]]

List of Student:
`Student[] s = new Student[0]`

find first element: `public Student getFirst();`

```java
public class StudentList{
	private Student[] students;
	pulic Student(int nRStudents){
		Srtudents = new Student[nRStudents];
	}
	public Student getFirst(){
		return Student[0];
	}
}

public interface List{
	public Student getFirst();
	public Student getLast();
	public void addLast(Student s);
	
	//problem: only works for Students
}
```
Solution - Generic type:
```java
public interface List<T>{
	public T getFirst();
	public T getLast();
	public void addLast(T t) //T is generic type
}

public class Student implements List<Student>{
	public void addLast(Student s){
	
	}
}
List<Student> s = new List<Student>;

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