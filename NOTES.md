# 📝 Learning Notes

## 00. Intro
- Rust uses `print!` and `println!` macros for console output
- `println!` automatically adds a newline at the end
- Use `{}` as placeholders for formatting values

## 01. Variables
- Variables are immutable by default in Rust
- Use `let` to declare a variable
- Add `mut` keyword to make a variable mutable: `let mut x = 5;`
- Can shadow variables by re-declaring with `let`
- Constants use `const` and must have a type annotation

## 02. Functions
- Functions are defined with `fn` keyword
- Use snake_case for function names
- Parameters must have type annotations: `fn add(x: i32, y: i32)`
- Return type specified with `->`: `fn add(x: i32, y: i32) -> i32`
- Last expression (without semicolon) is the return value
- Use `return` keyword for early returns

## 03. If
- Conditional statements use `if`, `else if`, and `else`
- Conditions must evaluate to a boolean (`true` or `false`)
- Can assign the result of an `if` expression to a variable

## 04. Primitive Types
- Booleans (`bool`): `true` or `false`, used in conditionals
- Characters (`char`): single quotes `'C'`, `'😉'`, has methods like `.is_alphabetic()`
- Arrays & slices: fixed size, slice syntax `&a[1..4]` (end exclusive)
- Tuples: multiple types `("name", 3.5)`, access with `tuple.0`, `tuple.1`

## 05. Vecs
- Vectors (`Vec<T>`): growable arrays, create with `vec![1, 2, 3]` macro
- Unlike arrays, vectors can change size at runtime
- Add elements with `.push()`, create empty with `Vec::new()`
- Loop through slice `&[i32]` thwi `for &element in input`
- Iterator pattern: `.iter().map(|x| x * 2).collect()` transforms elements

## 06. Move Semantics
- Ownership: Each value has a single owner; when owner goes out of scope, value is dropped
- Move: Passing a value to a function transfers ownership (moves it) by default
- Mutability: Parameters can be `mut` to allow modification: `fn fill_vec(mut vec: Vec<i32>)`
- Clone: Use `.clone()` to create a copy and keep the original accessible
- Borrowing: Mutable borrows (`&mut`) must be used one at a time, no overlapping borrows
- References vs Ownership: Use `&String` to borrow without taking ownership; use `String` to take ownership
- Key concepts: choosing between borrowing (`&T`) and ownership transfer depending on whether the function needs to consume the value

## 07. Structs
- Defined classic, tuple, and unit structs in [exercises/07_structs/structs1.rs](exercises/07_structs/structs1.rs)
- Instantiated each kind; accessed named fields (like `.red`) and tuple indices (`.0`, `.1`, `.2`); formatted a unit struct with `{:?}`
- Used struct update syntax (`..template`) in [exercises/07_structs/structs2.rs](exercises/07_structs/structs2.rs) to build a new `Order` from a template while overriding `name` and `count`
- Implemented methods and an associated constructor in [exercises/07_structs/structs3.rs](exercises/07_structs/structs3.rs): `is_international()` comparing countries, and `get_fees()` multiplying `cents_per_gram * weight_in_grams`
- Practiced method receivers with `&self`

## 08. Enums
- Defined basic enum with unit variants in [exercises/08_enums/enums1.rs](exercises/08_enums/enums1.rs)
- Enums can have different variant types in [exercises/08_enums/enums2.rs](exercises/08_enums/enums2.rs):
  - Unit variants: `Quit` (no data)
  - Tuple variants: `Move(Point)`, `Echo(String)` (unnamed fields)
  - Struct-like variants: `Resize { width: u32, height: u32 }` (named fields)
- Pattern matching with `match` in [exercises/08_enums/enums3.rs](exercises/08_enums/enums3.rs):
  - Destructure struct variants: `Message::Resize { width, height } => ...`
  - Extract tuple data: `Message::Move(point) => ...`
  - Handle all variants exhaustively (compiler enforces this)
- Match expressions delegate to appropriate methods based on enum variant
- Enums are powerful for representing data that can be one of several types

## 09. Strings
- Two main string types: `String` (owned, heap-allocated) and `&str` (string slice, borrowed)
- Converting `&str` to `String` in [exercises/09_strings/strings1.rs](exercises/09_strings/strings1.rs): `.to_string()` method
- Converting `String` to `&str` in [exercises/09_strings/strings2.rs](exercises/09_strings/strings2.rs): use `&` to borrow
- String methods in [exercises/09_strings/strings3.rs](exercises/09_strings/strings3.rs):
  - `.trim()` removes whitespace from both ends, returns `&str`
  - `format!("{} world!", input)` concatenates strings, returns `String`
  - `.replace("old", "new")` replaces substrings, returns new `String`
- Multiple ways to create `String` in [exercises/09_strings/strings4.rs](exercises/09_strings/strings4.rs):
  - `.to_string()` - converts to owned String
  - `String::from()` - creates String from literal
  - `.to_owned()` - clones into owned String
  - `.into()` - type conversion (requires type inference)
  - `format!()` - string interpolation
- String slicing `&String[0..1]` returns `&str` (byte indexing, not character indexing)
- Methods like `.trim()`, `.replace()`, `.to_lowercase()` return different types based on whether they modify

## 10. Modules
- Visibility and public API in [exercises/10_modules/modules1.rs](exercises/10_modules/modules1.rs): made `get_secret_recipe()` private and exposed `make_sausage()` with `pub`, then called `sausage_factory::make_sausage()` from `main`.
- Aliases and re-exports in [exercises/10_modules/modules2.rs](exercises/10_modules/modules2.rs): used `pub use` with `as` to re-export `fruits::PEAR` and `veggies::CUCUMBER` as `fruit` and `veggie`, so consumers can access `delicious_snacks::fruit` and `delicious_snacks::veggie`.
- Scoped imports in one line in [exercises/10_modules/modules3.rs](exercises/10_modules/modules3.rs): brought `SystemTime` and `UNIX_EPOCH` from `std::time` into scope with `use std::{time::SystemTime, time::UNIX_EPOCH};` and printed seconds since the Unix epoch.

## 11. Hashmaps
- HashMaps store key-value pairs with fast lookup: `HashMap<K, V>`
- Created HashMap with `HashMap::new()` in [exercises/11_hashmaps/hashmaps1.rs](exercises/11_hashmaps/hashmaps1.rs): used `.insert()` to add `String` keys and `u32` values
- Entry API in [exercises/11_hashmaps/hashmaps2.rs](exercises/11_hashmaps/hashmaps2.rs): `.entry(key).or_insert(value)` inserts only if key doesn't exist, preventing overwrites
- Custom structs as values in [exercises/11_hashmaps/hashmaps3.rs](exercises/11_hashmaps/hashmaps3.rs): `.entry(key).or_default()` creates entry with `Default` trait, then mutate the returned reference
- Applied to soccer scores: tracked goals scored and conceded per team across multiple matches

## 12. Options
- `Option<T>` represents optional values: `Some(value)` or `None` (replaces null)
- Returning Options in [exercises/12_options/options1.rs](exercises/12_options/options1.rs): return `Some(T)` when value exists, `None` otherwise; extract with `.unwrap_or(default)`
- Pattern matching in [exercises/12_options/options2.rs](exercises/12_options/options2.rs): `if let Some(value) = optional` for single case, `while let Some(Some(value))` for nested Options
- Borrowing in [exercises/12_options/options3.rs](exercises/12_options/options3.rs): use `Some(ref p)` to borrow instead of moving the value out of Option

## 13. Error Handling
- `Result<T, E>` represents operations that can succeed or fail: `Ok(value)` for success, `Err(error)` for failure
- Converting from Option to Result in [exercises/13_error_handling/errors1.rs](exercises/13_error_handling/errors1.rs): changed `Option<String>` to `Result<String, String>`, replacing `None` with `Err(message)` and `Some(value)` with `Ok(value)`
- The `?` operator in [exercises/13_error_handling/errors2.rs](exercises/13_error_handling/errors2.rs): propagates errors automatically; `parse::<i32>()?` returns early with `Err` if parsing fails, otherwise unwraps the `Ok` value
- Propagating errors in main in [exercises/13_error_handling/errors3.rs](exercises/13_error_handling/errors3.rs): changed `main()` to `main() -> Result<(), ParseIntError>` and added `Ok(())` at the end to allow using `?` operator
- Custom error types in [exercises/13_error_handling/errors4.rs](exercises/13_error_handling/errors4.rs): defined `CreationError` enum with `Negative` and `Zero` variants, used pattern matching to return appropriate error type
- Trait objects with `Box<dyn Error>` in [exercises/13_error_handling/errors5.rs](exercises/13_error_handling/errors5.rs): allows handling multiple error types by implementing the `Error` trait; `Box<dyn Error>` acts as a catch-all for any error type
- Composing custom errors in [exercises/13_error_handling/errors6.rs](exercises/13_error_handling/errors6.rs): created `ParseIntError`; used `.map_err()` to convert error types when propagating with `?`

## 14. Generics
- Defined generic vector `Vec<T>` in [exercises/14_generics/generics1.rs](exercises/14_generics/generics1.rs): explicit type annotation `Vec<i32>` needed when compiler cannot infer type from usage
- Generic structs and implementations in [exercises/14_generics/generics2.rs](exercises/14_generics/generics2.rs): defined `struct Wrapper<T>` to hold any type, and `impl<T> Wrapper<T>` to define methods for that generic type

## 15. Traits
- Implementing traits in [exercises/15_traits/traits1.rs](exercises/15_traits/traits1.rs): defined behavior using `impl Trait for Type`, adding method `append_bar` to `String`
- Trait implementations for generics in [exercises/15_traits/traits2.rs](exercises/15_traits/traits2.rs): implemented the trait for `Vec<String>`, demonstrating how to extend standard collection types
- Default implementations in [exercises/15_traits/traits3.rs](exercises/15_traits/traits3.rs): defined a default body for `licensing_info` in the trait so implementors share common behavior automatically
- Trait bounds with `impl Trait` in [exercises/15_traits/traits4.rs](exercises/15_traits/traits4.rs): used `fn func(arg: impl Trait)` to accept any type that implements a trait, enabling polymorphism
- Multiple trait bounds in [exercises/15_traits/traits5.rs](exercises/15_traits/traits5.rs): used `+` syntax (`impl Trait1 + Trait2`) to specify that a parameter must implement multiple traits

## 16. Lifetimes
- Lifetime annotations (`'a`) help the compiler ensure references are valid (prevent dangling pointers)
- Annotated function signatures in [exercises/16_lifetimes/lifetimes1.rs](exercises/16_lifetimes/lifetimes1.rs): `fn longest<'a>(x: &'a str, y: &'a str) -> &'a str` links output lifetime to inputs
- Fixed scope issues in [exercises/16_lifetimes/lifetimes2.rs](exercises/16_lifetimes/lifetimes2.rs): ensured data outlives its references by moving variable declaration to a wider scope
- Annotated structs in [exercises/16_lifetimes/lifetimes3.rs](exercises/16_lifetimes/lifetimes3.rs): defined `struct Book<'a>` to enforce that referenced fields (`author`, `title`) live at least as long as the struct

## 17. Tests
- Defined unit tests in a dedicated module with `#[cfg(test)]` annotation
- Imported parent module functions using `use super::*` to access code being tested
- Used `assert!(expression)` to verify boolean conditions in [exercises/17_tests/tests1.rs](exercises/17_tests/tests1.rs)
- Used `assert_eq!(left, right)` to verify equality between values in [exercises/17_tests/tests2.rs](exercises/17_tests/tests2.rs)
- Used `#[should_panic]` attribute to test that specific code paths (like invalid input) correctly panic in [exercises/17_tests/tests3.rs](exercises/17_tests/tests3.rs)

## 18. Iterators
- **Transformation & Collection**:
  - `.iter()` creates an iterator from a collection.
  - `.map()` transforms items lazily.
  - `.collect()` consumes the iterator. It can infer the return type:
    - `.collect::<Vec<_>>()`: Creates a list of results.
    - `.collect::<String>()`: Joins iterator results into a single string.
- **Handling Errors with Result**:
  - `collect()` behavior changes based on return type:
    - `Result<Vec<T>, E>`: Stops at the first error (fails fast).
    - `Vec<Result<T, E>>`: Collects all results, including success and errors.
- **Reduction**:
  - `.fold(init, op)`: Accumulates a single value from the iterator, starting with an initial value.
  - `.product()`: Specialized method to multiply all elements (concise alternative to `fold` for factorials).
  - Ranges `(1..=num)` can be used to generate sequences easily.
- **Filtering & Flattening**:
  - `.filter()`: Keeps only items matching a predicate.
  - `.values()`: Gets the values from a HashMap.
  - `.flat_map()`: Maps each element to an iterator and then flattens the nested structure (e.g., extracting values from a list of HashMaps into a single stream).
  - `.count()`: Consumes the iterator to count the remaining elements.

## 19. Smart Pointers
- **Box (`Box<T>`)**:
  - Allocates values on the heap instead of the stack.
  - **Recursive Types**: Necessary for defining types like linked lists (Cons list) where a type contains itself. Without `Box`, the size would be infinite/unknown at compile time. `Box` has a known pointer size.
  - **Usage**: `Box::new(value)` moves the value to the heap.
- **Rc (`Rc<T>`)**:
  - Reference Counted smart pointer.
  - **Multiple Ownership**: Allows multiple parts of your program to own the same data simultaneously (e.g., a "Sun" owned by multiple "Planets").
  - **Single-threaded**: ONLY for use in single-threaded scenarios. It is faster than `Arc` because it doesn't need atomic operations.
  - **Cloning**: `Rc::clone(&rc)` increments the reference count. Usually cheap (increments an integer), does not deep-copy the data.
- **Arc (`Arc<T>`)**:
  - Atomic Reference Counted.
  - **Thread-safe**: Same mechanism as `Rc` but uses atomic operations for the counter, making it safe to share across threads.
  - **Shared Ownership**: Used when multiple threads need access to the same read-only data.
  - **Usage**: `Arc::clone(&arc)` creates a new handle for another thread.
- **Cow (`Cow<T>`)**:
  - "Clone on Write".
  - **Optimization**: A smart enum that can hold either *borrowed* data (`&T`) or *owned* data (`T`).
  - **Lazy Cloning**: It keeps data borrowed (cheap) as long as you only read it. It only clones (expensive) if you try to mutate it (`.to_mut()`).
  - Useful for functions that verify data and only occasionally need to modify it.

## 20. Threads
- **Spawning**: `thread::spawn(move || { ... })` creates a new thread along with a closure containing the code to run.
  - The `move` keyword is often required to transfer ownership of variables into the thread's closure.
- **Join Handles**: `spawn` returns a `JoinHandle`.
  - Calling `.join()` blocks the current thread until the spawned thread finishes.
  - `.join()` returns a `Result`, allowing you to retrieve the value returned by the thread (or handle panics).
- **Shared Mutable State**:
  - **Arc (`Arc<T>`)**: Atomic Reference Counting. Used to share ownership of data across multiple threads.
  - **Mutex (`Mutex<T>`)**: Mutual Exclusion. Used to allow mutable access to shared data.
  - **Arc<Mutex<T>>**: The standard pattern for shared mutable state.
  - **Locking**: Call `.lock()` on the Mutex to get access to the inner data. This blocks until the lock is acquired. It returns a `MutexGuard` (wrapped in a Result) which automatically releases the lock when it goes out of scope.
- **Channels**:
  - `mpsc` (Multi-Producer, Single-Consumer) allows threads to communicate by sending messages.
  - `mpsc::channel()` returns a `(Sender, Receiver)` tuple.
  - **Cloning Senders**: To have multiple threads send to the same channel, you must `.clone()` the sender (`tx`).
  - **Ownership**: Be careful about moving data (like struct fields) into threads. You may need to destructure structs or clone specific parts *before* spawning threads to ensure each thread gets the ownership it needs.

## 21. Macros
- **Definition**: Defined using `macro_rules!` followed by the name and a block.
  - Unlike functions, macros end with `!`.
- **Matching**: Macros use a pattern matching syntax similar to `match` expressions.
  - `(patterns) => { code }`
  - Arguments are prefixed with `$` (e.g., `$val:expr` matches an expression and binds it to `$val`).
- **Scoping**:
  - Macros are lexically scoped; they must be defined *before* they are called in the file.
  - To use macros from a nested module, use `#[macro_use]` on the module declaration.
- **Arms**: Macros can have multiple "arms" to handle different arguments, separated by semicolons `;`.

---

## Quiz 1
- Wrote function with `u32` params and return type
- Applied bulk discount logic: if qty > 40 then 1 rustbuck/apple, else 2 rustbucks/apple
- Used `if/else` expression as return value (no semicolon needed)

## Quiz 2
- Built a string transformer function taking `Vec<(String, Command)>` input
- Defined enum with three variants: `Uppercase`, `Trim`, and `Append(usize)` (tuple variant)
- Used pattern matching to handle each command:
  - `Uppercase`: called `.to_uppercase()` to convert string to uppercase
  - `Trim`: called `.trim().to_string()` to remove whitespace and return owned String
  - `Append(n)`: looped `n` times pushing "bar" to a mutable string
- Imported function from module with `use crate::my_module::transformer`
- Combined concepts: enums, match expressions, vectors, string methods, modules, and move semantics

## Quiz 3
- Refactored `ReportCard` struct to support multiple grade types using generics
- Changed `grade: f32` to `grade: T` in the struct definition
- Updated `impl` block to generic implementation `impl<T: std::fmt::Display>`
- Used the `Display` trait bound to ensure the generic grade can be printed with `{}` inside `format!`
- Enabled polymorphism: `ReportCard` can now accept `f32` (numeric) or `String`/`&str` (alphabetic) grades while sharing the same printing logic