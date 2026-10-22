![[cb5d7131c3123e7610c05cfd4b16ebfb.jpg|317]]

```java
//in array list class
public Student remove(int i){
	if(i>=0 && i<size){
		Student temp = arr[i];
		ShiftUp(i) //starting from a specific index, will shift element up
		size--;
		return temp;
	}
	//else throw exception

}
```
![[afc53628fe90d2be61e0ba0be8a69fd5.jpg|381]]

Running time
```java
public boolean contains(int[] array, int target){
	int i = 0; 
	//runtime: C1
	while(i<array.length){
		if (array[i]==target){
			return true;
		}
	i++;
	}
	//runtime: C2 * N
	return false;
	//runtime: C3
}
```
How does the running time vary depending on the input size?
t(N)=C1+C2\*N+C3+**$N^2$(nested loops)** $\approx$ O(N) 
N is the dominant term
When we talk about the big O we talk about the critical path

Linked Lists链表
![[ae086b6dd57b2c8d546659f6461f53b3.jpg|420]]
ArrayList: consecutive memory space

Node: 
- reference to element of list
- next: reference to next node

```java
class SNode{
	Student element;
	SNode next;
}

SNode n = new SNode();
n.element = new Student();
```
![[d6bc7586ea5d405d64c4883774e3b00d.jpg|244]]

LinkedList --> sequence of nodes

```java
public class SinglyLinkedList(){
	private SNode head;
	private SNode tail;
	private size; //the # of actual object that currently existing in the link
	
	public SinglyLinkedList(){
	size=0;
	head=null;
	tail=null;
	}

	public void addFirst(Student e){
		SNode n = new SNode();
		n.element = e; // createing a node with a new element
		n.next=head;
		head = n;
		size++;
		if(size==1){
			tail = n;
		}
	}
	//running time: O(1)
}



```
