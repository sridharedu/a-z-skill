<!-- TODO: Add content for this topic -->

# ReentrantLock
Here’s an explanation of ReentrantLock in Java:

---

## ReentrantLock in Java

A ReentrantLock is a synchronization aid introduced in Java’s `java.util.concurrent.locks` package. It provides a more flexible and powerful locking mechanism compared to the traditional `synchronized` keyword.

### Key Features

1. **Reentrancy**
   - If a thread holds the lock, it can acquire it again without deadlocking itself.
   - The lock keeps track of how many times it’s been acquired by the same thread; it must be released the same number of times.

2. **Explicit Locking**
   - You must explicitly lock and unlock using `lock()` and `unlock()` methods.
   - Unlike `synchronized`, forgetting to call `unlock()` may lead to deadlocks.

3. **Try Lock & Timed Lock**
   - `tryLock()` method allows you to attempt to acquire the lock without blocking.
   - You can also try to acquire the lock within a certain time.

4. **Fairness Policy**
   - You can create a fair lock (`new ReentrantLock(true)`) to grant access to the longest-waiting thread, or a non-fair lock (`new ReentrantLock()`) for higher throughput.

5. **Condition Variables**
   - Supports multiple condition variables via the `newCondition()` method, enabling advanced thread signaling (like having multiple `wait()`/`notify()` queues).

### Basic Example

```java
import java.util.concurrent.locks.ReentrantLock;

public class Counter {
    private final ReentrantLock lock = new ReentrantLock();
    private int count = 0;

    public void increment() {
        lock.lock();
        try {
            count++;
        } finally {
            lock.unlock(); // Always unlock in the finally block
        }
    }
}
```

### When to Use ReentrantLock

- When you need advanced locking features (fairness, tryLock, multiple conditions).
- When you want explicit control over lock acquisition and release.
- For complex synchronization scenarios that can’t be handled by `synchronized`.

### Caution

- Always ensure that every call to `lock()` is matched with a call to `unlock()` (usually in a `finally` block) to avoid deadlocks.

---

Would you like more detailed examples or a deeper dive into advanced features like conditions or fairness?
<!-- Content will be added later -->
