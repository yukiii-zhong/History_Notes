# 语法

## When you use a new object, you have to establish it beforehand  

```java
  public DList() {
    //  Your solution here.
      head = new DListNode(null,null,null);
      head.prev = head;
      head.next = head;
      size =0;
  }
```

## "for-each" loop

```java
String[] arrData = {"Alpha", "Beta", "Gamma", "Delta", "Sigma"};
for (String strTemp : arrData){
    System.out.println(strTemp);
}
```



##  `toString()`  — > test

You can write a `toString()` method to test the class functions

```java
  public String toString() {
    String result = "[  ";
    DListNode current = head.next;
    while (current != head) {
      result = result + current.item + "  ";
      current = current.next;
    }
    return result + "]";
  }

```



## `max = (a>b)? a:b`

Condition: (a>b)

if the condition works: (a>b) return a, else return b



## `try` `catch exception`

```java
class Example1 {
   public static void main(String args[]) {
      int num1, num2;
      try {
         /* We suspect that this block of statement can throw 
          * exception so we handled it by placing these statements
          * inside try and handled the exception in catch block
          */
         num1 = 0;
         num2 = 62 / num1;
         System.out.println(num2);
         System.out.println("Hey I'm at the end of try block");
      }
      catch (ArithmeticException e) { 
         /* This block will only execute if any Arithmetic exception 
          * occurs in try block
          */
         System.out.println("You should not divide a number by zero");
      }
      catch (Exception e) {
         /* This is a generic Exception handler which means it can handle
          * all the exceptions. This will execute if the exception is not
          * handled by previous catch blocks.
          */
         System.out.println("Exception occurred");
      }
      System.out.println("I'm out of try-catch block in Java.");
   }
}
```



# `public` `protected`,Package Protection

| Visible:          | in the same package | in a subclass | everywhere |
| ----------------- | ------------------- | ------------- | ---------- |
| "public"          | Y                   | Y             | Y          |
| "protected"       | Y                   | Y             |            |
| default (Package) | Y                   |               |            |
| "private"         |                     |               |            |

## `protected` keyword 

1. `protected` the level of protection between `private` and `public`
2. a `private` field is visible —> declaring class
3. a `protected` field is visible  —> declaring class+ same package + **subclasses**

```java
public class SList {
    protected SListNode head;
    protected int size;
}
```

## Package Protection

```java
package list;

class SListNode{
    Object item;
    SListNode next;
}
```

By default, SListNode class and the 2 variables is within the Prackage Protection.

# Inheritance

``` java
public class SList{
    protected SListNode head;
    protected int size;
}

public class TailList extends SList{
    private SListNode tail;
    
    public TailList(int x){
        super(x);
        tail = null;
    }
}

SList s = new TailList();
s.insertEnd(obj);       // Calls TailList.insertEnd()
s = new SList();
s.insertEnd(obj);		// Calls SList.insertEnd() 


//COMPILE-ERROR:
SList s = new TailList();
s.earTail();          
//not every SList object has eatTail() method, so Java can't use dynamic method to lookup on the variable s.

//You need to make a cast
s = t;
t = (TailList)s;
```



## `instanceof`

```java
if (s instanceof TailList){
    s = (TailList)s;
}
```



## abstract classes

The sole purpose of abstract classes is to be **extended**.

```java
public abstract class List(){
    protected int size;
    
    public int length(){
        return size;
    }
    
    //The abstract method can guarantee every non-abstract subclasses will implement this method
    public abstract void insertFront(Object item);
}

public class SList extends List{
    protected SListNode head;
    
    //You must define 'insertFront()'method in SList class
    //Because you cannot have abstract method in an non-abstract class
    public void insertFront(Object item){
        head = new SListNode(item,head);
        size++
    }
}

//Implement
List myList = new SList();
myList.insertFront(obj);
```



# Java Interface(接口)

1. Java interface is like abstract classes, except 2 differences:

   1. in Java, a class can `extends` (inherite) only **1 class**,

      but can  `implement` as many  **Java interface** as you like

   2. a **Java interface** cannot implement any methods

   3. a **Java interface** can only include `final` `static` constants.

      ->It only contains method prototype(原型) and constants

2. In common

   You have to implement the abstract function in an `abstract class`

   You have to implement every class in an `interface`

``` java
//引入包
import java.lang.*

//Establish the interface
public interface Animal{
	public void eat();
	public void travel();
}

//implement the interface
public class MammelInt implements Animal{
	
    public void eat(){
    	System.out.println("Mammal eats");
    }
    
    public void travel(){
    	System.out.println("Mammal travels");
    }
}
```

```java
//in Nukeable.java
public interface Nukeable{
    public void nuke();   
}

//in Java.lang
//It's already in the java library
public interface Comparable{
    public int compareTo(Object o);
}

//implement
public class SList extends List implements Nukeable, Comparable{
	
    public void nuke(){
        head = null;
        size =0;
    }
    
    //You promise you will have a compareTo method
    //The following is a convention
    public int compareTo(Object o){
        [Returns a number < 0 if this < o,
        					0 if this.equals(o),
        				  > 0 if this >o.]
    }
}

// Because an SList is a Nukeable and a Comparable, we can assign it to variables.
of these types.   Nukeable n = new SList();
Nukeable n = new SList();
Comparable c = (comparable) n;

//a subinterface can have multiple superinterfaces.
public interface NukeandCompare extends Nukeable,comparable{
    ...
}
```





# Java Packages

**Package:** collection of **classes, Java interfaces, sub package**, that trust each other

 **3 Benefits:**

- Packages can contain hidden classes not visible outside package
- Classes in packages can have fields and methods that are visible inside the package only
- Different packages can have classes with the same name. 

**Examples:**

- java.io
- HWK4 'list' package
- java.awt.image.Model   (sub packages)



### Using Packages

1. Fully-qualified name

   `java.lang.System.out.println('');`

   Instead:

   `import java.io.File;`

   `import java.io.*;`



2. Java Complier Class path

   `javac -cp ".:~jrs/classes:libraries.jar" *.java`



3. **Public class** must be declared in file named after class.

   **"package" classes** can appear in any .java file.

   ​

4. Compiling and running must be done from **outside package**.

   **Compile:** `javac -g list/SList.java`

   **Run:** `java list.SList`

   ​

# Iterators

In **Java.util** there is a standard Java interface

```java
public interface Iterator{
    boolean hasNext();
    Object next();
    void remove();     //optional.
}
```

```JAVA
public interface Iterable{
    Iterator iterator();
}
```

An Iterator is like a bookmark. —>can have many Iterators in same data structure.

Iterator 是 一种辅助角色。

## "for- each" loop for Iterate

```java
for (Object o: l){
    //"l" refers to SList implements Iterable
    System.out.println(o);
} 
```

Equvialent to:

```java
for (Iterator i = l.iterator();i.hasNext()){
    Object o = i.next();
    System.out.println(o);
}
```



## Example

因为：**You can use `SListIterator` `implements Iterator` to get the next item of the `SList`**

所以：**`SList` can implement `Iterable` , with `iterator()` function.**

换句话说：**To establish the `iterator()` function for `SList`, you write a `SLitstIterator` class to `implements iterator`.**

```java
package list;
import java.util.*;

public class SListIterator implements Iterator{
    SListNode n;
    
    // Para: SList
    //Establish a new SListIterator for 'the' SList
    public SListIterator(SList l){
        n = l.head;
    }
    
    //You can find next node to Iterate
    public boolean hasNext{
        return n !=null;
    }
    
    // return the object of this node, and make the Iterator come to the next node
    public Object next(){
        //Exception situation
        if(n ==null){
            throw new NoSuchElementException();  // In Java.util
        }
        
        //Get the item and come to the next node
        Object i = n.item;
        n = n.next;
        return i;
    }
    
    public void remove(){
        throw new UnsupportedOperationException("Nice try, bozo.");  //In Java.lang
    }
}
```

```java
package list;
import java.util.*;

public class SList implements Iterable{
    SListNode head;
    int size;
    
    // Make a iterator()
    public Iterator iterator(){
        return new SListIterator(this);
    }
    ...
}
```

# Jar 包导入IntelliJ

1. `Command +: ` Project Structure


2. Modules —>Dependencies—>"+"Jar 包


## Creating a JAR File (IntelliJ)

1.) Go to File → Project Structure → Artifacts → JAR → “From modules with dependencies”

2.) Click OK a couple of times

3.) Click Build → Build Artifacts (this will create a JAR file in a folder called “Artifacts”)

4.) Distribute this JAR file to other Java programmers, who can now import it into IntelliJ (or otherwise)

## Build Systems

Rather than importing a list of libraries or whatnot each time we wanted to create a project, we can simply put the files into the appropriate place, and use “Build Systems” to automate the process of setting up your project. The advantages of Build Systems are especially seen in bigger teams and projects, where it’s largely beneficial to automate the process of setting up the project structure. Though the advantages of Build Systems are rather minimal in 61B, we did use Maven in Project 3 (BearMaps, Spring 2017), which is one of many popular build systems (including Ant and Gradle).




# Encapsulation (封装)

**Module**: A set of methods that work together to perform some tasks.

A module is **encapsulated** if its implementation is hidden, and it can be accessed only through a documented interface

**ADT** (Abstract data type): Encapsulated data structure.

****

Not all modules are ADTs

Algorithms (list sorters) & applications (network routing software) can be encapsulated.





# Asymptotic Analysis

### Detailed 

https://joshhug.gitbooks.io/hug61b/content/chap8/chap83.html

### Simplification Summary

- Only consider the worst case.(Order of growth)
- Pick a representative operation (aka: cost model)
- Ignore lower order terms
- Ignore multiplicative constants.

### Simplified Analysis Process

Rather than building the entire table, we can instead:

- Choose our cost model (representative operation we want to count).
  - EX: the operation `==`
- Figure out the order of growth for the count of our representative operation by either:
  - Making an exact count, and discarding unnecessary pieces
  - Or, using intuition/inspection to determine orders of growth (comes with practice!)

We’ll now re-analyze `dup1` using this process.

![image-20180408105123704](/var/folders/xj/x7t_xj850yv1z8td6xr3g0sh0000gn/T/abnerworks.Typora/image-20180408105123704.png)

### Case

| function        | order of growth |
| --------------- | --------------- |
| $N^3 + 3N^4$    | $N^4$           |
| $1/N+N^3$       | $N^3$           |
| $1/N+5$         | 1               |
| $Ne^N+N$        | $Ne^N$          |
| $40sin(N)+4N^2$ | $N^2$           |

### Example Analysis

```java
public static void printParty(int N) {
   for (int i = 1; i <= N; i = i * 2) {
      for (int j = 0; j < i; j += 1) {
         System.out.println("hello");   
         int ZUG = 1 + 1;
      }
   }
}
```

The first loop advances by *multiplying* `i` by 2 each time. 

The inner loop runs from 0 to the current value of `i`. 

The two operations inside the loop are both **constant time**, 

so let's approach this by asking "**how many times does this print out "hello" for a given value of N**?"

![image-20180408114440769](/var/folders/xj/x7t_xj850yv1z8td6xr3g0sh0000gn/T/abnerworks.Typora/image-20180408114440769.png)

$C(N) = 1 + 2 + 4 + ... + N$ (if N is a power of 2)

Again, we can think of this in a couple ways. Since we're already on a graphical roll, let's start there. If we graph the trajectory of 0.5 N (lower dashed line), and 4N (upper dashed line), and C(N) itself (the red staircase line) we see that C(N) is fully bounded between those two dashed lines.

![graph](https://joshhug.gitbooks.io/hug61b/content/assets/loops2_graph.png)

Therefore, the runtime (by definition) must also be linear!

Let's look at this another way as well:

We can solve our equation from above with the power of mathematics, and find that: $C(N) = 1 + 2 + 4 + ... + N = 2N - 1$ (again if N is a power of 2). For example, If N = 8, 1 + 2 + 4 + 8 = 15 = 2*8 - 1

And by removing lesser terms and multiplicative constants, we know that 2N - 1 is in the linear family.

We can also see this on our graph by plotting 2N:

![graph](https://joshhug.gitbooks.io/hug61b/content/assets/loops2_graph2.png)

### Big Theta VS Big O VS Big Omega

Big Theta: It deepends on the case

​	EX: The worst case runtime is Θ(N^2).

Big O: Order of growth is <= Big O

​	EX: The runtime is O(N^2).

Big Omega: Order of growth is >= Big Omega

|                       | Informal Meaning                                 | Example Family | Example Family Members         |
| --------------------- | ------------------------------------------------ | -------------- | ------------------------------ |
| Big Theta **Θ(f(N))** | Order of growth is f(N)                          | $Θ(N^2)$       | $N^2/2, 2N^2, N^2 + 38N + 1/N$ |
| Big O **O(f(N))**     | Order of growth is less than or equal to f(N)    | $O(N^2)$       | $N^2/2, 2N^2, \log N$          |
| Big Omega **Ω(f(N))** | Order of growth is greater than or equal to f(N) | $Ω(N2)$        | $N^2/2, 2N^2, 5^N$             |

## Sort a List(Define your own way)

### Method1 `Collections.sort(List<T>, Comparator())`

前提：

```java
public class Interval{
    int start;
    int end;
}
```

#### Method 1.1 Establish a new private class `implements Comparator` —> Contains method `compare`

```java
private class IntervalComparator implements Comparator<Interval>{
    public int compare(Interval a, Interval b){
        return a.start<b.start ? -1: a.start==b.start ? 0:1;
    }
}

public List<Interval> merge (List<Interval> intervals){
    Collections.sort(intervals, new IntervalComparator());
}
```



#### Method 1.2 Directly establish it in the `collections`,and define if within the function

```java
public List<Interval> merge (List<Interval> intervals){
    Collections.sort(intervals, new Comparator<Interval>(){
        public int compare(Interval a, Interval b){
            return a.start-b.start;
        }
    })
}
```

