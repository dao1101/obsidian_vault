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

|             | diff. return type | diff. parameters | diff. class   | diff. method name | diff. access |
| ----------- | ----------------- | ---------------- | ------------- | ----------------- | ------------ |
| overloading | yes               | yes              | no            | no                | yes          |
| overriding  | no                | no               | yes(subclass) | no                | no           |

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
虽然 `s1` 的引用类型被限制成了 `Student`，但**堆里实际存在的是一个完整的 `FTStudent` 对象**。 （**注意**：因为 `s1` 的声明类型是 `Student`，编译器在编译期只允许你通过 `s1.name` 或 `s1.id` 访问属性；如果你想直接访问 `s1.lockerNO`，编译器会报错，必须强制类型转换 `((FTStudent)s1).lockerNO` 才可以访问。）

![[IMG_2857.jpg|519]]
子类有父类的所有 但是父类没有子类的所有
想要父类声明访问子类的内容只能downcast
- **`s1.study()`**：`s1` 的声明类型是 `Student`，但堆里的实际对象是 `FTStudent`。调用 `study()` 时，JVM 会去调用 `FTStudent` 里重写（Override）的 `study()` 方法。
- 如果当你执行 `s1.study()` 时，因为子类没有重写，JVM 最终去执行的就是在 **`Student` 类里定义的那份 `study()` 代码**。
- **`s2.study()`**：`s2` 堆里的实际对象就是 `Student`，所以调用的是 `Student` 自己的 `study()` 方法。
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



