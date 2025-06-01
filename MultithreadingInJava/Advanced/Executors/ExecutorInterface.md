<!-- TODO: Add content for this topic -->

# Executor Interface
Here’s a comprehensive draft for the file MultithreadingInJava/Advanced/Executors/ExecutorInterface.md, covering the Java Executor interface, its purpose, usage, and examples:

---

# Executor Interface

The `Executor` interface is a key component of Java’s concurrency framework, introduced in Java 5 as part of the `java.util.concurrent` package. It provides a simple way of decoupling task submission from the mechanics of how each task will be run, including details such as thread use, scheduling, and synchronization.

## Purpose

- **Abstraction:** The `Executor` interface abstracts the execution of tasks from how they are run (e.g., directly in the calling thread, in a new thread, or in a thread pool).
- **Flexibility:** Enables switching between different execution strategies without changing your application logic.
- **Simplifies Concurrency:** Makes it easier to manage and control thread usage in concurrent applications.

## The Executor Interface

The interface is extremely simple, containing only one method:

```java
public interface Executor {
    void execute(Runnable command);
}
```

- The method accepts a `Runnable` task and executes it at some time in the future.

## Common Implementations

- **ThreadPoolExecutor:** Executes tasks using a pool of worker threads.
- **ScheduledThreadPoolExecutor:** Schedules commands to run after a given delay or periodically.
- **ExecutorService:** A more feature-rich subinterface that adds lifecycle and shutdown management.

## Basic Usage Example

```java
import java.util.concurrent.Executor;
import java.util.concurrent.Executors;

public class ExecutorExample {
    public static void main(String[] args) {
        Executor executor = Executors.newSingleThreadExecutor();

        Runnable task = () -> System.out.println("Task executed by: " + Thread.currentThread().getName());
        executor.execute(task);
    }
}
```

In the above example:
- `Executors.newSingleThreadExecutor()` returns an `Executor` that uses a single worker thread.
- The `execute` method submits a task for execution.

## Custom Executor Implementation

You can implement the `Executor` interface to define your own execution strategy. Here’s a simple example that runs each task in a new thread:

```java
public class SimpleExecutor implements Executor {
    @Override
    public void execute(Runnable command) {
        new Thread(command).start();
    }
}
```

## Best Practices

- Prefer using built-in executors from `Executors` or `ThreadPoolExecutor` for production code, as they are optimized and well-tested.
- Always ensure proper shutdown of executors (if applicable) to avoid resource leaks.
- Use the `ExecutorService` interface if you need to manage the executor’s lifecycle (for example, shutting down the executor).

## When to Use Executor

- When you need to submit tasks independently of how and when they are executed.
- When you want to take advantage of thread pools for efficient resource management.
- When you want to separate task submission from task execution logic.

## References

- [Java Docs: Executor Interface](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executor.html)
- [Java Concurrency Tutorial: Executors](https://docs.oracle.com/javase/tutorial/essential/concurrency/executors.html)

---

Let me know if you want to add or remove any sections or if you’d like a more advanced example!
<!-- Content will be added later -->
