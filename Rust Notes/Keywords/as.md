# as 
	perform primitive casting, disambiguate the specific trait containing an item, or rename items in `use` statements

# Rust "as" Keyword Examples

The `as` keyword in Rust is used for type casting (converting one type to another). Here are some examples of how it's used:

rust

```rust
fn main() {
    // Numeric type casting
    let x = 5;
    let y = x as f64;  // Convert integer to floating point
    println!("x: {}, y: {}", x, y);  // x: 5, y: 5.0
    
    // Truncating cast (larger integer to smaller)
    let large_number = 300;
    let small_number = large_number as u8;  // u8 can only hold values 0-255
    println!("large: {}, small: {}", large_number, small_number);  // large: 300, small: 44 (truncated)
    
    // Character to integer
    let letter = 'A';
    let letter_code = letter as u32;
    println!("'{}' has ASCII/Unicode value: {}", letter, letter_code);  // 'A' has ASCII/Unicode value: 65
    
    // Boolean to integer
    let flag = true;
    let flag_int = flag as i32;
    println!("flag as integer: {}", flag_int);  // flag as integer: 1
    
    // Reference to pointer (for FFI)
    let value = 42;
    let ptr = &value as *const i32;
    println!("Pointer address: {:?}", ptr);
}
```

The `as` keyword is also used in other contexts:

## In import statements for renaming:

rust

```rust
use std::io::Error as IoError;

fn some_function() -> Result<(), IoError> {
    // Using the renamed IoError
    Ok(())
}
```

## In pattern matching for binding matched values:

rust

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
}

fn process_message(msg: Message) {
    match msg {
        Message::Quit => println!("Quitting"),
        Message::Move { x, y } as movement => {
            println!("Movement details: {:?}", movement);
            println!("Moving to x: {}, y: {}", x, y);
        }
    }
}
```