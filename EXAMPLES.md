# This is where I put the example and code snippets from what I learned in Rustlings exercises.

### 00. Intro
```rust
fn main() {
    let greeting = "Hello, world!";
    println!("Hello, world!"); // prints Hello, world! to the console and adds a newline
    print!("Greeting: {}", greeting); // prints Greeting: Hello, world!
}
```

### 01. Variables
```rust
fn main() {
    let mut money = 10; // this is mutable (can be changed)
    println!("Current money: {}", money);
    money = 20;
    println!("Money now: {}", money);

    let money = money + 5; // shadowing the previous variable
    println!("After shadowing, money: {}", money);

    let id = 100; // immutable variable
    // id = 200; // this would cause a compile-time error

    const MAX_POINTS: u32 = 100_000; // constant with type annotation
    println!("Max points: {}", MAX_POINTS);
}
```

### 02. Functions
```rust
// This function takes two parameters and returns their difference
fn subtraction(a: i32, b: i32) -> i32 {
    a - b 
}

fn main() {
    let num1: i32 = 10;
    let num2: i32 = 5;
    let number: i32 = subtraction(num1, num2); // calling the function
    println!("{} - {} = {}", num1, num2, number);
}
```

### 03. If
```rust
fn verification(password: &str) -> &str {
    // First, determine the value of passwords based on the input password
    let passwords: i32 = if password == "rustisawesome" {
        0
    } else if password == "ihaterust" {
        1
    } else if password == "iloverust" {
        2
    } else {
        3
    };

    // Now use the value of passwords to determine the response
    if passwords == 0 {
        "Indeed it is, go ahead and enjoy your time here, new Rustacean"
    } else if password == 1 {
        "How dare you?"
    } else if password == 2 {
        "Really?"
    } else {
        "What?"
    }
}

fn main() {
    // Test the verification function with a sample password
    let entered_password: &str = "rustisawesome";
    let response: &str = verification(entered_password);
    println!("Password is: {}", response);
}
```

04. Primitive Types
```rust
fn main() {
    // Boolean example
    let rustisawesome: bool = true;
    if rustisawesome {
        println!("Heck Yeah!");
    }

    // Char example
    let chars = 'H';
    if chars.is_alphabetic() {
        println!("Alphabetical");
    } else {
        println!("It's not Alphabetical");
    }

    // Array and slices example
    let arr = "Once upon a midnight dreary, while I pondered, weak and weary, Over many a quaint and curious volume of forgotten lore— While I nodded, nearly napping, suddenly there came a tapping, As of some one gently rapping, rapping at my chamber door. “’Tis some visitor,” I muttered, “tapping at my chamber door— Only this and nothing more.”";
    if arr.len() >= 100 {
        println!("Yawn...")
    } else {
        println!("It's too short for me to care.")
    }

    let cake = [1, 2, 3, 4];
    let slice = &cake[0..4];
    assert_eq!([1, 2, 3, 4], slice);


    // Tuple example and how to access it
    let tuple = ("The year", 1999);
    print!("{} is {}", tuple.0, tuple.1);

}
```