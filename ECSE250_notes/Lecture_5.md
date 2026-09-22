```java
String S1 = "hello";
String S2 = "hello";
String S3 = new String("hello");

S1 == S2; //true
//JVM checks if `"hello"` is already in the heap memory
//If so, the JVM points `S2` to the already existing memory address.
//might not always work
//stirngs are objects(reference type), not primitive type
//for reference type, `==` compares memory address not, not content

//`S1` 和 `S2` 是两个独立存在的变量（各自占用 Stack 中的一小块地方），只是它们里面**存着数值相同的指针**（都指向 `0x01`）。
    
//即使你后来把 `S2` 改掉（比如 `S2 = "world";`），`S2` 只会去装一个新的地址，而 `S1` 依然指向 `0x01`，两者互不影响。

S1 == S3; //false
```
#### ==Note: One string address is 32 bits==


*What happens when i change the value of the string?*
```java
String s = "hey"
System.out.println(System.identityHashCode(s));
//输出对象的内存映射code

s = s + 'y'
System.out.println(System.identityHashCode(s));

```

Strings are immutable: once the memory is allocated, its contents can never be modified.
Modifying string variable meaning a new memory allocation.
==Strings are not arrays, since arrays are mutable==

| 'h'                               |
| --------------------------------- |
| 'e'                               |
| 'y'                               |
| *0x01 `s` no longer points to it* |
|                                   |
| 'h'                               |
| 'e'                               |
| 'y'                               |
| 'y'                               |
| *0x10*                            |
^java looks for block big enough to store this string
1. **The Internal Reference:** Even though your variable `s` stops pointing to `"hey"`, the **JVM's ==String Pool== keeps its own internal hidden reference** to `"hey"`.
    
2. **GC Rule:** Garbage Collection _only_ deletes objects that have **zero references**. Because the String Pool is still referencing `"hey"`, it is **not eligible for GC**.
    
3. **Lifespan:** `"hey"` will remain in memory for the entire life of your running Java program so that if another line of code later writes `String x = "hey";`, Java can reuse it instantly.
    

#### *When WOULD it go to GC?*
It would only become eligible for GC if it was **not a literal in the pool**. For example:
```java
// Dynamically created at runtime (NOT in the String Pool)
String s = new String(new char[]{'h', 'e', 'y'}); //Dynamic/runtime

s = s + 'y'; // 's' now points to "heyy"
```
- In Java, any object created with the `new` keyword bypasses the String Constant Pool and is stored as a standard object directly in general Heap memory.
- In this dynamic case, the original `"hey"` object in heap memory now has **zero references** pointing to it anywhere. It becomes eligible for Garbage Collection (though GC will clean it up whenever it runs next, rather than instantly).


### Arrays
- Holds a fixed number of values of **the same type**.
- Note: Array has a fixed size. If you need a bigger array, you must create a new one and copy contents.
```java
//Declaration
int[] numbers;
//^type/array/name
```

| null |
| ---- |
^numbers
- holds a reference to array in memory (==No memory allocated since you only declared a reference variable, not initiated an array object==)

```java
int[] numbers = {3, 4, 5, 8, 10};
numbers [1] = 5;

//OR

int[] myArray = new int[5]; 
//createobject/type/size
//if not directly putting value in the object needs to put new
```

| 3       |
| ------- |
| ~~4~~ 5 |
| 5       |
| 8       |
| 10      |
*0x01* numbers

```java 
int x; 
//No defualt value
//When declaring a primitive variable inside a method (local variables), Java allocates space for it on the Stack, but leaves it uninitialized.

int[] y = new int[5]; 
//Heap Objects Get Default Values: Using `new` allocates an array object in Heap memory. Java automatically initializes elements in heap-allocated arrays to default values (`0` for `int`, `false` for `boolean`, `null` for objects).

myArray[0] = 4; //Cannot do this without allocating array in memory

//You cannot assign values to array indices if the array variable hasn't been instantiated with `new`.
    
//If `myArray` was declared as `int[] myArray;` without `new`, it either contains nothing or is uninitialized. Attempting `myArray[0] = 4` fails because there is no underlying memory block to write to.
```

|     |
| --- |
|     |
|     |
|     |
|     |
*0xFF* myArray

e.g.
```java
String[] seasons;

Seasons = new String[4];
//default values of null in all 4 locations

String s;
//Note: For strings, if no value is assigned to the memory, the default value is null

Seasons[0] = "winter";

```

| *0x02* |
| ------ |
^seasons

| null |
| ---- |
^s

| *0x02* (array)            |
| ------------------------- |
| 0xFF (address of stiring) |
| Null                      |
| Null                      |
| Null                      |
| ...                       |
| ...                       |
| *0xFF* (string)           |
| 'w'                       |
| 'i'                       |
| 'n'                       |
| 't'                       |
| 'e'                       |
| 'r'                       |
#### Multi-dimensional arrays

```java
int[][] numbers = {{1}, {1,2}, {1,2,3}};

int[][] numbers = new int[3][2]; 
//size 3 for numbers and size 2 for the array inside numbers

int[][] numbers = new int[3][]; 
//size 3 numbers array containing null
```

