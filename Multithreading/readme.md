### Implementing runnable interface

- Steps to Create and Run a Thread Using the Runnable Interface
1. Create a Class that Implements Runnable:
- Implement the Runnable interface and override its run method. This method contains the code that defines the task to be executed by the thread.
2. Create an Instance of the Runnable Implementation:
- Instantiate the class that implements Runnable.
3. Create a Thread Object and Pass the Runnable Instance to It:
- Create a new Thread object and pass the Runnable instance to the Thread constructor.
4. Start the Thread:
- Call the start method on the Thread object to begin execution.
```
class MyRunnable implements Runnable {
    @Override
    public void run() {
        // Code that will run in a separate thread
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
            try {
                Thread.sleep(1000); // Sleep for 1 second
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();

        Thread thread1 = new Thread(myRunnable, "Thread-1");
        Thread thread2 = new Thread(myRunnable, "Thread-2");

        thread1.start(); // Start the first thread
        thread2.start(); // Start the second thread

        // Optionally, wait for threads to finish
        try {
            thread1.join(); // Wait for thread1 to finish
            thread2.join(); // Wait for thread2 to finish
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Both threads have finished execution.");
    }
}
```

### Implementing runnable interface

1. Create a Custom Thread Class:
- Extend the Thread class.
- Override the run method with the code you want the thread to execute.
2. Start Threads:
- Create instances of your custom thread class.
- Call the start method on each instance to begin execution. This will call the run method in a new thread.
3. Join Threads:
- Use the join method to wait for a thread to complete. This is optional but useful if you need to ensure all threads have finished before proceeding.

```
class MyThread extends Thread {
    @Override
    public void run() {
        // Code that will run in a separate thread
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
            try {
                Thread.sleep(1000); // Sleep for 1 second
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread1 = new MyThread();
        MyThread thread2 = new MyThread();

        thread1.start(); // Start the first thread
        thread2.start(); // Start the second thread

        // Optionally, wait for threads to finish
        try {
            thread1.join(); // Wait for thread1 to finish
            thread2.join(); // Wait for thread2 to finish
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Both threads have finished execution.");
    }
}
```

### Apart from above two ways,there are more better ways of implementing Multithreading,once of which is *[Using Executer Service](https://medium.com/javarevisited/java-multithreading-using-executor-service-ebffd18b00b6)*
```
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class Main {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2); // Pool of 2 threads

        Runnable task = () -> {
            for (int i = 0; i < 5; i++) {
                System.out.println(Thread.currentThread().getName() + " - " + i);
                try {
                    Thread.sleep(1000); // Sleep for 1 second
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        };

        executor.submit(task);
        executor.submit(task);

        executor.shutdown(); // Shut down the executor service
    }
}
```
- Advantages:
1. Thread Management: ExecutorService manages a pool of threads, reducing the overhead of creating and destroying threads frequently.
2. Task Submission: Simplifies task submission with methods like submit and invokeAll, allowing better control over task execution.
3. Concurrency Control: Provides built-in thread pool management strategies like fixed thread pool, cached thread pool, etc., optimizing resource usage.
4. Graceful Shutdown: Allows for graceful shutdown of threads with shutdown and shutdownNow methods, ensuring all running tasks are completed or terminated safely.


### Thready safety in java
- Thread safety ensures that concurrent access to shared resources by multiple threads does not result in data corruption or inconsistent behavior. It's essential for maintaining data integrity and preventing race conditions in multi-threaded applications.
  
- Thread safety can be achieved through various mechanisms, each suited to different scenarios. Here are the primary ways to ensure thread safety:
1. Synchronization
a. Synchronized Methods : Synchronize the entire method to ensure that only one thread can execute it at a time.
```
public synchronized void synchronizedMethod() {
    // Critical section
}
```
b. Synchronized Blocks : Synchronize only a portion of the method for more fine-grained control.
```
public void method() {
    synchronized (this) {
        // Critical section
    }
}
```
2. Volatile Keyword : Use the volatile keyword for variables to ensure visibility of changes to variables across threads.
```
private volatile boolean flag = true;
```
3. Atomic Variables : Use classes from the java.util.concurrent.atomic package for atomic operations without explicit synchronization.
```
import java.util.concurrent.atomic.AtomicInteger;

private AtomicInteger atomicCount = new AtomicInteger(0);

public void increment() {
    atomicCount.incrementAndGet();
}
```

4. Concurrent Collections : Use thread-safe collections from the java.util.concurrent package, such as ConcurrentHashMap, CopyOnWriteArrayList, etc.
```
import java.util.concurrent.ConcurrentHashMap;

private ConcurrentHashMap<String, String> map = new ConcurrentHashMap<>();

public void putValue(String key, String value) {
    map.put(key, value);
}
```

5. Executors and Thread Pools : Use ExecutorService to manage thread creation and lifecycle, avoiding manual thread management.
```
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

ExecutorService executor = Executors.newFixedThreadPool(10);

executor.submit(() -> {
    // Task to be executed
});

executor.shutdown();
```


### Synchronization for Thready Safety
- **Synchronization** is needed in multithreading to prevent **concurrent access issues**. It ensures that only one thread can access a critical section of code at a time, thereby **avoiding data inconsistency** and **race conditions** where multiple threads modify shared resources simultaneously.

**Key Concepts**:
1. Intrinsic Locks (Monitors):
- Every Java object has an intrinsic lock.
- Threads use these locks to coordinate access to shared resources.
2. Synchronized Methods:
- When a thread calls a synchronized method, it must acquire the intrinsic lock of the object.
- Only one thread can hold this lock at a time, ensuring that only one thread can execute any synchronized method of the object.
3. Synchronized Blocks:
- Similar to synchronized methods, but provide more fine-grained control.
- The thread acquires the lock on a specific object before executing the block of code.

**How Synchronization works**
1. Acquiring the Lock:
- When a thread enters a synchronized method or block, it attempts to acquire the intrinsic lock.
- If the lock is already held by another thread, the calling thread is blocked until the lock becomes available.
2. Executing the Code:
- Once the thread acquires the lock, it can safely execute the synchronized code without interference from other threads.
3. Releasing the Lock:
- After the synchronized method or block is executed, the thread releases the lock.
- This allows other waiting threads to acquire the lock and execute their synchronized code.

- Example : A simple counter increment task will be used to demonstrate synchronization. Without synchronization, the result may be inconsistent.
```
class Counter {
    private int count = 0;

    public void increment() {
        int temp = count;
        temp++;
        count = temp;
    }

    public int getCount() {
        return count;
    }
}
```

1. Synchronized Method : Synchronize the entire method to ensure only one thread can execute it at a time.
```
class Counter {
    private int count = 0;

    public synchronized void increment() {
        int temp = count;
        temp++;
        count = temp;
    }

    public int getCount() {
        return count;
    }
}
```

2. Synchronized Block : A synchronized block works similarly but offers finer control by allowing you to synchronize only a specific part of the code rather than the entire method
```
class Counter {
    private int count = 0;

    public void increment() {
        synchronized (this) {
            int temp = count;
            temp++;
            count = temp;
        }
    }

    public int getCount() {
        return count;
    }
}
```

3. Using synchronized with ExecutorService : Combine synchronization with a thread pool to manage concurrent execution. Manages thread execution and combines well with synchronized methods or blocks for concurrency control.
```
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class Counter {
    private int count = 0;

    public synchronized void increment() {
        int temp = count;
        temp++;
        count = temp;
    }

    public int getCount() {
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        Counter counter = new Counter();
        ExecutorService executor = Executors.newFixedThreadPool(2);

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        };

        executor.submit(task);
        executor.submit(task);

        executor.shutdown();
        while (!executor.isTerminated()) {}

        System.out.println("Final count: " + counter.getCount());
    }
}
```

### How Synchronization in Static Methods Works
1. Class-Level Lock:
- When a static method is declared as synchronized, the lock used is associated with the Class object of the class containing the method.
- This is different from instance methods, where the lock is associated with the instance of the object.
2. Lock Acquisition:
- When a thread calls a synchronized static method, it must acquire the lock on the Class object.
- If another thread is already holding the lock (e.g., it is executing another synchronized static method of the same class), the calling thread is blocked until the lock is released.
3. Lock Release:
- After the thread finishes executing the synchronized static method, it releases the lock on the Class object.
- This allows other waiting threads to acquire the lock and execute synchronized static methods of that class.
```
class Counter {
    private static int count = 0;

    // Synchronized static method
    public static synchronized void increment() {
        count++;
    }

    // Another synchronized static method
    public static synchronized void decrement() {
        count--;
    }

    public static int getCount() {
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                Counter.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                Counter.decrement();
            }
        });

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final count: " + Counter.getCount());
    }
}
```
- Explanation
- Synchronized Static Methods (increment and decrement):
- Both methods are synchronized at the class level.
- When increment() or decrement() is called, the thread must acquire the lock on the Class object of Counter.
- This ensures that only one thread can execute either increment or decrement at any given time, providing thread-safe access to the shared static variable count.

### Volatile keyword for thread safety
- The volatile keyword ensures visibility of changes to variables across threads. It guarantees that when a thread writes to a volatile variable, the value is immediately visible to other threads.
1. volatile is lightweight and ensures visibility only, unlike synchronization mechanisms which provide both visibility and atomicity.
2. Use volatile when you only need visibility guarantees, but for operations requiring atomicity or compound actions, other mechanisms like synchronization or atomic variables should be preferred.

### Executors and Thread Pools for thread safety
- Using Executors and Thread Pools ensures thread safety by managing a pool of threads and controlling the execution of tasks. Each task submitted to an Executor is executed sequentially, one after the other, by the threads in the pool. This sequential execution eliminates the need for explicit synchronization in most cases, as each task is executed independently of others, ensuring thread safety.
- Scenarios to use Executors and Thread Pools:
1. Task Execution : When you have multiple tasks that need to be executed concurrently, but in a controlled manner, Executors and Thread Pools are useful.
2. Resource Management : If your application requires efficient management of thread resources, such as limiting the number of concurrent threads, reusing threads, and managing their lifecycle, Executors and Thread Pools are ideal.
3. Concurrent Operations : When dealing with I/O-bound or CPU-bound operations that can be parallelized, Executors and Thread Pools simplify concurrent execution, providing better performance and resource utilization.
4. Preventing Thread Explosion : Executors and Thread Pools help prevent a "thread explosion" scenario, where creating threads manually may lead to excessive resource consumption and degradation of system performance.
- In summary, Executors and Thread Pools are suitable when you need to execute multiple tasks concurrently, manage thread resources efficiently, and ensure thread safety without explicit synchronization. They provide a high-level abstraction for concurrent programming, simplifying development and maintenance while promoting thread safety.


### Producer - Consumer problem 
- The Producer-Consumer Problem (sometimes called the Bounded-Buffer Problem) is a classic example of a multi-threaded synchronization problem.
- The problem describes two threads, the Producer and the Consumer, and they are sharing a common, fixed-size bufferthat is used as a queue.
1. The Producer produces an item, puts that item into the buffer, and keeps repeating this process.
2. On the other hand, the Consumer is consuming the item from the shared buffer, one item at a time.

**Where exactly problem occurs** [Code](https://medium.com/@basecs101/producer-consumer-problem-in-java-multi-threading-latest-2a306f003973)
- when the producer added an item into the buffer and the buffer is no longer empty. Then consumer thread-1 tries to remove this item but before doing this, a context switches to back consumer thread-2, now this thread removes the item from the buffer. But again context switches back to the consumer thread-1 and then this thread tries to remove the item from the buffer but there is no item in the buffer and hence ArrayIndexOutOfBoundsException exception occurred.
- This issue occurred as the shared buffer is not synchronized, and hence all the threads are trying to add and remove from the buffer at the same time causing an exception as explained above.


## Read about Executor Service and Threadpool, Reentrant lock
