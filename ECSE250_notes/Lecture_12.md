### Array list  --> use array to implement a list
数组大小固定,但列表需要能随意增删元素,所以我们自己写一个类,把数组包起来,在里面处理好"空间不够"和"移动元素"这些麻烦事。
- add(e): add element at end of the list
- remove(i): remove + return i-th element
- add(i,e): add element at index i
- get(i): return i-th element
- set(e,i): replace i-th element with e
- isEmpty(): check/return boolean
- Clear(): empty list

e.g Student array
```java
Student[] students = new Student[5];
```
![[Screenshot 2026-10-16 at 20.55.30.png]]
数组里存的是引用，指向Student对象

ArrayList makes it easier to manipulate lists
```java
public class StudentList{
	private Student[] arr;
	private int size;
	
	public StudentList(){
		arr = new Student[10]; //十个空位里全是null
		size = 0; //实际存了0个元素
	}
}

StudentList list = new StudentList();
```
![[Screenshot 2026-10-16 at 20.59.03.png]]

```java
//get(i) --> return element at i-th position
public Student get(int i){ //Student is the return type
	if(i>=0 && i<size){ //where size<arr.length
		return this.arr[i];
	}else{
		throw new IndexOutOfBoundsException();
	}
}

public Student set(int i, Student e){
	//e.g. Student old = list.set(2, newStudent);
	//arr[i]=e; this would lose old object
		
	if(i>=0 && i<size){
		Student temp = arr[i]; //先把旧对象存起来
		arr[i]=e;              //放入新对象
		return temp;           //返回旧对象
	}else{
		throw //exception
	}
}

public void add(Student s){
	//first makesure there is room in array
	if(arr.length == size){
		resize(); //helper method double the length
	}
	arr[size]=s;
	size++;
}
```
![[Screenshot 2026-10-16 at 21.13.43.png|378]]
```java
public void resize{
	//create bigger array
	//copy each element from arr to bigger
	//this.arr=bigger
}
```
![[Screenshot 2026-10-16 at 21.19.43.png|390]]
```java
public void add(int i, Student s){
	if(i>=0 && i<size){
		if(arr.length==size){
			resize();
		}
		ShiftDown(i);
	}
}
```
![[Screenshot 2026-10-16 at 21.21.27.png|385]]
```java
private void ShiftDown(int i){
	for (int k=size; k>i; k--){
		this.arr[k]=this.arr[k-1];
	}
}
```
![[Screenshot 2026-10-16 at 21.32.30.png|393]] 