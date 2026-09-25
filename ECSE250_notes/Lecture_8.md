
#### static
static field --> belongs to entire class

```java
private static double minGPA=2.0
//only 1 slot in memory for this variable
//NOT one per instance

Student s = new Student();
	s.minGPA;
	//or
	Student.minGPA=2.5;
```


| minGPA | 2.0  |
| ------ | ---- |
| S1     | name |
|        | id   |
| S2     | name |
|        | id   |
|        |      |


Static methods belong to the entire class
- cannot be called *on* objects
- methods that manage the flow of the execution of code (e.g. MainClass must be static)

```java
public void setName(String newname){
	this.name = newName;
}

public static void changeName(Student stu, String newName){
	stu.setName(newName);
}

changeNmae(s, newName:"KP");
```

Passing object variabels in methods
- variable is passed as a reference(not copy)
	- original student is modified
- modifying student keeps it in same place in the memory

Inheritance
- Full-time students are allowed a locker
- instead of copying pasting Student into FTStudent, we use inheritance

```java
public class FTStudent{
	String name;
	int id;
	int lockerNO;
}

public class FTStudent extends Student{ 
//subclass FTStudent inherits superclass Student
	//only declares the specific fields
	private int lovkerNO;
	public FTStudent(String name, int id, int lockerNO){
		this.name=name; //error, private fields
						//this.name is inherited
		super(name,id); //call Student(constructor)
		this.lockerNO=#
	}
}
FTStudent fts=new FTStudent("KP", 1234567);
//write constructor for object lockerNO

class FTEngStudent extends FTStudent {
	String PNUColour;
	public FTEngStudent(String name, int id, int lockerNO, String colour){
		super(name,id,lockerNO);
		this.PNUColour = colour;
	}
}
```