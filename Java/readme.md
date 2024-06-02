### Q.OOP in java
- In programming, an "Oops" typically refers to Object-Oriented Programming (OOP). OOP is a programming paradigm based on the concept of "objects," which are instances of classes. These objects can contain data in the form of fields (often known as attributes or properties) and code in the form of procedures (often known as methods).
- Key concepts in OOP include:
1. Class: A blueprint for creating objects. It defines a set of attributes and methods that the created objects will have.
2. Object: An instance of a class. It is created from a class and represents an entity with attributes and behaviors defined by the class.
3. Encapsulation: The bundling of data (attributes) and methods (functions or procedures) that operate on the data into a single unit, or class. It also involves restricting direct access to some of the object's components, which is a means of preventing accidental interference and misuse.
4. Inheritance: The mechanism by which one class can inherit attributes and methods from another class. This allows for code reusability and the creation of a hierarchical relationship between classes.
5. Polymorphism: The ability of different objects to respond to the same method call in different ways. This is typically achieved through method overriding (a subclass provides a specific implementation of a method that is already defined in its superclass) and method overloading (multiple methods have the same name but different parameters).
6. Abstraction: The process of hiding the complex implementation details and showing only the essential features of the object. This helps in reducing programming complexity and effort.
- These concepts form the foundation of many modern programming languages, including Java, C++, Python, and others. OOP aims to provide a clear modular structure for programs, making it easier to manage large software systems by promoting code reuse and improving maintainability.

### Q.String literal pool
- The String Literal Pool in Java is a special memory area in the Java heap that stores string literals. When you create a string literal, Java checks the pool to see if an identical string already exists. If it does, Java reuses the existing string. If it doesn't, Java creates a new string in the pool. This approach helps save memory by avoiding the creation of duplicate strings. Here's an example to illustrate:

```
String str1 = "Hello";
String str2 = "Hello";

// Both str1 and str2 point to the same string in the literal pool
System.out.println(str1 == str2); // Output: true
```
- In this example, both `str1` and `str2` refer to the same string object in the string literal pool, demonstrating how the pool helps in memory optimization.

### Q.ArrayList vs LinkedList
1. *Performance in Accessing Elements*:
   - *ArrayList*: Provides fast random access to elements (O(1) time complexity) because it is backed by an array.
   - *LinkedList*: Slower random access (O(n) time complexity) since it requires traversal from the beginning or end of the list to reach a specific element.

2. *Performance in Modifying Elementns*:
   - *ArrayList*: Adding or removig elements, especially in the middle of the list, can be slow (O(n) time complexity) due to the need to shift elements.
   - *LinkedList*: Adding or removing elements is faster (O(1) time complexity) when done at the beginning or end of the list. For modifications in the middle, it still requires traversal (O(n) time complexity).

3. *Memory Overhead*:
   - *ArrayList*: Uses less memory as it stores data in a contiguous array.
   - *LinkedList*: Uses more memory due to the storage of node pointers (next and previous references) in addition to the data.

**When to Use What**
- *Use ArrayList when*:
  - You need fast random access to elements.
  - You have a stable list size or modifications are infrequent.
  - Memory overhead is a concern and you prefer lower memory usage.

- *Use LinkedList when*:
  - You need to frequently add or remove elements from the beginning or end of the list.
  - The cost of traversal for random access is not a concern.
  - You prefer efficient memory management when dealing with a large number of insertions and deletions.

### Q.Singleton Design pattern.Is it thread safe?If not,how to make it thread safe?
- The Singleton pattern ensures that a class has only one instance and provides a global point of access to that instance. Here's a basic implementation of the Singleton pattern in ```
```
public class Singleton {
    // Private static instance variable
    private static Singleton instance;

    // Private constructor to prevent instantiation from outside
    private Singleton() {
    }

    // Public static method to get the instance
    public static Singleton getInstance() {
        // Lazy initialization: create instance if not already exists
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```
- Explanation:
1. Private Constructor: The constructor of the Singleton class is made private to prevent instantiation from outside the class.
2. Static Instance Variable: A private static variable instance holds the single instance of the class.
3. getInstance() Method: The public static method getInstance() provides a global point of access to the instance. It ensures that only one instance of the class is created and returned.
4. Lazy Initialization: The above implementation uses lazy initialization, meaning the instance is created only when getInstance() is called for the first time. This approach is thread-safe for most scenarios but may lead to race conditions in a multithreaded environment.

- **Thread-Safe Singleton**:
-  To make the Singleton pattern thread-safe, you can use double-checked locking or initialize the instance statically. Here's an example using double-checked locking:
```
public class ThreadSafeSingleton {
    private static volatile ThreadSafeSingleton instance;

    private ThreadSafeSingleton() {
    }

    public static ThreadSafeSingleton getInstance() {
        if (instance == null) {
            synchronized (ThreadSafeSingleton.class) {
                if (instance == null) {
                    instance = new ThreadSafeSingleton();
                }
            }
        }
        return instance;
    }
}
```
-In this version, the getInstance() method uses double-checked locking to ensure thread safety while minimizing synchronization overhead.
- Singleton pattern is widely used in scenarios where you want to ensure that there is only one instance of a class throughout the application, such as logger, database connection, configuration settings, etc.

### Q.I am calling singleton getinstance method using serialisation and writing in some file , that is doing serialisation. That is storing the state. Now Using the same file which I stored I am doing deserialization , so now will I get 2 objects,right? (Extended question on previous question,may not be asked)
- In the case of serialization and deserialization with a singleton class, if the class is implemented correctly, you should not get multiple instances of the singleton. Here's why:
- Singleton Instance: The whole point of the singleton pattern is to ensure that only one instance of the class exists throughout the JVM.
- Serialization and Deserialization: When you serialize a singleton object and then deserialize it back, the deserialized object will not have gone through the constructor. Instead, it will be created using the existing instance that was already in memory.

### Q.Some git commands
- Initialize a new Git repository: git init
- Clone an existing repository: git clone https://github.com/user/repository.git
- Check the status of the repository: git status
- Add files to the staging area: git add filename.txt
- To add all files: git add .
- Commit changes: git commit -m "Commit message"
- View the commit history: git log
- Create a new branch: git branch new-branch
- Switch to a different branch: git checkout new-branch
- Create and switch to a new branch: git checkout -b new-branch
- Merge a branch into the current branch: git merge new-branch
- Delete a branch: git branch -d new-branch
- List remote repositories: git remote -v
- Fetch changes from the remote repository: git fetch origin
- Push changes to the remote repository: git push origin main
- Pull changes from the remote repository: git pull origin main
- Show changes between the working directory and the index: git diff
- Show changes between the index and the last commit: git diff --cached
- Show changes between two commits: git diff commit1 commit2

### Suppose 2 developers are working on core related functionality, one of the developer pushed his changes on common branch and other developer is still working on changes , but when other developer push the changes on master he will get conflicts, so what is good approach for other developer to avoid conflicts
- To avoid conflicts when multiple developers are working on core-related functionality and pushing to a common branch, a good approach involves the following steps:
- Best Practices for Avoiding Conflicts
1. Frequent Pulls and Rebases: The second developer should frequently pull the latest changes from the common branch (e.g., master) and rebase their work onto the latest state. This way, they can resolve any conflicts locally before pushing their changes.
2. Feature Branches: Developers should work on separate feature branches and only merge into the common branch after their work is completed and conflicts are resolved.

### Q.If I use this code in production will this code compile and run properly. If not then what challenges will it face and how to resolve them.
```
abstract class Employee {
    public EmployeeDetails getDetails(int id) throws SQLException {
        // Connects to DB and fetches the details
    }
}

class EmployeeDal extends Employee {
    @Override
    public EmployeeDetails getDetails(int id) throws SQLException, IOException {
        // Fetches DB details from a file
        // Connects to DB and fetches the details
    }
}
```
**Compilation and Runtime Issues**
- Method Signature Mismatch:
The method getDetails(int id) in the Employee class is overridden in the EmployeeDal class. However, the overridden method in EmployeeDal adds an additional exception (IOException) to its throws clause. This is not allowed because the overridden method cannot throw new or broader checked exceptions than the method it overrides.

### If both methods are private then can we override it , in the above code And what about protected method 
- In Java, method overriding has specific rules regarding access modifiers:
- Private Methods: Private methods are not visible to subclasses. Therefore, they cannot be overridden. Each class has its own private copy of the method, and there is no relationship between the private methods in the superclass and the subclass. If both methods are private in the superclass and subclass, they are considered separate methods, not an override.
- Protected Methods: Protected methods can be overridden by subclasses. The protected access modifier allows the method to be visible in the same package and in subclasses, even if they are in different packages. When a subclass overrides a protected method, it can use the same access level or a more permissive access level (i.e., protected or public).

### Method Overloading vs Overriding
- Method overloading and method overriding are both concepts used to achieve polymorphism in Java, but they have distinct differences. Here's a detailed comparison:
1. Method Overloading (Compile Time Polymorphism)
- Method overloading is the ability to create multiple methods in the same class with the same name but with different parameters (different type, number, or both).
- Overloaded methods must have different parameter lists (type, number, or both).
- The return type can be different in overloaded methods but does not contribute to the method signature (i.e. does not affect method overloading)
- Access modifiers can be different, but it does not affect the method overloading.
- Static methods can be overloaded.
```
public class MathUtils {
    public int add(int a, int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }
}
public class TestOverloading {
    public static void main(String[] args) {
        MathUtils math = new MathUtils();
        System.out.println(math.add(5, 3));       // Calls add(int, int)
        System.out.println(math.add(5.0, 3.0));   // Calls add(double, double)
        System.out.println(math.add(5, 3, 2));    // Calls add(int, int, int)
    }
}
```
2. Method Overriding (Runtime polymorphism)
- Method overriding occurs when a subclass provides a specific implementation of a method that is already defined in its superclass.
- The method in the subclass must have the same parameter list as the method in the superclass.
- The return type must be the same or a subclass (covariant return type) of the return type declared in the original method in the superclass.
- The access level cannot be more restrictive than the overridden method's access level in the superclass.
- *Static methods cannot be overridden*. If you define a static method with the same signature in a subclass, it will hide the superclass static method.
- The @Override annotation is often used to indicate that a method is overriding a method in its superclass. This is optional but recommended as it helps catch errors.
```
class Animal {
    public void makeSound() {
        System.out.println("Some generic animal sound");
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Bark");
    }
}

public class TestOverriding {
    public static void main(String[] args) {
        Animal myAnimal = new Dog();
        myAnimal.makeSound(); // Outputs "Bark"
    }
}
```

### Q.String class in Java are immutable, why they are made immutable 
- In Java, the String class is immutable for several reasons, each contributing to the robustness and performance of Java applications:
1. String Pool: Java uses a string pool to manage memory more efficiently. If strings were mutable, changing the value of one string could inadvertently affect other strings that reference the same value in the pool.
2. Security: Many critical parameters, like database connection URLs, user credentials, and file paths, are passed as strings. If strings were mutable, these values could be changed unintentionally or maliciously, leading to security vulnerabilities.
3. Caching Hashcode: Immutable strings can cache their hashcode. Since the hashcode of an immutable string never changes, it can be computed once and reused, improving performance in scenarios like using strings as keys in hash-based collections.
4. Thread Safety (Concurrency): Immutable objects are inherently thread-safe, as their state cannot change after they are created. This eliminates the need for synchronization when strings are shared between multiple threads, simplifying concurrent programming. (*Strings are thread safe*)

### Q.Apart from string which class is immutable 
1. Wrapper Classes: All the primitive wrapper classes in Java are immutable. Integer, Long, Float etc.
2.  LocalDate: Represents an immutable date without time and time zone.
3. LocalTime: Represents an immutable time-of-day without date and time zone.

### Q.You are working on project where there is requirements to have all methods of string class ,There are some custom requirements where we need to modify String class . We need to extend string class , is it possible to write a class to extend String class
- In Java, you cannot extend the String class because it is declared as final. The final keyword in the class declaration prevents any other class from inheriting from it. This design choice ensures that the String class remains immutable and secure.
- *Alternatives to Extending the String Class*
1. *Composition*: Create a custom class that wraps a String object and provides additional methods.
2. *Utility Class*: Create a utility class with static methods that operate on String objects.
3. *Use of Decorator Pattern*: Implement the decorator pattern to extend the functionality of the String class. (don't mention if not knowing about design patterns)

1. Using Composition
```
public final class CustomString {
    private final String str;

    public CustomString(String str) {
        this.str = str;
    }

    // Delegate methods to the internal string
    public int length() {
        return str.length();
    }

    public char charAt(int index) {
        return str.charAt(index);
    }

    public CustomString concat(String str) {
        return new CustomString(this.str.concat(str));
    }

    public boolean equals(Object obj) {
        return str.equals(obj);
    }

    public int hashCode() {
        return str.hashCode();
    }

    public String toString() {
        return str;
    }

    // Custom method
    public CustomString customMethod() {
        // Your custom implementation
        return this;
    }

    // Add more methods as required
}
```

2. Utility Class
```
public final class StringUtils {

    private StringUtils() {
        // Prevent instantiation
    }

    public static String customMethod(String str) {
        // Your custom implementation
        return str;
    }

    // Add more static methods as required
}
```

3. Using Decorator Pattern
```
public interface CustomStringInterface {
    int length();
    char charAt(int index);
    CustomStringInterface concat(String str);
    boolean equals(Object obj);
    int hashCode();
    String toString();
    // Add custom methods
    CustomStringInterface customMethod();
}

public final class CustomStringDecorator implements CustomStringInterface {
    private final String str;

    public CustomStringDecorator(String str) {
        this.str = str;
    }

    public int length() {
        return str.length();
    }

    public char charAt(int index) {
        return str.charAt(index);
    }

    public CustomStringInterface concat(String str) {
        return new CustomStringDecorator(this.str.concat(str));
    }

    public boolean equals(Object obj) {
        return str.equals(obj);
    }

    public int hashCode() {
        return str.hashCode();
    }

    public String toString() {
        return str;
    }

    public CustomStringInterface customMethod() {
        // Your custom implementation
        return this;
    }
}
```

### Q.Collections in Java (it's main interfaces anc classes)
1. List Interface: Represents an ordered collection (sequence) that allows duplicate elements.
- ArrayList: Resizable-array implementation of the List interface.
- LinkedList: Doubly-linked list implementation of the List and Deque interfaces.
- Vector: Synchronized resizable-array implementation of the List interface.
- Stack: Subclass of Vector that implements a last-in-first-out stack.

2. Set Interface: Represents a collection that does not allow duplicate elements.
- HashSet: Hash table-backed implementation of the Set interface.
- LinkedHashSet: Hash table and linked list implementation of the Set interface, with predictable iteration order.
- TreeSet: Red-black tree implementation of the NavigableSet interface.
- EnumSet: Specialized Set implementation for use with enum types.

3. Queue Interface: Represents a collection designed for holding elements prior to processing.
- PriorityQueue: Unbounded priority queue based on a priority heap.
- LinkedList: Can also be used as a Queue implementation.
- ArrayDeque: Resizable-array implementation of the Deque interface.
- LinkedBlockingQueue: Linked node-based implementation of the BlockingQueue interface.

4. Map Interface: Represents a collection that maps keys to values, without duplicate keys. Does not extend Collection,rest mentioned above does.
- HashMap: Hash table-based implementation of the Map interface.
- LinkedHashMap: Hash table and linked list implementation of the Map interface, with predictable iteration order.
- TreeMap: Red-black tree implementation of the NavigableMap interface.
- ConcurrentHashMap: Concurrent implementation of the Map interface.
- WeakHashMap: Implementation of the Map interface with weak keys, allowing for automatic garbage collection of keys.

### Q.Explain Map in Java
- In Java, the Map interface represents a mapping between a key and a value. It is part of the Java Collections Framework and provides a way to store and manipulate key-value pairs. Unlike collections such as List or Set, Map does not inherit from the Collection interface.
- Key Features of Map
1. Key-Value Pairs: A Map stores data in key-value pairs.
2. No Duplicate Keys: Each key in a Map must be unique.
3. Value Access: Values can be accessed, inserted, or removed using their corresponding keys.
4. Null Keys and Values: Some implementations of Map allow null keys and values (e.g., HashMap).

- Common Implementations
1. HashMap: Provides constant-time performance for basic operations (get and put). Allows null keys and values. Does not guarantee any order of the keys.
2. LinkedHashMap: Extends HashMap to maintain a doubly-linked list of the entries. Preserves the insertion order or the order in which keys were last accessed.
3. TreeMap: Implements the NavigableMap interface. Keys are sorted based on their natural ordering or by a specified comparator. Guarantees log(n) time cost for basic operations.
4. ConcurrentHashMap: Part of the java.util.concurrent package. Designed for concurrent access, allowing concurrent reads and writes without locking the entire map.

### Q.What is time complexity of Hashmap 
- The time complexity of operations in a HashMap largely depends on how well the hash function distributes the keys and how collisions are handled. 
- Average case:
1. Insertion (put): O(1)
2. Lookup (get): O(1)
3. Deletion (remove): O(1)
4. Contains Key (containsKey): O(1)

- Worst-Case Time Complexities
1. Insertion (put): O(n) (In the worst case, if many keys hash to the same bucket (causing a collision), a linked list (or a balanced tree, in the case of Java 8+ with many collisions) may be used. In the case of a linked list, insertion in the worst case is O(n) because it may require traversing the list.)
2. Lookup (get): O(n)
3. Deletion (remove): O(n)
4. Contains Key (containsKey): O(n)

- Factors Affecting Time Complexity (not asked usually)
1. Hash Function Quality: A good hash function distributes keys evenly across the hash table, minimizing collisions and maintaining constant time complexity for operations.
2. Load Factor: The load factor is the measure of how full the hash table is allowed to get before its capacity is automatically increased. A lower load factor reduces collisions but uses more memory.
3. Collision Resolution Strategy: HashMap uses separate chaining (linked lists or trees) to resolve collisions. The efficiency of this strategy affects the overall time complexity, especially when many collisions occur.
4. Initial Capacity: The initial capacity of the hash table affects the need for resizing. A higher initial capacity reduces the frequency of resizing operations, which can be costly.

### Q.Any connection between immutable class and Map/Why keys in Map are immutable?
- Yes, there is a connection between immutable classes and the use of Map. (Immutable Keys) - Using immutable objects as keys in a Map is a best practice. 
1. Consistency: The immutability of keys ensures that their hash codes and equality checks remain consistent throughout their lifetime. If a key's state were to change while it is in the Map, it could lead to incorrect behavior, such as the keys can get lost..
2. Thread Safety: Immutable keys are inherently thread-safe. If multiple threads access the Map concurrently, there is no risk of the keys being modified by one thread while another thread is accessing or modifying the Map.

### Q.Let's say there is a class that is not immutable, can we use it as key of map?
- It can be used but it is generally not recommended because it can lead to unpredictable behavior. Here are some reasons why using mutable objects as keys in a Map is problematic, along with potential workarounds if you must use mutable objects.
1. Problems with Using Mutable Keys
- Inconsistent Behavior: If a key's state changes after it has been added to the Map, its hash code and equality comparison might also change. This can cause the key to become "lost" in the Map because it will no longer be found in the bucket corresponding to its original hash code.
- Difficulty in Retrieving Values: If the key has changed, you might not be able to retrieve the associated value using the mutated key or even the original key.

### Q. Let's say I have created a custom class , mutuble class which always returns 1 , can we use this class as key in Map. If we do so what are disadvantages 
- If you create a custom mutable class where the hashCode() method always returns 1, it can technically be used as a key in a Map, but it comes with significant disadvantages. 
Disadvantages of Using Such a Class as a Key in a Map
1. Hash Collisions: Since the hashCode() method always returns 1, all keys will hash to the same bucket in the HashMap. This leads to a high number of hash collisions.
2. Linked List in Buckets: In the case of a large number of keys, the single bucket will degenerate into a linked list (or a balanced tree in Java 8+ if the number of elements in the bucket exceeds a threshold). This makes the time complexity for basic operations (get, put, remove) degrade from O(1) to O(n).
3. Slow Operations: With many keys in a single bucket, the performance of get, put, and remove operations will be similar to that of a linked list, resulting in O(n) time complexity for these operations.

### Q.(follow up question) And will the time complexity get affected and what will be new time complexity?
- Insertion (put): O(n) with a linked list. O(log n) with a balanced tree (Java 8+ with many collisions)
- Lookup (get): O(n) with a linked list. O(log n) with a balanced tree (Java 8+ with many collisions)
- Deletion (remove): O(n) with a linked list. O(log n) with a balanced tree (Java 8+ with many collisions)

### Q.Is hashmap thread safe?
- No, HashMap is not thread-safe. If multiple threads access a HashMap concurrently and at least one of the threads modifies the map structurally (e.g., adding or removing elements), it must be synchronized externally to avoid data corruption and unpredictable behavior. Structural modifications are those that affect the size of the map or modify the internal structure of the map in a way that can cause a concurrent access issue.

### Q.Volatile keyword in Java
- The volatile keyword in Java is used to mark a variable as being stored in main memory. More precisely, every read of a volatile variable will be read from the computer's main memory, and not from the CPU cache, and every write to a volatile variable will be written to main memory, and not just to the CPU cache. Volatile only ensures readability i.e visibility and not thread safety that means multiple threads can work on it simultaneously,it has to be synchronized externally for thread safety.

### Q.Can volatile keyword used with primitive datatype
- Yes, the volatile keyword can be used with primitive data types in Java. This ensures that any read or write to a volatile variable is done directly to and from the main memory, thus making changes visible to all threads.
- Visibility but Not Atomicity: Declaring a variable as volatile ensures that its value is always read from and written to main memory, making changes visible to all threads. However, operations like incrementing a counter (counter++) are not atomic, even if the variable is declared volatile. These operations involve multiple steps (read, modify, write), and volatile does not ensure atomicity.

### Q.Can we use volatile with object reference or for object reference 
- Yes, you can use the volatile keyword with object references in Java. This ensures that the reference to the object is always read from and written to main memory, making any changes to the reference visible to all threads. However, it is important to note that volatile does not make the object itself thread-safe; it only ensures the visibility of the reference to the object.

### Q.which maps are thread safe in java collections?
1. *Collections.synchronizedMap*
2. *ConcurrentHashMap*
- Choosing the Right Thread-Safe Map
1. Performance: If you need high performance in a concurrent environment, ConcurrentHashMap is typically the best choice. It allows concurrent reads and fine-grained locking for write operations.
2. Legacy Code: If you’re working with legacy code that already uses Hashtable or if simplicity is a priority over performance, Hashtable or Collections.synchronizedMap might be sufficient.
3. Simplicity vs. Concurrency: If you need a simple thread-safe map and don’t expect high contention, Collections.synchronizedMap can be used. However, for better scalability and performance, especially in a highly concurrent environment, prefer ConcurrentHashMap.

### what is wait(),notify() and notifyAll() method?
1. wait(): Causes the current thread to wait until another thread invokes the notify() method or the notifyAll() method for this object.
2. notify(): Wakes up a single thread that is waiting on this object's monitor.
3. notifyAll(): Wakes up all threads that are waiting on this object's monitor.
- Here's a brief overview of how they are typically used:
1. wait() is called within a synchronized block to release the lock and wait until another thread notifies it.
2. notify() is called to notify a single waiting thread that it can proceed. It's important to note that which thread gets notified is not deterministic.
3. notifyAll() is called to notify all waiting threads that they can proceed. This method is often used to avoid the risk of leaving threads waiting indefinitely, which can occur with notify() if the wrong thread gets notified.
- These methods are commonly used in concurrent programming to implement producer-consumer scenarios, where one thread produces data and another consumes it. They are also used in other scenarios where synchronization between threads is necessary. It's important to use them carefully to avoid issues like deadlock or livelock.


### Q.ConcurrentHashmap and synchronisedHashmap difference (multithreadibg questions from this are asked only in companies that requires very strong multithreading knowledge)
1. Concurrency Strategy:
- ConcurrentHashMap: Uses a partitioned locking mechanism, where the map is divided into segments, and each segment has its own lock. Multiple threads can modify the map concurrently as long as they are operating on different segments.
- Collections.synchronizedMap(HashMap): Utilizes a single lock to synchronize access to the entire map. Only one thread can modify the map at a time, while other threads must wait for the lock to be released.

2. Performance:
- ConcurrentHashMap: Generally offers better performance under high concurrency due to its finer-grained locking strategy and reduced contention.
- Collections.synchronizedMap(HashMap): Tends to exhibit poorer performance under heavy concurrent access, as all operations are synchronized on a single mutex, leading to more contention and potential thread contention.

3.Iterators:
- ConcurrentHashMap: Supports weakly consistent iterators, meaning they reflect the state of the map at the time of creation and may or may not show the effects of subsequent modifications.
- Collections.synchronizedMap(HashMap): Provides fail-fast iterators, which throw ConcurrentModificationException if the map is structurally modified while an iterator is in use.

### Let's say a application is using synchroniseMap , can we replace this with concurrentHashmap, will any issue happens or we can directly replace it?And is vice versa possible?
- While replacing Collections.synchronizedMap with ConcurrentHashMap, take care of below points :
- Iteration Handling: Ensure that any manual synchronization used with synchronizedMap during iteration is removed when switching to ConcurrentHashMap.
- Null Key and Value Handling: Check and refactor any code that relies on inserting null keys or values, as ConcurrentHashMap does not allow them.
- Atomic Operations: Leverage the atomic operations(putIfAbsent, remove, and replace) provided by ConcurrentHashMap to simplify and optimize your code.

- While replacing ConcurrentHashMap with Collections.synchronizedMap, take care of below points :
- Iteration Handling: Add manual synchronization for iteration to prevent ConcurrentModificationException (as synchronizedMap will throw this execption which was not in ConcurrentHashMap).
- Null Key and Value Handling: Ensure that null keys and values are properly handled or prevented.
- Performance and Concurrency: Be aware of potential performance degradation due to increased contention and lower concurrency.
- Atomic Operations: Add necessary synchronization logic to ensure atomicity of operations as ConcurrenthashMaps atomic method will be absent in synchronizedMap.

### Q.how does synchronized and concurrentHashMap ensures thread safety?or hwo do they achieve concurrency?
- Collections.synchronizedMap ensures thread safety by synchronizing all method calls using the intrinsic lock of the synchronized map object, resulting in coarse-grained locking. In contrast, ConcurrentHashMap uses finer-grained locking and non-blocking algorithms, providing much better scalability and performance under high concurrency.

1. Collections.synchronizedMap
- The Collections.synchronizedMap method returns a synchronized (thread-safe) map backed by the specified map. This synchronization is achieved by wrapping the map and synchronizing access to it using the intrinsic lock (monitor) of the synchronized map object.
- How It Works:
1. Synchronization on Each Method Call: Every method that accesses or modifies the map is synchronized, ensuring that only one thread can execute a method at a time. This is done by using the synchronized keyword on the methods.
2. Intrinsic Lock: The lock used for synchronization is the intrinsic lock (monitor) of the synchronizedMap object.

2. ConcurrentHashMap
- ConcurrentHashMap is part of the java.util.concurrent package and provides a more sophisticated and efficient way to handle concurrency.
- How It Works:
1. Segmented Locking (Prior to Java 8): In earlier versions (Java 7 and before), ConcurrentHashMap used a segmented locking mechanism. The map was divided into segments, each with its own lock. This allowed multiple threads to access different segments concurrently without contention.
2. Lock Striping (Java 8 and later): In Java 8, the internal structure of ConcurrentHashMap was redesigned to use a finer-grained locking mechanism called lock striping, and it also introduced non-blocking algorithms (using CAS operations) for some operations.
- Fine-Grained Synchronization:
1. Bucket-Level Locking: Instead of locking the entire map, it locks only a part of the map. This significantly reduces contention and improves throughput.
2. Non-Blocking Reads: Read operations do not block, thanks to the use of volatile variables and atomic operations.

### Q.why wait(),notify() and notifyAll() is in Object class and not in Thread class?
- In the Java language, you wait() on a particular instance of an Object – a monitor assigned to that object to be precise. If you want to send a signal to one thread that is waiting on that specific object instance then you call notify() on that object. If you want to send a signal to all threads that are waiting on that object instance, you use notifyAll() on that object.
- If wait() and notify() were on the Thread instead then each thread would have to know the status of every other thread. How would thread1 know that thread2 was waiting for access to a particular resource? If thread1 needed to call thread2.notify() it would have to somehow find out that thread2 was waiting. There would need to be some mechanism for threads to register the resources or actions that they need so others could signal them when stuff was ready or available.
- In Java, the object itself is the entity that is shared between threads which allows them to communicate with each other. The threads have no specific knowledge of each other and they can run asynchronously. They run and they lock, wait, and notify on the object that they want to get access to. They have no knowledge of other threads and don't need to know their status. They don't need to know that it is thread2 which is waiting for the resource – they just notify on the resource and whomever it is that is waiting (if anyone) will be notified.
- In Java, we then use objects as synchronization, mutex, and communication points between threads. We synchronize on an object to get mutex access to an important code block and to synchronize memory. We wait on an object if we are waiting for some condition to change – some resource to become available. We notify on an object if we want to awaken sleeping threads.

### Q.Producer Consumer Multithreading problem (Solution must handle multiple producer and multiple consumer)
- The Producer-Consumer problem is a classic synchronization problem in which a fixed-size buffer is shared between multiple producer threads and multiple consumer threads. Producers produce items and place them into the buffer, while consumers take items from the buffer. The buffer must be protected from concurrent access to ensure data consistency and to avoid race conditions.
- Here is a working solution using Java's BlockingQueue to handle multiple producers and multiple consumers. *BlockingQueue provides thread-safe operations and handles synchronization internally*.
```
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;

class Producer implements Runnable {
    private BlockingQueue<Integer> queue;
    private int id;

    public Producer(BlockingQueue<Integer> queue, int id) {
        this.queue = queue;
        this.id = id;
    }

    @Override
    public void run() {
        try {
            int item;
            while (true) {
                item = produce(); //Calls the produce method to generate an item.
                queue.put(item); //Puts the produced item into the queue. If the queue is full, this method blocks until space becomes available.
                System.out.println("Producer " + id + " produced: " + item);
            }
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }

    private int produce() {
        // Simulate item production
        return (int) (Math.random() * 100);
    }
}

class Consumer implements Runnable {
    private BlockingQueue<Integer> queue;
    private int id;

    public Consumer(BlockingQueue<Integer> queue, int id) {
        this.queue = queue;
        this.id = id;
    }

    @Override
    public void run() {
        try {
            while (true) {
                int item = queue.take();//Takes an item from the queue. If the queue is empty, this method blocks until an item becomes available.
                consume(item);//Calls the consume method to process the consumed item.
                System.out.println("Consumer " + id + " consumed: " + item);
            }
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }

    private void consume(int item) {
        // Simulate item consumption
    }
}

public class ProducerConsumerExample {
    public static void main(String[] args) {
        final int BUFFER_SIZE = 10;
        final int NUM_PRODUCERS = 4;
        final int NUM_CONSUMERS = 4;

        BlockingQueue<Integer> queue = new ArrayBlockingQueue<>(BUFFER_SIZE);

        // Start producer threads
        for (int i = 1; i <= NUM_PRODUCERS; i++) {
            new Thread(new Producer(queue, i)).start();
        }

        // Start consumer threads
        for (int i = 1; i <= NUM_CONSUMERS; i++) {
            new Thread(new Consumer(queue, i)).start();
        }
    }
}
```
- Explanation
1. BlockingQueue:
- The BlockingQueue interface is part of the java.util.concurrent package and is designed to handle producer-consumer scenarios.
- ArrayBlockingQueue is used as the buffer, which has a fixed capacity (BUFFER_SIZE). It provides thread-safe put and take methods.
2. Producer Class:
- Implements the Runnable interface.
- In the run method, it continuously produces items and puts them into the queue using queue.put(item). The put method blocks if the queue is full, ensuring that producers wait until space is available.
3. Consumer Class:
- Implements the Runnable interface.
- In the run method, it continuously takes items from the queue using queue.take(). The take method blocks if the queue is empty, ensuring that consumers wait until items are available.
4. Main Method:
- Creates an ArrayBlockingQueue with a specified buffer size.
- Starts multiple producer and consumer threads.

- Key Points
- BlockingQueue: Manages synchronization internally, making the code simpler and easier to understand.
- Multiple Producers and Consumers: The solution handles multiple producers and consumers without additional synchronization mechanisms.
- Blocking Methods: put and take methods in BlockingQueue handle blocking when the queue is full or empty, respectively.
- This approach ensures that producers and consumers can operate concurrently without the risk of race conditions, while also efficiently managing the buffer size.

- Internal Mechanism
- The ArrayBlockingQueue (and other implementations of BlockingQueue) handle these blocking operations internally using low-level concurrency primitives such as locks and condition variables. Here's a simplified explanation of the internal mechanism:
- Locks: The queue uses locks to ensure that only one thread can modify the queue at a time. This prevents race conditions.
- Condition Variables: The queue uses condition variables to manage the state of the queue (e.g., not empty, not full). Threads can wait on these conditions and be notified when the conditions change.

### Q. In the run methods we have called expections , what will happen if interurrupt exception is recieved, will thread stop or continue?
- In the run methods of both the Producer and Consumer classes, we catch InterruptedException. What Happens When InterruptedException is Received
- Interruption During Blocking Operations: If a thread is blocked on a queue.put() (for the producer) or queue.take() (for the consumer) and it is interrupted, an InterruptedException is thrown.
- Handling the Exception: When InterruptedException is caught, the code inside the catch block is executed. Thread.currentThread().interrupt(); is called to restore the interrupted status of the thread. This is a common practice to ensure that the thread's interrupted status is preserved, allowing other parts of the code to detect that an interruption has occurred.
- Thread Behavior After Interruption:
- Exiting the Loop: In the provided code, the while (true) loop does not have a break statement after catching the InterruptedException, so the thread does not exit the loop. Instead, it continues running and re-enters the loop.
- Continuing Execution: Since the loop continues, the thread will attempt to perform the blocking operation (put or take) again. If the thread is not interrupted again, it will continue its normal operation.
- Modifying the Code to Stop the Thread :If you want the thread to stop executing when it is interrupted, you need to add a break statement or return statement inside the catch block:

### Q.Apart from blocking queue, is there any other way to handle this producer and consumer problem?
- Yes, you can solve the Producer-Consumer problem using a LinkedList along with explicit synchronization using wait() and notify() methods. This approach requires careful handling of synchronization to avoid race conditions and ensure proper coordination between producer and consumer threads.

### Q.What thing to take care when using wait method ?
- When using the wait() method in Java, it is crucial to ensure correct synchronization and proper handling of the wait-notify mechanism. 
- wait() must be called within a synchronized block or method. The thread must own the monitor (lock) of the object on which wait() is called.
- Always use the same lock object for calling wait(), notify(), and notifyAll().
- Handling Spurious Wakeups:
- wait() can sometimes return without being notified (a spurious wakeup). To handle this, always call wait() inside a loop that checks the condition. The loop ensures that after being awakened, the thread rechecks the condition and waits again if necessary.
```
synchronized(lock) {
    while (!condition) {
        lock.wait();
    }
  // perform action
}
```
- Properly Use notify() and notifyAll(): Use *notify()* to wake up a single thread waiting on the object's monitor. This should be used when only one thread needs to proceed. Use *notifyAll()* to wake up all threads waiting on the object's monitor. This should be used when any of the waiting threads can proceed.
- Interruptions: Handle InterruptedException appropriately. If a thread is interrupted while waiting, it throws InterruptedException. Typically, you should restore the interrupted status of the thread or handle the interruption in a meaningful way.
- Summary
1. Synchronization: Ensure wait() and notify() are called within synchronized blocks.
2. Condition Check: Always use wait() inside a loop that checks the condition.
3. Notify Properly: Use notify() or notifyAll() to wake up waiting threads appropriately.
4. Interruptions: Handle InterruptedException and restore the thread's interrupt status.

## Coding and SQL

### We Have an Employee table ,with 3 columns namely, Id , salary and name . Write a sql query to get name of employee with second highest salary.
```
SELECT name 
FROM Employee 
ORDER BY salary DESC 
LIMIT 1 OFFSET 1;
```
- This will return only one employee with second highest salary and will not work in case of duplicate salaries. It orders the rows in the Employee table by salary in descending order using ORDER BY salary DESC.
- It uses the LIMIT clause to restrict the result set to one row, starting from the second row (LIMIT 1 OFFSET 1), effectively selecting the second highest salary.
- Finally, it selects the name of the employee with the second highest salary.
- This optimized query is more concise and easier to understand compared to the nested subquery approach, and it achieves the same result.

**What does limit 1 and offset 1 do.**
- The LIMIT and OFFSET clauses are used in SQL queries to control the number of rows returned and where to start returning rows from, respectively.
1. LIMIT: Specifies the maximum number of rows to return in the result set. For example, LIMIT 1 limits the result set to one row.
2. OFFSET: Specifies the number of rows to skip before starting to return rows. For example, OFFSET 1 skips the first row.
- In combination, LIMIT and OFFSET are commonly used for pagination or to retrieve subsets of rows from large result sets.
- In the context of the query SELECT name FROM Employee ORDER BY salary DESC LIMIT 1 OFFSET 1;, LIMIT 1 restricts the result set to one row, and OFFSET 1 skips the first row. As a result, the query returns the second row in the sorted result set, effectively retrieving the name of the employee with the second highest salary.

## For nth highest salary (handles duplicate salaries properly)
- For finding the Nth highest salary, the approach can become quite complex with subqueries. Instead, we can use a different approach using LIMIT and OFFSET in SQL, which works well in MySQL. Here's the approach for finding the Nth highest salary using a Common Table Expression (CTE):
- SQL Query to Find the Employee with the Nth Highest Salary:
1. Using Common Table Expression (CTE) and DENSE_RANK():
```
WITH SalaryRank AS (
    SELECT name, salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rank
    FROM Employee
)
SELECT name
FROM SalaryRank
WHERE rank = 4;  -- Replace 4 with N to get the Nth highest salary
```
- Explanation:
1. Common Table Expression (CTE):
- We define a CTE named SalaryRank that includes the columns name, salary, and the rank of each salary using the DENSE_RANK() window function. DENSE_RANK() ranks the rows based on the salary column in descending order.
```
WITH SalaryRank AS (
    SELECT name, salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rank
    FROM Employee
)
```
2. Select the Nth Highest Salary:
- We then select the name of the employee where the rank matches the desired Nth position.
```
SELECT name
FROM SalaryRank
WHERE rank = 4;  -- Replace 4 with N to get the Nth highest salary
```
This method is flexible and allows you to easily find the Nth highest salary by changing the rank number in the final WHERE clause.

### Q. There are two tables, Emp and Dept , Deptid is foreign key in Emp, Write a sql query to get department name and number of employees in that department 
```
SELECT D.dept_name, COUNT(E.emp_id) AS num_employees
FROM DEPT D
LEFT JOIN EMP E ON D.dept_id = E.dept_id
GROUP BY D.dept_name;
```

### Q.Implement a custom arraylist in Java, we should have 2 methods where we should be able to add elements, While adding the elements we should check the capacity , if the capacity is above 80 percent then we have to double the capacity of arraylist . Then we should have get method to get random access to elements.
- To implement a custom ArrayList in Java, we'll create a class called CustomArrayList. This class will manage an array internally and provide methods to add elements and get elements by index. It will automatically resize the internal array when the capacity exceeds 80%.
```
public class CustomArrayList<T> {
    private T[] array;
    private int size;
    private int capacity;

    // Constructor to initialize the CustomArrayList
    @SuppressWarnings("unchecked")
    public CustomArrayList(int initialCapacity) {
        this.capacity = initialCapacity;
        this.array = (T[]) new Object[initialCapacity];
        this.size = 0;
    }

    // Default constructor with initial capacity of 10
    public CustomArrayList() {
        this(10);
    }

    // Method to add elements to the CustomArrayList
    public void add(T element) {
        if (size >= 0.8 * capacity) {
            resize();
        }
        array[size] = element;
        size++;
    }

    // Method to resize the internal array
    @SuppressWarnings("unchecked")
    private void resize() {
        capacity = capacity * 2;
        T[] newArray = (T[]) new Object[capacity];
        for (int i = 0; i < size; i++) {
            newArray[i] = array[i];
        }
        array = newArray;
    }

    // Method to get an element by index
    public T get(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException("Index: " + index + ", Size: " + size);
        }
        return array[index];
    }

    // Method to get the current size of the CustomArrayList
    public int size() {
        return size;
    }

    // Main method for testing the CustomArrayList
    public static void main(String[] args) {
        CustomArrayList<Integer> customArrayList = new CustomArrayList<>();

        // Adding elements to the CustomArrayList
        for (int i = 1; i <= 20; i++) {
            customArrayList.add(i);
        }

        // Getting elements from the CustomArrayList
        for (int i = 0; i < customArrayList.size(); i++) {
            System.out.print(customArrayList.get(i) + " ");
        }
    }
}
```
- Explanation
- Constructor: Initializes the CustomArrayList with a specified initial capacity or a default capacity of 10. Uses an array to store elements and keeps track of the current size and capacity.
- Add Method: Adds a new element to the list. Checks if the size exceeds 80% of the current capacity. If it does, the resize method is called to double the capacity.
- Resize Method: Doubles the capacity of the internal array. Creates a new array with the doubled capacity and copies the existing elements to the new array.
- Get Method: Returns the element at a specified index. Throws an IndexOutOfBoundsException if the index is out of the valid range.
- Main Method: Tests the CustomArrayList by adding and retrieving elements. This implementation ensures that the CustomArrayList resizes itself when needed and provides efficient random access to elements, similar to the behavior of ArrayList in Java.

### Q.Below values of the array represents the value of stock price and index represents the day. Write a code to return the maximum profit a user can make in a day. Input array : [2,1,4,7]
- To solve the problem of finding the maximum profit from stock prices given as an array where the index represents the day, we can use the following approach:
1. Iterate through the array to keep track of the minimum price encountered so far.
2. Calculate the potential profit for each day by subtracting the current price from the minimum price.
3. Keep track of the maximum profit encountered.
```
public class StockProfit {

    public static int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }

        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;

        for (int price : prices) {
            // Update the minimum price encountered so far
            if (price < minPrice) {
                minPrice = price;
            }

            // Calculate the potential profit
            int profit = price - minPrice;

            // Update the maximum profit encountered so far
            if (profit > maxProfit) {
                maxProfit = profit;
            }
        }

        return maxProfit;
    }

    public static void main(String[] args) {
        int[] prices = {2, 1, 4, 7};
        int maxProfit = maxProfit(prices);
        System.out.println("Maximum profit: " + maxProfit); // Output: Maximum profit: 6
    }
}
```
- Explanation
1. Initialization: minPrice is initialized to Integer.MAX_VALUE to ensure that any price in the array will be less than this initial value.
maxProfit is initialized to 0.
2. Iteration: For each price in the array, we update minPrice to be the minimum of the current minPrice and the current price. Calculate the potential profit for the current day by subtracting minPrice from the current price. Update maxProfit to be the maximum of the current maxProfit and the calculated profit.
3. Result: The function returns the maximum profit found.
- Edge Cases : If the input array is empty or null, the function returns 0, as no transactions can be made.
- This algorithm runs in O(n) time complexity, where n is the number of days, because it only involves a single pass through the array. It also uses O(1) space complexity.

### Q.Longest common prefix
```
public static String findLongestCommonPrefix(String[] strs) {
    if (strs == null || strs.length == 0) return "";
    String prefix = strs[0];
    for (int i = 1; i < strs.length; i++) {
        while (strs[i].indexOf(prefix) != 0) {
            prefix = prefix.substring(0, prefix.length() - 1);
            if (prefix.isEmpty()) return "";
        }
    }
    return prefix;
}
```
- Explanation :
1. Null or Empty Check:
```
if (strs == null || strs.length == 0) return "";
```
- If the input array is null or empty, the method returns an empty string as there can be no common prefix.
2. Initialize the Prefix:
```
String prefix = strs[0];
```
The first string in the array is taken as the initial prefix.
3. Iterate Over the Array:
```
for (int i = 1; i < strs.length; i++) {
    while (strs[i].indexOf(prefix) != 0) {
        prefix = prefix.substring(0, prefix.length() - 1);
        if (prefix.isEmpty()) return "";
    }
}
```
- The method iterates over the rest of the strings in the array starting from the second string (i = 1).
- For each string, it checks if the current prefix is a prefix of that string using the indexOf method.
- strs[i].indexOf(prefix) != 0 checks if the prefix is not found at the beginning of the string (indexOf returns 0 if the prefix is found at the start).
- If the current prefix is not found at the beginning, the prefix is shortened by one character from the end using prefix.substring(0, prefix.length() - 1).
- If the prefix becomes empty, the method returns an empty string as there is no common prefix.
- After iterating through all strings, the remaining prefix is the longest common prefix.

For the input array {"flower", "flow", "flight"}:
- Initially, prefix = "flower".
- Comparing with "flow":
- "flow".indexOf("flower") is -1, so the prefix is shortened to "flowe".
- Continue shortening until prefix = "flow" which is found at the start of "flow".
- Comparing with "flight":
- "flight".indexOf("flow") is -1, so the prefix is shortened to "flo", then to "fl", which is found at the start of "flight".
- The final common prefix is "fl".

### Output of below code :
```
interface A {
    int id = 0;
    void incrementId();
    int getId();
}

class Employee implements A {
    int id = 0;

    public void incrementId() {
        id++;
    }

    public int getId() {
        return id;
    }
}

class Professor implements A {
    int id = 0;

    public void incrementId() {
        id++;
    }

    public int getId() {
        return id;
    }
}

class Main {
    public static void main(String[] args) {
        A a1 = new Employee();
        A a2 = new Professor();

        a1.incrementId();
        a2.incrementId();

        System.out.println(a1.getId()); // What would be printed?
    }
}
```
- Now, let's walk through the main method:
- A a1 = new Employee(); creates an instance of Employee and assigns it to the variable a1. The id in Employee is initialized to 0.
- A a2 = new Professor(); creates an instance of Professor and assigns it to the variable a2. The id in Professor is also initialized to 0.
- a1.incrementId(); calls the incrementId method on the Employee instance, which increments id from 0 to 1.
- a2.incrementId(); calls the incrementId method on the Professor instance, which increments id from 0 to 1.
- System.out.println(a1.getId()); calls the getId method on the Employee instance, which returns id, which is 1.
- Therefore, the output printed will be: 1

### Q.There are 1 million records, I want to print unique records in descending order of their age.
- {"Smit", "1000", "30", "IT", "Some Address"});
- {"Smit", "1000", "30", "IT", "Some Address"}); // Duplicate
- {"Smit D", "1000", "30", "IT", "Some Address"});
- {"Smit", "1000", "25", "IT", "Some Address"});
- {"Smit", "1000", "25", "IT", "Some Address"}); // Duplicate
- {"Smit", "1000", "25", "IT", "Some Address"}); // Duplicate
- Given the requirement to handle 1 million records efficiently, we need to optimize the code for performance and memory usage. We can achieve this by using data structures and algorithms that have good performance characteristics.
- Here’s a more optimized approach using a TreeSet to maintain unique records and sort them automatically:
- Use a TreeSet with a custom comparator: This will ensure that the records are sorted as they are inserted and duplicates are handled efficiently.
```
class Employee implements Comparable<Employee> {
    String name;
    String salary;
    int age;
    String dept;
    String address;

    public Employee(String name, String salary, int age, String dept, String address) {
        this.name = name;
        this.salary = salary;
        this.age = age;
        this.dept = dept;
        this.address = address;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Employee employee = (Employee) o;
        return age == employee.age &&
                Objects.equals(name, employee.name) &&
                Objects.equals(salary, employee.salary) &&
                Objects.equals(dept, employee.dept) &&
                Objects.equals(address, employee.address);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, salary, age, dept, address);
    }

    @Override
    public String toString() {
        return name + ", " + salary + ", " + age + ", " + dept;
    }

    @Override
    public int compareTo(Employee other) {
        if (this.age != other.age) {
            return Integer.compare(other.age, this.age); // Descending order by age
        } else {
            // Break ties by comparing other fields to maintain uniqueness
            int cmp = this.name.compareTo(other.name);
            if (cmp != 0) return cmp;
            cmp = this.salary.compareTo(other.salary);
            if (cmp != 0) return cmp;
            cmp = this.dept.compareTo(other.dept);
            if (cmp != 0) return cmp;
            return this.address.compareTo(other.address);
        }
    }
}

public class Main {
    public void printStats(List<String[]> employeeDetails) {
        Set<Employee> employeeSet = new TreeSet<>();
        for (String[] details : employeeDetails) {
            String name = details[0];
            String salary = details[1];
            int age = Integer.parseInt(details[2]);
            String dept = details[3];
            String address = details[4];
            Employee employee = new Employee(name, salary, age, dept, address);
            employeeSet.add(employee);
        }

        for (Employee employee : employeeSet) {
            System.out.println(employee);
        }
    }

    public static void main(String[] args) {
        List<String[]> employeeDetails = new ArrayList<>();
        employeeDetails.add(new String[]{"Smit", "1000", "30", "IT", "Some Address"});
        employeeDetails.add(new String[]{"Smit", "1000", "30", "IT", "Some Address"}); // Duplicate
        employeeDetails.add(new String[]{"Smit D", "1000", "30", "IT", "Some Address"});
        employeeDetails.add(new String[]{"Smit", "1000", "25", "IT", "Some Address"});
        employeeDetails.add(new String[]{"Smit", "1000", "25", "IT", "Some Address"}); // Duplicate
        employeeDetails.add(new String[]{"Smit", "1000", "25", "IT", "Some Address"}); // Duplicate
        // Add more records as needed

        Main main = new Main();
        main.printStats(employeeDetails);
    }
}
```
- Employee Class: The Employee class implements Comparable<Employee> to provide a natural ordering for the TreeSet. The compareTo method ensures that employees are sorted by age in descending order and breaks ties by comparing other fields to ensure uniqueness.
- TreeSet: Using a TreeSet automatically sorts the elements and removes duplicates based on the compareTo method.
- Main Logic: The printStats method processes the list of employee details and adds each employee to the TreeSet. It then iterates through the TreeSet and prints each unique, sorted employee. This approach ensures that the code is optimized for handling large datasets, providing efficient insertion, uniqueness check, and sorting with the TreeSet.

### String with any numerical digits. Calculate the number of digits . 
```
public class Main {
    public static void main(String[] args) {
        String input = "This is a test string with numbers 1234567890";
        int numberOfDigits = countDigits(input);
        System.out.println("Number of digits in the string: " + numberOfDigits);
    }

    public static int countDigits(String input) {
        int count = 0;
        for (int i = 0; i < input.length(); i++) {
            if (Character.isDigit(input.charAt(i))) {
                count++;
            }
        }
        return count;
    }
}
```
- Explanation:
- Input String: The input string contains alphanumeric characters and spaces.
- countDigits Method: This method takes a string as input and initializes a count variable to zero. It iterates over each character in the string. It checks if the current character is a digit using the Character.isDigit method.If it is a digit, it increments the count.
- Main Method: The main method demonstrates the usage of the countDigits method with a sample input string. It prints the number of digits found in the string.
- Output: When you run this code, it will output:  Number of digits in the string: 10
- This solution is efficient with a time complexity of O(n), where n is the length of the string. It processes each character in the string exactly once.

### Output of below java code
```
public class Test {
    public static void main(String[] args) {
        Integer a = 1000, b = 1000;
        System.out.println(a == b);

        Integer c = 100, d = 100;
        System.out.println(c == d);
    }
}
```
The output of this code will be:
```
false
true
```
- Explanation:
1. Integer Caching Mechanism: Java caches Integer objects for values between -128 and 127. This is known as the Integer Cache.When you create Integer objects using autoboxing within this range, they refer to the same cached objects.
2. Comparison with == Operator: The == operator compares the references of objects, not their values.
- Analysis of the Code:
For a and b:
```
Integer a = 1000, b = 1000;
System.out.println(a == b);
```
The values 1000 are outside the cache range (-128 to 127). Therefore, a and b refer to different Integer objects. a == b compares the references of these two different objects, which are not the same. Thus, the output is *false*. \
For c and d:
```
Integer c = 100, d = 100;
System.out.println(c == d);
```
The values 100 are within the cache range (-128 to 127). Therefore, c and d refer to the same cached Integer object. c == d compares the references of these two objects, which are the same. Thus, the output is *true*.


### Check if strings are anagrams of each others
- Anagrams are strings that are exactly same when read from front or back
1. Sort and Check
```
public static boolean areAnagrams(String str1, String str2) {
        // If lengths are not the same, they cannot be anagrams
        if (str1.length() != str2.length()) {
            return false;
        }

        // Convert both strings to character arrays
        char[] charArray1 = str1.toCharArray();
        char[] charArray2 = str2.toCharArray();

        // Sort both character arrays
        Arrays.sort(charArray1);
        Arrays.sort(charArray2);

        // Compare the sorted arrays
        return Arrays.equals(charArray1, charArray2);
    }
```
2. Using Character Count
```
public static boolean areAnagrams(String str1, String str2) {
        if (str1.length() != str2.length()) {
            return false;
        }

        Map<Character, Integer> charCountMap = new HashMap<>();

        // Count characters in the first string
        for (char c : str1.toCharArray()) {
            charCountMap.put(c, charCountMap.getOrDefault(c, 0) + 1);
        }

        // Subtract counts using the second string
        for (char c : str2.toCharArray()) {
            if (!charCountMap.containsKey(c)) {
                return false;
            }
            charCountMap.put(c, charCountMap.get(c) - 1);
            if (charCountMap.get(c) == 0) {
                charCountMap.remove(c);
            }
        }

        // If the map is empty, the strings are anagrams
        return charCountMap.isEmpty();
    }
```

### Custom Immutable class in Java
- Steps to Make a Class Immutable
1. Declare the class as final so it cannot be subclassed.
2. Make all fields private and final to prevent modification after the object is constructed.
3. Do not provide setters for any fields.
4. Provide only getters to access the fields.
5. If the class holds references to mutable objects, ensure that getters return deep copies of these objects.
- the tags list passed to the constructor is copied using the new ArrayList<>(tags) statement. This deep copy ensures that any modifications to the original tags list after the ImmutableClass object is created do not affect the internal state of the ImmutableClass object.

```
public final class ImmutableClass {
    private final int id;
    private final String name;
    private final List<String> tags;

    // Constructor
    public ImmutableClass(int id, String name, List<String> tags) {
        this.id = id;
        this.name = name;
        // Create a deep copy of the list to ensure immutability
        this.tags = new ArrayList<>(tags);
    }

    // Getters
    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    // Return a copy of the list to preserve immutability
    public List<String> getTags() {
        return new ArrayList<>(tags);
    }

    // No setters provided
}

```

### Second largest integer
```
public static int findSecondLargest(int[] arr) {
        if (arr == null || arr.length < 2) {
            throw new IllegalArgumentException("Array must contain at least two elements.");
        }

        int largest = Integer.MIN_VALUE;
        int secondLargest = Integer.MIN_VALUE;

        for (int num : arr) {
            if (num > largest) {
                secondLargest = largest;
                largest = num;
            } else if (num > secondLargest && num < largest) {
                secondLargest = num;
            }
        }

        if (secondLargest == Integer.MIN_VALUE) {
            throw new IllegalArgumentException("No second largest element found.");
        }

        return secondLargest;
    }
```


## Other topics

### Q.What is kubernetes?
- Kubernetes, often abbreviated as K8s,is designed to automate deploying, scaling, and operating application containers.
- *Why Do We Require Kubernetes?*
- In simple terms, Kubernetes helps manage applications that are made up of multiple containers. Containers are like lightweight, standalone, and executable software packages that include everything needed to run a piece of software, including the code, runtime, system tools, and libraries. Containers can run on any computer and in any environment without needing to be modified.
1. Automates Deployment and Scaling:
- Without Kubernetes: Manually deploying and scaling applications across multiple servers is labor-intensive and error-prone.
- With Kubernetes: You can define how your applications should be deployed and scaled, and Kubernetes automatically manages these tasks.
2. Self-Healing:
- Without Kubernetes: If a part of your application fails, you need to manually detect and fix the issue.
- With Kubernetes: It automatically detects failures, replaces failed containers, and restarts them as needed.
3. Efficient Resource Utilization:
- Without Kubernetes: Ensuring efficient use of server resources can be challenging.
- With Kubernetes: It optimally places containers based on their resource requirements and server capacity.
4. Load Balancing:
- Without Kubernetes: Distributing network traffic across multiple containers manually can be complex.
- With Kubernetes: It automatically load balances network traffic to ensure stability and performance.

### Q.Microservice vs monolithic difference 
- Microservices and monolithic architectures are two different approaches to designing and building software applications. Each has its own advantages and disadvantages, and they are suitable for different types of projects and organizational needs.
1. Single Codebase vs. Decoupled Services
- Monolithic Architecture: Single Codebase - All components of the application are tightly integrated into a single, unified codebase. This means that the user interface, business logic, and data access layers are all part of one large codebase.
- Microservices Architecture: Decoupled Services - The application is divided into smaller, independent services. Each service handles a specific piece of functionality and can be developed, deployed, and scaled independently.
2. Single Deployment vs. Independent Deployment
- Monolithic Architecture: Single Deployment - The entire application is packaged and deployed as a single unit. Any change in the application requires redeploying the entire system.
- Microservices Architecture: Independent Deployment - Each microservice can be deployed independently, allowing for more flexible and faster deployment cycles.
3. Tightly Coupled Components vs. Communication
- Monolithic Architecture: Tightly Coupled Components - Components are tightly linked, making it difficult to isolate and modify individual parts without impacting others.
- Microservices Architecture: Communication - Services typically communicate with each other through well-defined APIs, often using HTTP/REST or messaging queues.
4. Scalability
- Monolithic Architecture: Scalability - Difficult to scale components independently. The entire application must be scaled even if only one part needs more resources.
- Microservices Architecture: Scalability - Individual services can be scaled independently based on demand, leading to more efficient use of resources.
5. Deployment
- Monolithic Architecture: Deployment - Any change, even a small one, requires redeploying the entire application, which can be time-consuming and risky.
- Microservices Architecture: Deployment - Small, independent services can be deployed more frequently and quickly, enabling continuous delivery and integration.

### Q.Kubernetes with microservices vs kubernetes with monolithic
1. Microservices with Kubernetes
- Independent Scaling: Kubernetes efficiently scales individual microservices based on demand, optimizing resource usage.
- Resilience: Kubernetes handles container failures and manages microservices independently, ensuring overall application stability.
- Continuous Deployment: Kubernetes supports seamless updates and deployments, aligning well with microservices' frequent updates.

2. Monolithic Applications on Kubernetes
- Single Deployment Unit: Monolithic apps are deployed as one unit; any change requires full redeployment, which can be inefficient.
- Resource Utilization: Scaling monolithic applications means scaling the entire app, leading to potential resource wastage.
- Complexity in Scaling: Different scaling needs within monolithic apps can't be individually addressed, causing possible over-provisioning.



