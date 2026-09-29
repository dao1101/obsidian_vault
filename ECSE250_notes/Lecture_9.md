Overriding: subclass method has same name, parameters, and same return type as super class.
- @override used to tell the compiler that i'm overriding a superclass's method
```java
// 父类
class Student {
    String name;

    public void study() {
        System.out.println(name + " is studying");
    }
}

// 子类：必须使用 extends 继承父类
class FTStudent extends Student {
    
    //@Override 是注解，写在被重写的方法上方，用于检查语法是否正确
    @Override 
    public void study() {
        // Java 中要用 System.out.println，而不是 print
        System.out.println("The FTStudent is studying"); 
    }
}

// 测试类（方法调用必须在方法内部，比如 main 方法）
public class Test {
    public static void main(String[] args) {
        FTStudent s = new FTStudent();
        s.study(); // 输出: The FTStudent is studying
    }
}
```

Overloading: 2+ methods in same class with same name, but different parameters
- 简化命名：不需要为功能相似但入参不同的方法取一堆复杂的名字
```java
class Student{
	String name;
	public void study(){
		System.out.print(name+"is studying")
	}
	public void study(String friend){
		print(name+"is studying with"+friend);
	}
}
```

```java
Student s = new Student("kp", 123);
s.study(); //kp is studying
s.study("mp") //kp is studying with mp
```

|             | diff. return type | diff. parameters | same class   | same method name |
| ----------- | ----------------- | ---------------- | ------------ | ---------------- |
| overloading | yes               | yes              | yes          | yes              |
| overriding  | no                | no               | no(subclass) | yes              |

#### Final keyword
```java
public final class Student{}
//can't be extended

public final int n = 10
// can't be changed, compile error if you trynna change it 

public final void study()
//can't be overriden
```

#### Class Casting
![[IMG_2856.jpg|518]]
![[IMG_2857.jpg|519]]
```java
Student s1 = new FTStudent();
Student s2 = new Student();
// polymorphism

((FTStudent)s1).openLocker() //compiles
((FTStudent)s2).openLocker() // ClassCastException 父类不能强行转为子类
```

![[IMG_2858.jpg|549]]
![[IMG_2859.jpg|551]]

```java
Stduent s1 = new FTStudent("KP", 123, 7);
System.out.pritnln(s1 instanceof Student);   //true
System.out.pritnln(s1 instanceof FTStudent); //true since FT inherited Student

Stduent s2 = new Student("KP", 12345);
System.out.pritnln(s2 instanceof Student);   //true
System.out.pritnln(s2 instanceof FTStudent); //false
```



