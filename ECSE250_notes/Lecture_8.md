#### static

- 若需要对对象自身属性的操作与读写，就不加static
- 若是工具函数，如Math.pow()或不需要依赖对象状态的操作

static field --> belongs to entire class

```java
private static double minGPA=2.0
//only 1 slot in memory for this variable
//NOT one per instance

Student s = new Student();
	s.minGPA; //语法正确但是不推崇
	//or
	Student.minGPA=2.5;
```


| minGPA --> | 2.0  |
| ---------- | ---- |
| S1 -->     | name |
|            | id   |
| S2 -->     | name |
|            | id   |
|            |      |

Static methods belong to the entire class
- cannot be called *on* objects the way non-static methods are
	- **非 static 方法**：`对象.方法()` $\rightarrow$ 必须依靠某个具体的对象来发起调用，方法内部有 `this`
	- **static 方法**：`类名.方法(参数)` $\rightarrow$ 是全类共享的独立逻辑，即使你把对象作为参数传进去，它也不是“在那个对象上执行”（not on the object）
- methods that manage the flow of the execution of code (e.g. MainClass must be static)

```java
public void setName(String newName){
	this.name = newName;
}

public static void changeName(Student stu, String newName){
	stu.setName(newName);
}

changeName(s, newName:"KP");
```

Passing object variables in methods
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
	
	int lockerNO; //added fields
}

public class FTStudent extends Student{ 
//subclass FTStudent inherits superclass Student
	//only declares the specific fields
	private int lockerNO;
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