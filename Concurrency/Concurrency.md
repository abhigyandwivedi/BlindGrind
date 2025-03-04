# Printing Natural Numbers Using Goroutines in Go

## Introduction

This Go program prints natural numbers from `1` to `20` using two goroutines. One goroutine prints odd numbers, and the other prints even numbers. Synchronization is managed using a `channel` to ensure numbers are printed in the correct order without deadlocks.

## Code Implementation

```go
package main

import (
    "fmt"
    "sync"
)

func printOdd(oddCh, evenCh chan struct{}, wg *sync.WaitGroup) {
    defer wg.Done()
    for i := 1; i <= 19; i += 2 {
        <-oddCh
        fmt.Println(i)
        evenCh <- struct{}{}
    }
}

func printEven(oddCh, evenCh chan struct{}, wg *sync.WaitGroup) {
    defer wg.Done()
    for i := 2; i <= 20; i += 2 {
        <-evenCh
        fmt.Println(i)
        if i != 20 {
            oddCh <- struct{}{}
        }
    }
}

func main() {
    oddCh := make(chan struct{})
    evenCh := make(chan struct{})
    var wg sync.WaitGroup

    wg.Add(2)
    go printOdd(oddCh, evenCh, &wg)
    go printEven(oddCh, evenCh, &wg)

    oddCh <- struct{}{} // Start the sequence with the odd number goroutine
    wg.Wait()
}
```

## Explanation

1. **Channels for Synchronization:**
    
    - Two channels, `oddCh` and `evenCh`, are used to alternate execution between the two goroutines.
    - The `oddCh` channel starts the sequence by sending a signal first.
2. **Goroutines:**
    
    - `printOdd`: Waits for a signal from `oddCh`, prints an odd number, then signals `evenCh`.
    - `printEven`: Waits for a signal from `evenCh`, prints an even number, then signals `oddCh` **only if `i != 20`**.
3. **WaitGroup:**
    
    - Ensures both goroutines complete before exiting `main`.
4. **Deadlock Prevention:**
    
    - Unlike previous versions, this approach prevents a deadlock by ensuring the last signal isn't sent unnecessarily.

## Output

```
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
```

This version ensures correct alternating printing of numbers using goroutines and channels while avoiding deadlocks.



 # Without using channels
 
```go
package main

import (
    "fmt"
    "sync"
)

var (
    cond  = sync.NewCond(&sync.Mutex{})
    number = 1
    maxNum = 10
    isOdd  = true
)

func printOdd() {
    for number <= maxNum {
        cond.L.Lock()
        for !isOdd {
            cond.Wait()
        }
        if number <= maxNum {
            fmt.Println("Odd:", number)
            number++
            isOdd = false
        }
        cond.L.Unlock()
        cond.Signal()
    }
}

func printEven() {
    for number <= maxNum {
        cond.L.Lock()
        for isOdd {
            cond.Wait()
        }
        if number <= maxNum {
            fmt.Println("Even:", number)
            number++
            isOdd = true
        }
        cond.L.Unlock()
        cond.Signal()
    }
}

func main() {
    var wg sync.WaitGroup
    wg.Add(2)

    go func() {
        defer wg.Done()
        printOdd()
    }()

    go func() {
        defer wg.Done()
        printEven()
    }()

    wg.Wait()
}
```