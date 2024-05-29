### Thread and it's type
- A thread is the smallest unit of execution within a process. Threads allow concurrent execution of multiple tasks within a single process, enabling efficient utilization of CPU resources. Mainly there are two types:
1. User Threads
These threads are created and managed by the application or user-level libraries, rather than the operating system. User threads provide flexibility and are usually more lightweight than kernel threads. However, they rely on the underlying kernel threads for execution.
2. Daemon Threads
Daemon threads are background threads that run in the background and provide services to user threads or perform tasks such as garbage collection, monitoring, etc. They automatically terminate when all non-daemon threads have finished execution.

### Thread Transition
- Thread transition refers to the movement of a thread between different states during its lifecycle. Here's a [brief explanation](https://medium.com/javarevisited/thread-state-and-lifecycle-in-java-multithreading-updated-2023-8e6bf29a7666):
1. New: The thread is in this state when it's created but not yet started.
2. Runnable: The thread is ready to run and waiting for processor time.
3. Running: The thread is currently executing its task.
4. Blocked/Waiting: The thread is temporarily inactive, waiting for a resource or condition to become available.
5. Timed Waiting: Similar to Blocked, but with a timeout period.
6. Terminated/Dead: The thread has completed execution or been terminated.
- Threads transition between these states depending on their execution, waiting for resources, and other factors. Efficient management of these transitions ensures effective utilization of system resources and proper synchronization in multi-threaded applications.

### Thread creation implementing runnable interface

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

### Thread creation extending Thread class

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


### Thread running and yielding
- In Java, the Thread.yield() method is used to give a hint to the scheduler that the current thread is willing to pause its execution temporarily, allowing other threads of equal priority to run.
1. Running a Thread
- When a thread is running, it is actively executing its task or code. The scheduler allocates CPU time to the thread, and it progresses through its execution until it either completes its task or yields the CPU voluntarily or involuntarily (due to time slicing).
2. Yielding a Thread
- Purpose: The yield() method is called by a thread to indicate that it's willing to give up its current use of the CPU.
- Effect: When a thread yields, it moves from the running state back to the runnable state, allowing other threads of equal priority to have a chance to run.
- Usage: It's typically used in situations where a thread has completed a small unit of work or is in a state where it can temporarily give up the CPU without adverse effects.
```
public class MyRunnable implements Runnable {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
            Thread.yield(); // Yielding the CPU voluntarily
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Runnable task = new MyRunnable();
        Thread thread1 = new Thread(task, "Thread 1");
        Thread thread2 = new Thread(task, "Thread 2");

        thread1.start();
        thread2.start();
    }
}
```
- Both Thread 1 and Thread 2 are instances of the same MyRunnable class and share the same runnable task.
- When Thread.yield() is called inside the run() method of MyRunnable, it gives up the CPU, allowing the other thread to run.
-This alternation between threads continues until both threads complete their execution or are interrupted.
- When to Use Yielding
1. Fairness: Use yielding to promote fairness among threads of equal priority.
2. Resource Sharing: Use it when threads can temporarily give up CPU time without impacting the correctness of the program.


### Thread Sleeping and Waking
- In Java, the Thread.sleep() method is used to pause the execution of a thread for a specified amount of time. Here's how it works:
1. Sleeping a Thread
-Purpose: The sleep() method suspends the execution of the current thread for the specified duration.
- Usage: It's commonly used to introduce delays or wait periods in a thread's execution.
- Exception: It throws InterruptedException if the thread is interrupted while sleeping.
2. Waking a Thread
- Interrupt: To wake a sleeping thread prematurely, another thread can interrupt it using the interrupt() method.
- Exception Handling: The sleeping thread should handle InterruptedException to respond appropriately to being interrupted.
```
public class MyRunnable implements Runnable {
    public void run() {
        try {
            System.out.println(Thread.currentThread().getName() + " is starting.");
            Thread.sleep(5000); // Sleep for 5 seconds
            System.out.println(Thread.currentThread().getName() + " has woken up.");
        } catch (InterruptedException e) {
            System.out.println(Thread.currentThread().getName() + " was interrupted while sleeping.");
            // Handle the interruption gracefully
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(new MyRunnable(), "WorkerThread");
        thread.start();
        
        // Interrupt the thread after 2 seconds
        try {
            Thread.sleep(2000);
            thread.interrupt(); // Interrupt the sleeping thread
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```
- Is Interrupting a Sleeping Thread a Good Choice?
1.Complexity: In complex applications, interrupting a sleeping thread can introduce unexpected behavior or lead to synchronization issues.
2. Graceful Handling: Sleeping threads should handle interruptions gracefully to ensure that resources are released properly and the application remains responsive.
3. Alternative Approaches: Consider using other synchronization mechanisms or higher-level concurrency utilities for better control over thread interruption and coordination.
- [Java sleep and interruption](https://samedesilva.medium.com/java-thread-sleep-and-interrupt-methods-3850e6201169)


### Thread wait,notify,notifyAll
```
import java.util.LinkedList;

public class SharedResource {
    private LinkedList<Integer> items = new LinkedList<>();
    private final int MAX_SIZE = 5; // Maximum capacity of the shared resource

    public synchronized void produce(int item) {
        while (items.size() >= MAX_SIZE) {
            try {
                System.out.println("Producer is waiting as the resource is full...");
                wait(); // Wait if the resource is full
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        items.add(item);
        System.out.println("Producer produced item: " + item);
        notify(); // Notify the consumer that an item is available
    }

    public synchronized int consume() {
        while (items.isEmpty()) {
            try {
                System.out.println("Consumer is waiting as the resource is empty...");
                wait(); // Wait if the resource is empty
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        int item = items.remove();
        System.out.println("Consumer consumed item: " + item);
        notifyAll(); // Notify all producers that space is available
        return item;
    }
}

public class Producer implements Runnable {
    private SharedResource resource;

    public Producer(SharedResource resource) {
        this.resource = resource;
    }

    @Override
    public void run() {
        for (int i = 1; i <= 10; i++) {
            resource.produce(i);
            try {
                Thread.sleep(1000); // Simulate production time
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class Consumer implements Runnable {
    private SharedResource resource;

    public Consumer(SharedResource resource) {
        this.resource = resource;
    }

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            resource.consume();
            try {
                Thread.sleep(2000); // Simulate consumption time
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();
        Thread producerThread = new Thread(new Producer(resource));
        Thread consumerThread = new Thread(new Consumer(resource));

        producerThread.start();
        consumerThread.start();
    }
}
```
- Explanation:
1. Producer-Consumer Interaction:
- Producers produce items and add them to the shared resource using the produce() method.
- Consumers consume items from the shared resource using the consume() method.
2. Synchronization:
- Both produce() and consume() methods are synchronized to ensure thread safety.
- If the resource is full, the producer waits by calling wait() until space is available.
- If the resource is empty, the consumer waits by calling wait() until an item is available.
3. Notification:
- When a producer produces an item, it notifies the consumer by calling notify().
- When a consumer consumes an item, it notifies all producers that space is available by calling notifyAll().
4. Output:
- The output demonstrates the producer producing items and the consumer consuming them, while ensuring that the resource capacity is maintained and threads wait when necessary.

- [Detailed explanation](https://medium.com/@adam.rizk9/demystifying-java-wait-notify-and-join-methods-for-multithreading-an-in-depth-look-ffb43a514bbc)


### Thread priority
- Thread priority in Java is a crucial concept that helps in determining the order in which threads are scheduled for execution.
- In Java, thread priorities range from MIN_PRIORITY (1) to MAX_PRIORITY (10), with NORM_PRIORITY (5) being the default for every thread.
- Setting thread priorities allows you to control the relative importance of threads, influencing which threads should be executed first when multiple threads compete for system resources.
- The use of thread priority in Java is significant for managing the execution order and resource allocation of threads in multi-threaded programming.
- By assigning priorities to threads, you can ensure that high-priority threads are given precedence over lower-priority ones, although the exact execution order is platform-dependent and not guaranteed.
- However, manipulating thread priorities in Java comes with certain risks. High-priority threads can potentially monopolize CPU time, leading to situations like "starvation" where lower-priority threads may not get a chance to run, causing unpredictable behavior or performance issues.
```
public class PriorityExample {
    public static void main(String[] args) {
        Thread thread1 = new Thread(new MyRunnable(), "Thread 1");
        Thread thread2 = new Thread(new MyRunnable(), "Thread 2");

        // Set priorities
        thread1.setPriority(Thread.MIN_PRIORITY); // Priority 1
        thread2.setPriority(Thread.MAX_PRIORITY); // Priority 10

        thread1.start();
        thread2.start();
    }
}
```

### Thread scheduling and scheduler
- **Thread scheduling** in Java is typically preemptive. This means the thread scheduler can suspend the currently running thread to allow another thread to run. The decision is based on thread priorities and the state of the threads. However, the actual behavior can vary depending on the JVM implementation and the underlying operating system.
- A component of Java that decides which thread to run or execute and which thread to wait is called a **thread scheduler** in Java. In Java, a thread is only chosen by a thread scheduler if it is in the runnable state. However, if there is more than one thread in the runnable state, it is up to the thread scheduler to pick one of the threads and ignore the other ones. There are some criteria that decide which thread will execute first. There are two factors for scheduling a thread i.e. Priority and Time of arrival.
1. Priority: Priority of each thread lies between 1 to 10. If a thread has a higher priority, it means that thread has got a better chance of getting picked up by the thread scheduler.
2. Time of Arrival: Suppose two threads of the same priority enter the runnable state, then priority cannot be the factor to pick a thread from these two threads. In such a case, arrival time of thread is considered by the thread scheduler. A thread that arrived first gets the preference over the other threads.

**Thread Scheduling Algorithms**
1. Fixed Priority Scheduling:
- Threads are scheduled based on their priority. Higher priority threads are given preference over lower priority ones. If multiple threads have the same priority, they are scheduled in a round-robin manner.
2. Time-Slicing (Round-Robin Scheduling):
- Each thread is given a fixed time slice or quantum to run. After its time slice expires, the thread is moved to the back of the queue, and the next thread is given a chance to run. This ensures that all runnable threads get a fair share of the CPU time.
3. First-Come-First-Served (FCFS):
- Threads are scheduled in the order they arrive in the runnable state. The first thread to arrive is the first to be scheduled.

- [Detailed explanation](https://www.javatpoint.com/thread-scheduler-in-java)


### Deadlock,Livelock,Startvation and Race condition
1. Deadlock
- Definition: A situation where two or more threads are unable to proceed because each is waiting for the other to release a resource.
- Example: Thread A holds Lock 1 and waits for Lock 2, while Thread B holds Lock 2 and waits for Lock 1.
- Impact: The threads remain blocked indefinitely.
2. Livelock
- Definition: A situation where two or more threads keep changing their state in response to each other without making any progress.
- Example: Two threads repeatedly yielding to each other in an attempt to avoid deadlock.
- Impact: The threads continue running but do not perform useful work.
3. Starvation
- Definition: A situation where a thread is perpetually denied access to resources, preventing it from making progress.
- Example: A low-priority thread never gets CPU time because high-priority threads keep running.
- Impact: The starved thread cannot complete its task.
4. Race Condition
- Definition: A situation where the behavior of a program depends on the relative timing of threads executing, leading to unpredictable results.
- Example: Two threads simultaneously incrementing a shared counter without proper synchronization.
- Impact: Leads to inconsistent or incorrect data.
- [Detailed explanation](https://pradeesh-kumar.medium.com/deadlock-livelock-race-condition-and-starvation-c225018bbae6)


### Q.which maps are thread safe in java collections?
1. *Collections.synchronizedMap*
2. *ConcurrentHashMap*
- Choosing the Right Thread-Safe Map
1. Performance: If you need high performance in a concurrent environment, ConcurrentHashMap is typically the best choice. It allows concurrent reads and fine-grained locking for write operations.
2. Legacy Code: If you’re working with legacy code that already uses Hashtable or if simplicity is a priority over performance, Hashtable or Collections.synchronizedMap might be sufficient.
3. Simplicity vs. Concurrency: If you need a simple thread-safe map and don’t expect high contention, Collections.synchronizedMap can be used. However, for better scalability and performance, especially in a highly concurrent environment, prefer ConcurrentHashMap.

### Q.how does synchronized and concurrentHashMap ensures thread safety?
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


- [thread pool and executer service](https://medium.com/@erayaraz10/a-comprehensive-guide-to-thread-pools-in-java-75a06657fda)

- [reentrant-locks](https://medium.com/@greekykhs/reentrant-locks-163ee3d6f9a5)


## Read about Executor Service and Threadpool, Reentrant lock
