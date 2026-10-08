- Every class in Java is a subclass of `Object`
	- Passing `person1` directly to `System.out.println()` invokes its `toString()` method.
	- The base `java.lang.Object` class already comes with a default implementation of `toString()`
	- When you define your own `toString()` method inside `Person`, you are **overriding** the parent method inherited from `java.lang.Object`.

- **`finally` Block Order:** A `finally` block **always** executes right before a `try` or `catch` block returns control to the caller.

- No matter which declaration(super/sub), as long as the object points to sub class object, the function called gets overridden.

 - methods on arrays

| **Action Inside Method**  | **Example Code**            | **Modifies Original Array Outside?** |
| ------------------------- | --------------------------- | ------------------------------------ |
| **Reassigning Parameter** | `dogs = new Dog[10];`       | **No** (Only changes local variable) |
| **Mutating Array Index**  | `dogs[0] = new Dog("Rex");` | **Yes** (Modifies shared memory)     |
| **Mutating Object State** | `dogs[0].setName("Rex");`   | **Yes** (Modifies shared object)     |

- object.equals() method
	- **True:** The default `equals` method in `Object` uses reference equality (`==`). It works and performs equality checks for user-defined classes out-of-the-box, comparing whether two references point to the exact same object in memory.
    
	- **True:** This describes the **symmetric property** required by the Java specification (`equals` contract): if `a.equals(b)` is `true`, then `b.equals(a)` must also be `true`.
	    
	- **False:** `equals()` is a method on `Object` and **cannot** be called on primitives (`int`, `double`, etc.). Primitives are compared using `==`.
	    
	- **False:** The default `equals()` in `Object` does **not** perform a deep content comparison; it performs reference equality (`this == obj`).
	    
	- **True:** Overriding `equals()` allows you to define custom logical/value equality based on object fields (e.g., matching IDs or names) rather than memory locations.
	    
	- **False:** While you _can_ pass any object as an argument, proper `equals` implementations enforce type safety via `instanceof` or `getClass()`. Comparing objects of entirely unrelated classes generally returns `false` to uphold the symmetry contract.


- memory is allocated by *JVM* while the program runs.

### Println() method
#### 1. Declared only

| Variable kind                   | `int x;`                                                                                                    | `String s;` / `int[] a;` / `Student st;` |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| **Local variable**              | Compile error                                                                                               | Compile error                            |
| **Field of a class**            | Prints `0` (`double`: `0.0`, `boolean`: `false`, `char`: the NUL character, which shows as nothing visible) | Prints `null`                            |
| **Array element** (after `new`) | Prints `0` (same defaults as above)                                                                         | Prints `null`                            |

For a local variable, the "might not have been initialized" error stops the program from compiling, so nothing prints.

#### 2. Initialized

#### Primitive

|Code|`print` output|
|---|---|
|`int x = 5;`|`5`|
|`double d = 1;`|`1.0`|
|`boolean b = true;`|`true`|
|`char c = 'a';`|`a`|

#### Built-in reference types

| Code                                        | `print` output               | Why                                   |
| ------------------------------------------- | ---------------------------- | ------------------------------------- |
| `String s = "hello";`                       | `hello`                      | `String` overrides `toString()`       |
| `String s = null;`                          | `null`                       | `print` handles null specially        |
| `Integer n = 25;`                           | `25`                         | Wrapper classes override `toString()` |
| `int[] a = new int[3];`                     | `[I@1b6d3586` (address-like) | Arrays don't override `toString()`    |
| `a[0]` (elements of that array)             | `0`                          | Array elements get defaults           |
| `Arrays.toString(a)`                        | `[0, 0, 0]`                  | Prints the contents                   |
| `ArrayList<Integer> l = new ArrayList<>();` | `[]`                         | Collections override `toString()`     |

#### Your own class

Assume `Student` has fields `String name;` and `int id;`.

| Code                                                                         | `print` output                                           |
| ---------------------------------------------------------------------------- | -------------------------------------------------------- |
| `Student s;` (local, unassigned)                                             | Compile error                                            |
| `Student s = null;` then `print(s)`                                          | `null`                                                   |
| `Student s = null;` then `s.name`                                            | **`NullPointerException`** (crashes instead of printing) |
| `Student s = new Student();`, no `toString()` override                       | `Student@1b6d3586` (class name plus hash code)           |
| `s.name` / `s.id` after `new Student()`                                      | `null` / `0` (field defaults)                            |
| `new Student("KP", 123)`, then `s.name` / `s.id`                             | `KP` / `123`                                             |
| Same object, with `toString()` overridden to return `name + " (" + id + ")"` | `KP (123)`                                               |

#### Key points
1. **Local variables** must be assigned before they're read, or the code won't compile.
2. **Fields and array elements** get defaults: `0`, `0.0`, `false`, or `null`.
3. **Printing a null reference** shows `null`. **Accessing a member** of a null reference (`s.name`, `s.toString()`, `a.length`) throws `NullPointerException`.
4. **Printing a non-null reference** calls its `toString()`. If the class doesn't override it, you get `ClassName@hash`.


![[Screenshot 2026-09-30 at 13.41.28.png]]![[Screenshot 2026-09-30 at 13.41.45.png]]![[Screenshot 2026-09-30 at 13.43.12.png]]![[Screenshot 2026-09-30 at 13.49.05.png]]
循环推出前 i 再一次增值到3![[Screenshot 2026-09-30 at 14.11.25.png]]![[Screenshot 2026-09-30 at 14.16.19.png]]![[Screenshot 2026-09-30 at 14.19.48.png]]![[Screenshot 2026-09-30 at 14.23.13.png]]![[Screenshot 2026-09-30 at 14.24.47.png]]![[Screenshot 2026-09-30 at 14.28.08.png]]![[Screenshot 2026-09-30 at 14.33.56.png]]
![[Screenshot 2026-09-30 at 14.42.18.png]]