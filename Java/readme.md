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



## Coding

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

- For the input array {"flower", "flow", "flight"}:
- Initially, prefix = "flower".
- Comparing with "flow":
- "flow".indexOf("flower") is -1, so the prefix is shortened to "flowe".
- Continue shortening until prefix = "flow" which is found at the start of "flow".
- Comparing with "flight":
- "flight".indexOf("flow") is -1, so the prefix is shortened to "flo", then to "fl", which is found at the start of "flight".
- The final common prefix is "fl".

