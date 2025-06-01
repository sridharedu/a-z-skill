<!-- TODO: Add content for this topic -->

# Future Interface
Great! I’ll provide a detailed explanation and example for the Java Future interface that you can use to fill the FutureInterface.md file.

---

# Future Interface

The `Future` interface in Java represents the result of an asynchronous computation. It provides methods to check if the computation is complete, to wait for its completion, and to retrieve the result. Futures are most commonly used with Java's Executor framework.

## Key Methods

- `get()`: Waits if necessary for the computation to complete, then retrieves the result.
- `get(long timeout, TimeUnit unit)`: Waits for the computation to complete up to the specified timeout.
- `cancel(boolean mayInterruptIfRunning)`: Attempts to cancel execution.
- `isCancelled()`: Returns true if the task was canceled before it completed.
- `isDone()`: Returns true if the task is completed.

## Usage Example

```java
import java.util.concurrent.*;

public class FutureExample {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        ExecutorService executor = Executors.newSingleThreadExecutor();

        Callable<Integer> task = () -> {
            Thread.sleep(2000); // Simulate long computation
            return 42;
        };

        Future<Integer> future = executor.submit(task);

        System.out.println("Task submitted, doing other work...");

        // Wait for the result
        Integer result = future.get();
        System.out.println("Result: " + result);

        executor.shutdown();
    }
}
```

## When to Use Future

- When you want to execute tasks asynchronously and retrieve their results later.
- When you need to manage timeouts or cancel running tasks.
- When you want to check if a task has completed without blocking.

## Limitations

- The standard `Future` does not provide a way to receive a callback when the computation completes; you must poll or block.
- For more advanced asynchronous programming, consider using `CompletableFuture` introduced in Java 8.

---

Would you like to include an advanced example or explanation about `CompletableFuture` as well?
<!-- Content will be added later -->
