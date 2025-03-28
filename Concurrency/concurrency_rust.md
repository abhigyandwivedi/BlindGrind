
```rust
use std::sync::{Arc, Mutex}; // Import Arc for shared ownership and Mutex for safe mutable access
use tokio::sync::Notify; // Import Notify for thread synchronization
use tokio::task; // Import task module for spawning asynchronous tasks

#[tokio::main] // Tokio runtime entry point
async fn main() {
    let counter = Arc::new(Mutex::new(1)); // Shared counter protected by a mutex
    let notify_odd = Arc::new(Notify::new()); // Notification mechanism for odd thread
    let notify_even = Arc::new(Notify::new()); // Notification mechanism for even thread

    // Clone shared resources for the odd thread
    let counter_odd = Arc::clone(&counter);
    let notify_odd_thread = Arc::clone(&notify_odd);
    let notify_even_thread = Arc::clone(&notify_even);

    // Clone shared resources for the even thread
    let counter_even = Arc::clone(&counter);
    let notify_odd_thread_even = Arc::clone(&notify_odd);
    let notify_even_thread_even = Arc::clone(&notify_even);

    // Spawn the odd thread
    let odd_thread = task::spawn(odd_numbers(
        counter_odd,
        notify_odd_thread,
        notify_even_thread,
    ));
    // Spawn the even thread
    let even_thread = task::spawn(even_numbers(
        counter_even,
        notify_odd_thread_even,
        notify_even_thread_even,
    ));

    // Start by notifying the odd thread to begin execution
    notify_odd.notify_one();

    // Wait for both threads to complete execution
    let _ = tokio::join!(odd_thread, even_thread);
}

// Function to print odd numbers in order
async fn odd_numbers(counter: Arc<Mutex<i32>>, notify_odd: Arc<Notify>, notify_even: Arc<Notify>) {
    loop {
        notify_odd.notified().await; // Wait until notified
        let mut num = counter.lock().unwrap(); // Acquire lock on the counter
        if *num > 10 {
            // Stop condition
            notify_even.notify_one(); // Ensure even thread exits
            break;
        }
        println!("Odd Thread: {}", *num); // Print odd number
        *num += 1; // Increment counter
        notify_even.notify_one(); // Notify the even thread
    }
}

// Function to print even numbers in order
async fn even_numbers(counter: Arc<Mutex<i32>>, notify_odd: Arc<Notify>, notify_even: Arc<Notify>) {
    loop {
        notify_even.notified().await; // Wait until notified
        let mut num = counter.lock().unwrap(); // Acquire lock on the counter
        if *num > 10 {
            // Stop condition
            notify_odd.notify_one(); // Ensure odd thread exits
            break;
        }
        println!("Even Thread: {}", *num); // Print even number
        *num += 1; // Increment counter
        notify_odd.notify_one(); // Notify the odd thread
    }
}

```

# Understanding Tokio in Rust: Ordered Thread Execution with Asynchronous Notifications

## Introduction

Rust has become one of the most popular programming languages for system-level and high-performance applications due to its memory safety and concurrency capabilities. Tokio, an asynchronous runtime for Rust, plays a significant role in enabling efficient and safe concurrent programming.

In this article, we will explore Tokio's key components, focusing on thread synchronization and inter-thread communication. We will analyze a practical example where two asynchronous tasks (threads) print numbers in an alternating fashion using `tokio::sync::Notify` and `Arc<Mutex<i32>>`. This example demonstrates Tokio's powerful concurrency model and its ability to manage synchronization without blocking system resources.

## The Problem Statement

The goal of our example program is to print numbers from `1` to a user-defined maximum (`max_num`) in an alternating manner using two asynchronous threads:

- **One thread prints odd numbers**
    
- **Another thread prints even numbers**
    

Synchronization is required to ensure that the numbers are printed in the correct order. We achieve this by using Tokio’s `Notify` primitive along with `Arc<Mutex<i32>>` to coordinate the execution between the two tasks.

## Understanding the Code

Let’s break down the code into its essential parts and understand how each component works.

### Importing Required Modules

```rust
use std::sync::{Arc, Mutex}; // Import Arc for shared ownership and Mutex for safe mutable access
use tokio::sync::Notify; // Import Notify for thread synchronization
use tokio::task; // Import task module for spawning asynchronous tasks
use std::env; // Import env to read command-line arguments
```

- `Arc<Mutex<i32>>`: Used for shared access to a counter across multiple tasks. The `Arc` (Atomic Reference Counted) pointer ensures safe ownership sharing, and `Mutex` provides thread-safe mutation of the counter.
    
- `Notify`: Tokio’s lightweight notification system for waking up tasks efficiently without blocking execution.
    
- `task`: The module that provides functions for spawning asynchronous tasks.
    
- `env`: Used to read command-line arguments.
    

### The `main` Function: Initializing and Spawning Tasks

```rust
#[tokio::main] // Tokio runtime entry point
async fn main() {
    let args: Vec<String> = env::args().collect();
    let max_num: i32 = args.get(1).map(|s| s.parse().unwrap_or(10)).unwrap_or(10);

    let counter = Arc::new(Mutex::new(1)); // Shared counter protected by a mutex
    let notify_odd = Arc::new(Notify::new()); // Notification mechanism for odd thread
    let notify_even = Arc::new(Notify::new()); // Notification mechanism for even thread

    let counter_odd = Arc::clone(&counter);
    let notify_odd_thread = Arc::clone(&notify_odd);
    let notify_even_thread = Arc::clone(&notify_even);

    let counter_even = Arc::clone(&counter);
    let notify_odd_thread_even = Arc::clone(&notify_odd);
    let notify_even_thread_even = Arc::clone(&notify_even);

    let odd_thread = task::spawn(odd_numbers(counter_odd, notify_odd_thread, notify_even_thread, max_num));
    let even_thread = task::spawn(even_numbers(counter_even, notify_odd_thread_even, notify_even_thread_even, max_num));

    notify_odd.notify_one();

    let _ = tokio::join!(odd_thread, even_thread);
}
```

- We read the `max_num` from the command-line arguments. If not provided, it defaults to `10`.
    
- The counter and notify mechanisms remain unchanged.
    
- The `max_num` value is passed to both tasks to control the execution limit.
    

### Implementing the Odd Number Task

```rust
async fn odd_numbers(counter: Arc<Mutex<i32>>, notify_odd: Arc<Notify>, notify_even: Arc<Notify>, max_num: i32) {
    loop {
        notify_odd.notified().await; // Wait until notified
        let mut num = counter.lock().unwrap(); // Acquire lock on the counter
        if *num > max_num { // Stop condition
            notify_even.notify_one(); // Ensure even thread exits
            break;
        }
        println!("Odd Thread: {}", *num); // Print odd number
        *num += 1; // Increment counter
        notify_even.notify_one(); // Notify the even thread
    }
}
```

### Implementing the Even Number Task

```rust
async fn even_numbers(counter: Arc<Mutex<i32>>, notify_odd: Arc<Notify>, notify_even: Arc<Notify>, max_num: i32) {
    loop {
        notify_even.notified().await; // Wait until notified
        let mut num = counter.lock().unwrap(); // Acquire lock on the counter
        if *num > max_num { // Stop condition
            notify_odd.notify_one(); // Ensure odd thread exits
            break;
        }
        println!("Even Thread: {}", *num); // Print even number
        *num += 1; // Increment counter
        notify_odd.notify_one(); // Notify the odd thread
    }
}
```

## Key Tokio Concepts in Depth

### `tokio::sync::Notify`

Tokio’s `Notify` is a primitive for task wake-ups. Unlike traditional mutex-based synchronization mechanisms, `Notify` allows efficient signaling without blocking threads.

- **`notify_one()`**: Wakes up one waiting task. If no task is waiting, the notification is stored until a task requests it.
    
- **`notified().await`**: Suspends the task until a notification is received.
    

This allows lightweight, non-blocking coordination between asynchronous tasks.

### `tokio::task::spawn`

Tokio’s `spawn` function creates an asynchronous task that runs concurrently with other tasks:

```rust
tokio::task::spawn(async move { ... })
```

It allows executing concurrent work without blocking the main thread.

### `tokio::join!`

The `join!` macro runs multiple asynchronous tasks concurrently and waits for all of them to complete:

```rust
let _ = tokio::join!(task1, task2);
```

This ensures that our odd and even threads run together, rather than sequentially.

## Conclusion

In this article, we explored how Tokio enables efficient thread synchronization and task coordination. By using `Notify`, `spawn`, and `join!`, we implemented an elegant solution that prints numbers in an alternating fashion without unnecessary blocking.

Now, our implementation allows users to specify the maximum number via command-line arguments, making it more flexible. Happy coding with Tokio! 🚀