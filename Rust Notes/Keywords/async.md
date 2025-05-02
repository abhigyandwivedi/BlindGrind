# Rust Async Programming Guide

## Introduction to `async` in Rust

In Rust, the `async` keyword enables asynchronous programming by transforming functions to return `Future`s instead of blocking the current thread. This approach allows your program to make progress on other tasks while waiting for I/O or other operations to complete.

## Core Concepts

### The `async` Keyword

The `async` keyword in Rust:

- Transforms a function, block, or closure into a state machine that implements the `Future` trait
- Changes the function's return type to an anonymous type that implements `Future<Output = T>`, where `T` is your function's declared return type
- Does not execute the function body immediately, but creates a `Future` that must be run on an executor

### Basic Syntax

```rust
// An async function that returns a Future<Output = String>
async fn fetch_data() -> String {
    // Asynchronous code here
    String::from("some data")
}

// Async block expression
let future = async {
    // Asynchronous code here
    "result"
};
```

## Using Async Functions

### Awaiting Futures with `.await`

The `.await` operator suspends execution until the `Future` completes:

```rust
async fn process_data() -> Result<String, Error> {
    let data = fetch_data().await;
    let processed = transform_data(data).await?;
    Ok(processed)
}
```

### Running Futures

Futures are lazy and need an executor to run. Common approaches:

```rust
// Using tokio runtime
#[tokio::main]
async fn main() {
    let result = fetch_data().await;
    println!("Got result: {}", result);
}

// Alternative with block_on
fn main() {
    let result = tokio::runtime::Runtime::new()
        .unwrap()
        .block_on(fetch_data());
    println!("Got result: {}", result);
}
```

## Complete Examples

### Basic HTTP Request

```rust
use reqwest::Error;

async fn fetch_url(url: &str) -> Result<String, Error> {
    let response = reqwest::get(url).await?;
    let body = response.text().await?;
    Ok(body)
}

#[tokio::main]
async fn main() -> Result<(), Error> {
    println!("Fetching data...");
    match fetch_url("https://www.rust-lang.org").await {
        Ok(body) => println!("Body length: {} bytes", body.len()),
        Err(e) => eprintln!("Error: {}", e),
    }
    Ok(())
}
```

### Concurrent Operations

```rust
use futures::future::join_all;
use std::time::Duration;

async fn delayed_hello(name: &str, delay_ms: u64) -> String {
    tokio::time::sleep(Duration::from_millis(delay_ms)).await;
    format!("Hello, {}!", name)
}

#[tokio::main]
async fn main() {
    // Create multiple futures
    let futures = vec![
        delayed_hello("Alice", 100),
        delayed_hello("Bob", 50),
        delayed_hello("Charlie", 200),
    ];
    
    // Run all futures concurrently
    let results = join_all(futures).await;
    
    // Process results
    for result in results {
        println!("{}", result);
    }
}
```

### Error Handling with `?` Operator

```rust
use std::fs::File;
use std::io::{self, Read};
use tokio::fs as async_fs;

// Async function that can return an error
async fn read_file_async(path: &str) -> io::Result<String> {
    let mut file = async_fs::File::open(path).await?;
    let mut contents = String::new();
    let mut buffer = Vec::new();
    let bytes_read = file.read_to_end(&mut buffer).await?;
    
    println!("Read {} bytes", bytes_read);
    String::from_utf8(buffer).map_err(|e| io::Error::new(io::ErrorKind::InvalidData, e))
}

#[tokio::main]
async fn main() -> io::Result<()> {
    let contents = read_file_async("example.txt").await?;
    println!("File contents: {}", contents);
    Ok(())
}
```

### Timeouts and Cancellation

```rust
use tokio::time::{timeout, Duration};
use std::io;

async fn slow_operation() -> String {
    tokio::time::sleep(Duration::from_secs(5)).await;
    "Completed".to_string()
}

#[tokio::main]
async fn main() -> io::Result<()> {
    // Apply a 2-second timeout to our operation
    match timeout(Duration::from_secs(2), slow_operation()).await {
        Ok(result) => println!("Operation result: {}", result),
        Err(_) => println!("Operation timed out"),
    }
    
    Ok(())
}
```

## Advanced Patterns

### Streams with `async`

```rust
use futures::stream::{self, StreamExt};

#[tokio::main]
async fn main() {
    // Create a stream of futures
    let mut stream = stream::iter(1..=5)
        .map(|i| async move {
            tokio::time::sleep(Duration::from_millis(100)).await;
            i * 2
        })
        .buffer_unordered(3); // Process up to 3 items concurrently
    
    // Process stream items as they complete
    while let Some(result) = stream.next().await {
        println!("Result: {}", result);
    }
}
```

### Select with `tokio::select!`

```rust
use tokio::sync::mpsc;
use tokio::time::{sleep, Duration};

#[tokio::main]
async fn main() {
    let (tx, mut rx) = mpsc::channel(10);
    
    // Spawn a task that sends a message after 1 second
    tokio::spawn(async move {
        sleep(Duration::from_secs(1)).await;
        tx.send("Message received").await.unwrap();
    });
    
    tokio::select! {
        // Branch 1: Wait for message
        Some(msg) = rx.recv() => {
            println!("Got message: {}", msg);
        }
        // Branch 2: Timeout after 2 seconds
        _ = sleep(Duration::from_secs(2)) => {
            println!("Timed out waiting for message");
        }
    }
}
```

## Best Practices

1. **Minimize `.await` points** inside critical loops for better performance
2. **Use appropriate executors** (tokio, async-std, etc.) based on your needs
3. **Handle errors properly** with `Result` types and proper propagation
4. **Avoid blocking operations** in async code
5. **Use `?` operator** for cleaner error handling in async functions
6. **Consider using `join` or `join_all`** for concurrent operations
7. **Apply timeouts** to prevent waiting indefinitely

## Common Pitfalls

1. **Forgetting to `.await` a future**
2. **Blocking the executor** with CPU-intensive tasks
3. **Creating too many tasks** which can exhaust system resources
4. **Improper error handling** in async contexts
5. **Not understanding the "Send" requirement** for tasks spawned on thread pools

By mastering Rust's async features, you can write efficient, concurrent code that maximizes resource utilization while maintaining Rust's safety guarantees.