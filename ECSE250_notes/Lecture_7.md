### OOP

Objects: group of relevant pieces of data

| Student                      |          |
| ---------------------------- | -------- |
| name: String<br>Id: int <br> | (data)   |
| Study()                      | (method) |
class
- where our program runs (main)
- template for creating objects (instance of a class)

```java
public class Student{
	
	private String name;
	public int id;
	//fields: delcare at beginning of class, outside of methods
	//where you want to store your data
	
	/*
	access modifier:
	private: only methods inside class can access
	public: any method can access
	*/
}

public class Main{
	public ... {
		Student s = new Student; 
		//if field is public		
		s.id = 12345
		s.name //error, private, cannot be accessed outside class
	}
}

```

If no public/private specified: package-private by default
- which means only the classes in the same package (folder) can have access to it
- package name must be the same as the folder name

Example (correct)
```java
package people;
public class Student {...}
```

```java
package buildings;
public class Resident{
	Student resident; 
	//have access since Student is a public class
	//even in different packages
}
```

Example (wrong)
```java
package people;
class Student {...} //no public
```

```java
package buildings;
public class Resident{
	Student resident;
	//compile error
}
```

One file usually contains only one class, *especially public class*, and the same name as file name.

==In general, fields are set to private, while methods are set to public.==

#### Fields vs Local Variables?

Field: declared for class and is used anywhere in class.
Local variables: declared inside a method

#### Constructor
- special method used to create object 

```java
public Student(){}
//default constructor; fields set to default values
```

```java
public Student (String sName, int sID){ //second letter upper case
	name = sName;
	id = sId;
} //to initialize object
```

```java
Class Main() { 
	Student s = new Student();
	Student s2 = new Student ("KP", 123);
}
//can delare multiple constructors
```

| Null         | <-- s  |
| ------------ | ------ |
| 0            |        |
| "KP" address | <-- s2 |
| 123          |        |


#### Other methods
- called on specific object
```java
s2.study(); //correct
Student.study()//wrong
```

- `this` method
```java
public void study(){
	System.out.println(name+"is studying");
	//same as
	System.out.println(this.name + "is studying")
	//`this` is the object on which the method is called
}
```

```java
public Student(String name, int id){
	this.name = name; //second name is local variable
	this.id = id;
	//object being called
	//`this` is necessary
	//在实际开发中，大家更习惯把参数名和属性名写成一模一样，这时候就必须使用`this`来防止“名称遮蔽”（Name Shadowing）
}
```

```java
Class Main{
	void main(){
		Student s = new Student();
		System.out.print(this.name); //error, `this`cannot use outside of Student
		System.out.print(s.name)//depends on accessibility
	}
}
```