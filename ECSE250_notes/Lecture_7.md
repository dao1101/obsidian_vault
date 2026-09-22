### OOP

Objects: group of relevant pieces of data

| Student (object)                   |
| ---------------------------------- |
| name: String<br>Id: int <br>(data) |
| Study (method)                     |
class
- where out program runs (main)
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
		s.name //private, cannot be accessed outside class
	}
}

```

If no public/private specified: package-private by default