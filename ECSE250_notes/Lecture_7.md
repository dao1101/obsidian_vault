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
package buidings;
public class Resident{
	Student resident;
	//compile error
}
```

One file usually contains only one class, *especially public class*, and the same name as file name.

In general, fields are set to private, while methods are set to public.

#### Fields vs local 