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
