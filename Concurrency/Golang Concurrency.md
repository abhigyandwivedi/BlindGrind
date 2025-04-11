
# Golang Concurrency Patterns

Go has built-in support for concurrency through goroutines and channels. Below are several powerful and idiomatic concurrency patterns worth exploring:

---

## 🔁 1. Fan-Out / Fan-In

**Use case**: Parallel processing and collecting results.

- **Fan-Out**: Multiple goroutines read from the same input channel and process data in parallel.
    
- **Fan-In**: Results from multiple goroutines are sent to a single output channel.
    

```go
// Fan-Out
for i := 0; i < n; i++ {
    go worker(input, output)
}

// Fan-In
go func() {
    for r := range result1 {
        merged <- r
    }
}()
```

---

## 🧱 2. Worker Pool

**Use case**: Limit the number of concurrent goroutines (e.g., API calls or database writes).

```go
jobs := make(chan Job)
results := make(chan Result)

for w := 0; w < numWorkers; w++ {
    go worker(w, jobs, results)
}
```

---

## ⛔ 3. Pipeline

**Use case**: Stream data through a series of processing stages.

```go
c1 := gen()
c2 := sq(c1)
c3 := sq(c2)
```

---

## 🔁 4. Ticker Pattern

**Use case**: Periodic actions (polling, cron-like behavior).

```go
ticker := time.NewTicker(1 * time.Second)
for {
    select {
    case <-ticker.C:
        fmt.Println("Tick")
    }
}
```

---

## ⚙️ 5. Context Cancellation

**Use case**: Graceful shutdown and timeout propagation.

```go
ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
defer cancel()
```

---

## 🕳️ 6. Select Statement for Multiplexing

**Use case**: Wait on multiple channels.

```go
select {
case msg1 := <-ch1:
    fmt.Println(msg1)
case msg2 := <-ch2:
    fmt.Println(msg2)
case <-time.After(1 * time.Second):
    fmt.Println("Timeout")
}
```

---

## 🚪 7. Channel Semaphore

**Use case**: Limit access to a resource (e.g., only N tasks at a time).

```go
sem := make(chan struct{}, maxConcurrent)

sem <- struct{}{} // acquire
go func() {
    defer func() { <-sem }() // release
    doWork()
}()
```

---

## 🔒 8. Singleflight Pattern

**Use case**: Prevent duplicate concurrent calls (e.g., cache stampede).

```go
import "golang.org/x/sync/singleflight"

var g singleflight.Group
val, err, _ := g.Do("key", func() (interface{}, error) {
    return getDataFromDB(), nil
})
```

---

## 👮‍♂️ 9. Mutex and RWMutex

**Use case**: When shared memory cannot be avoided (last resort in Go).

```go
var mu sync.Mutex
mu.Lock()
data := sharedResource
mu.Unlock()
```