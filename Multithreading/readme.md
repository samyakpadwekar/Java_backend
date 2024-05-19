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

