# RUST

## INFO

* Rust is an **ahead-of-time** compiled language, meaning you can compile a program and give the executable to someone else, and they can run it even without having Rust installed. 
* Rust has a strong, static type system. Rust is a statically typed language, which means that it must know the types of all variables at compile time. The compiler can usually infer what type we want to use based on the value and how we use it.
* In Rust, variables are immutable by default.
* Rust defaults to an i32 if the type of the number variable is not specified.
* The default type is f64 if the value.
* Rust’s char type is four bytes in size and represents a Unicode Scalar Value, which means it can represent a lot more than just ASCII. Accented letters; Chinese, Japanese, and Korean characters; emoji; and zero-width spaces are all valid char values in Rust. Unicode Scalar Values range from U+0000 to U+D7FF and U+E000 to U+10FFFF inclusive. However, a “character” isn’t really a concept in Unicode, so your human intuition for what a “character” is may not match up with what a char is in Rust.
* Rust code uses snake case as the conventional style for function and variable names, in which all letters are lowercase and underscores separate words.
* Ownership: Ownership is a set of rules that governs how a Rust program manages memory. All programs have to manage the way they use a computer’s memory while running.  In order to support a mutable, growable piece of value, we need to allocate an amount of memory on the heap, unknown at compile time, to hold the contents. 
    - Some languages have garbage collection that constantly looks for no-longer used memory as the program runs; 
    - in other languages, the programmer must explicitly allocate and free the memory. 
    - Rust uses a third approach: memory is managed through a system of ownership with a set of rules that the compiler checks. If any of the rules are violated, the program won’t compile. None of the features of ownership will slow down your program while it’s running.
**Ownership rules:**
    - Each value in Rust has a variable that’s called its owner.
    - There can only be one owner at a time.
    - When the owner goes out of scope, the value will be dropped.
Rust will never automatically create “deep” copies of your data. Therefore, any automatic copying can be assumed to be inexpensive in terms of runtime performance. The ownership of the heap data is moved to the assigned variable and previous variable is invalidated by Rust. To do a deep copy, then use clone method. When you see a call to clone, you know that some arbitrary code is being executed and that code may be expensive. It’s a visual indicator that something different is going on.
Types such as integers that have a known size at compile time are stored entirely on the stack, so copies of the actual values are quick to make.

**The ownership of a variable follows the same pattern every time: assigning a value to another variable moves it. When a variable that includes data on the heap goes out of scope, the value will be cleaned up by drop unless ownership of the data has been moved to another variable.**
Rust has a feature for using a value without transferring ownership, called references (referencing/dereferencing).

Types such as integers that have a known size at compile time are stored entirely on the stack, so copies of the actual values are quick to make. So when you assing from one variable to the other the variable doesn't get invalid after assignment.Complier just clones the content.
Rust has a special annotation called the **Copy trait** that we can place on types that are stored on the stack like integers are (we’ll talk more about traits in Chapter 10). If a type implements the Copy trait, a variable is still valid after assignment to another variable. Rust won’t let us annotate a type with Copy if the type, or any of its parts, has implemented the **Drop trait**.
As a general rule, any group of simple scalar values can implement Copy, and nothing that requires allocation or is some form of resource can implement Copy.

* Mutable references have one big restriction: you can have only one mutable reference to a particular piece of data at a time.
* The concepts of ownership, borrowing, and slices ensure memory safety in Rust programs at compile time.

## Terminology

* Rustaceans: Rust developer
* Package:
* Crate: packages of code are referred to as crates. Crate is a collection of Rust source code files. The project we’ve been building is a binary crate, which is an executable. The rand crate is a library crate, which contains code intended to be used in other programs, and can’t be executed on its own.
* Prelude: By default, Rust has a few items defined in the standard library that it brings into the scope of every program. This set is called the prelude, and you can see everything in it in the standard library documentation (https://doc.rust-lang.org/std/prelude/index.html). You need to use 'use' statement to bring in the feature which is not in the prelude.
* Crates.io: Crates.io is where people in the Rust ecosystem post their open source Rust projects for others to use.
* Mutable variable: by using 'mut' keyword
* Growable variable: e.g. String in the prelude
* Associated function: An associated function is a function that’s implemented on a type (e.g. ::new())
* References: Using a variable starting with '&'. They are immutable by default.
* Enumerations: types Often referred to as enums, which can have a fixed set of possibilities known as variants.
* Traits: 
* Shadowing: Lets us reuse a variable name rather than forcing us to create two unique variables, such as my_variable_str and my_variable for example. Shadowing vs mutable: Shadowing creates new variable with same name. But if we use 'mut', we can't change its type.
* Binding: Assigning to a variable
* Panicking: Rust uses the term panicking when a program exits with an error. 
* Two’s complement wrapping:  While compiling in release mode, program doesn't panic if an integer overflow happens. Rust does not include checks for integer overflow that cause panics. Instead, if overflow occurs, Rust performs two’s complement wrapping. In short, values greater than the maximum value the type can hold “wrap around” to the minimum of the values the type can hold. In the case of a u8, the value 256 becomes 0, the value 257 becomes 1, and so on. The program won’t panic, but the variable will have a value that probably isn’t what you were expecting it to have. Relying on integer overflow’s wrapping behavior is considered an error.
* Destructing: To get the individual values out of a tuple, we can use pattern matching to destructure a tuple value like:
```    
    let tup = (500, 6.4, 1);
    let (x, y, z) = tup;
```
* unit type, un,t value: The tuple without any values, (), is a special type that has only one value, also written (). The type is called the unit type and the value is called the unit value. Expressions implicitly return the unit value if they don’t return any other value.
* Statements: are instructions that perform some action and do not return a value. Statements don’t evaluate to a value, which is expressed by (), the unit type.
* Expressions: Expressions evaluate to a resulting value. So they can be assıgned(/bound) to a variable. Calling a function is an expression. Calling a macro is an expression. A new scope block created with curly brackets is an expression. **NOTE THAT:** If you add a semicolon to the end of an expression, you turn it into a statement, and it will then not return a value. e.g.:
```
let number = if condition { 5 } else { 6 };
```
* Arms: If expressions are sometimes called arms, just like the arms in match expressions.
* Loop label: You can label loops to use with break and continue keywords. The format is '<label name>. e.g.: 'outer_loop
* Data race: A data race is similar to a race condition and happens when these three behaviors occur:
    - Two or more pointers access the same data at the same time.
    - At least one of the pointers is being used to write to the data.
    - There’s no mechanism being used to synchronize access to the data.
Data races cause undefined behavior and can be difficult to diagnose and fix when you’re trying to track them down at runtime; Rust prevents this problem by refusing to compile code with data races!
Rust enforces a similar rule for combining mutable and immutable references. 
* Non-Lexical Lifetimes (NLL): A reference’s scope starts from where it is introduced and continues through the last time that reference is used. So this code is permitted by the compiler:
    ```
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    println!("{} and {}", r1, r2);
    // variables r1 and r2 will not be used after this point

    let r3 = &mut s; // no problem
    println!("{}", r3);
    ```
* Dangling references: In Rust, the compiler guarantees that references will never be dangling references: if you have a reference to some data, the compiler will ensure that the data will not go out of scope before the reference to the data does.
* Slices: let you reference a contiguous sequence of elements in a collection rather than the whole collection. A slice is a kind of reference, so it does not have ownership. Solves the empties memory
  String slices: A string slice is a reference to part of a String, and it looks like this:
```
    let s = String::from("hello world");

    let hello = &s[0..5];
    let world = &s[6..11];
```
The type that signifies “string slice” is written as &str.
```
    fn first_word(s: &String) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }

    &s[..]
}
```
Note: String slice range indices must occur at valid UTF-8 character boundaries. If you attempt to create a string slice in the middle of a multibyte character, your program will exit with an error.
* struct update syntax: The syntax .. specifies that the remaining fields not explicitly set should have the same value as the fields in the given instance.
```
fn main() {
    // --snip--

    let user2 = User {
        email: String::from("another@example.com"),
        ..user1
    };
}
```
Note that the struct update syntax uses = like an assignment; this is because it moves the data.
    
## Types

### Scalar Types: 

* Rust has four primary scalar types: integers, floating-point numbers, Booleans, and characters.
* Signed numbers are stored using two’s complement representation.
* In debug build, compiler adds code to crash if there is an integer overflow happens. However, while compiling in release mode, program doesn't panic. Rust does not include checks for integer overflow that cause panics. Instead, if overflow occurs, Rust performs two’s complement wrapping. In short, values greater than the maximum value the type can hold “wrap around” to the minimum of the values the type can hold. In the case of a u8, the value 256 becomes 0, the value 257 becomes 1, and so on. The program won’t panic, but the variable will have a value that probably isn’t what you were expecting it to have. Relying on integer overflow’s wrapping behavior is considered an error.
* Rust will not automatically try to convert non-Boolean types to a Boolean.

### Compound Types:

#### Tuples

The tuple without any values, (), is a special type that has only one value, also written (). The type is called the unit type and the value is called the unit value. Expressions implicitly return the unit value if they don’t return any other value.    

```
let tup: (i32, f64, u8) = (500, 6.4, 1);
let first_index_value = x.0;
let second_index_value = x.1;    
```
You can destruct tuple content:
````
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {}", y);
    
This program first creates a tuple and binds it to the variable tup. It then uses a pattern with let to take tup and turn it into three separate variables, x, y, and z. This is called destructuring, because it breaks the single tuple into three parts. 
    
#### The Array Type
    Unlike a tuple, every element of an array must have the same type. Unlike arrays in some other languages, arrays in Rust have a fixed length.
```
    let a = [1, 2, 3, 4, 5];
    let b: [i32; 5] = [1, 2, 3, 4, 5];
    let a = [3; 5];  // 5 elements with same value 3

```    
Arrays are useful when you want your data allocated on the stack rather than the heap or when you want to ensure you always have a fixed number of elements.
    
#### Structs

1. Normal struct:
    
* structs are unmutable by default. Note that the entire instance must be mutable; Rust doesn’t allow us to mark only certain fields as mutable.
* struct update syntax: The syntax .. specifies that the remaining fields not explicitly set should have the same value as the fields in the given instance.
```
fn main() {
    // --snip--

    let user2 = User {
        email: String::from("another@example.com"),
        ..user1
    };
}
```
Note that the struct update syntax uses = like an assignment; this is because it moves the data.

2. Tuple struct:

Rust also supports structs that look similar to tuples, called tuple structs. Tuple structs have the added meaning the struct name provides but don’t have names associated with their fields; rather, they just have the types of the fields. Tuple structs are useful when you want to give the whole tuple a name and make the tuple a different type from other tuples, and when naming each field as in a regular struct would be verbose or redundant.

3. Unit-Like structs: 
    
## Tools

* rustup: Check, install updates
* rustc : Compiler
* rustfmt : Code formatter
* cargo: Build system & package manager (such as building your code, downloading the libraries your code depends on, and building those libraries.)
** Ref: https://doc.rust-lang.org/cargo/ 
** cargo build (only build), cargo run (build & run), cargo check (check if code is buildable without creating binary), cargo update (updates the versions of depended crates), cargo doc --open (Create documentation for all dependencies and opens in browser)
** TOML: Tom’s Obvious, Minimal Language. Cargo's configuration format. https://toml.io/en/
** Build target profiles: debug, release
** Project structure:
    <Project folder>
    -> Cargo.toml
    -> README.md
    -> src/
        -> rs files
    -> target/debug       (cargo build or cargo run creates for build output) 
    -> target/release     (cargo build --release creates to compile code with optimizations)
    -> Cargo.lock         (When you build a project for the first time, Cargo figures out all the versions of the dependencies that fit the criteria and then writes them to the Cargo.lock file. When you build your project in the future, Cargo will see that the Cargo.lock file exists and use the versions specified there rather than doing all the work of figuring out versions again. This lets you have a reproducible build automatically. In other words, your project will remain at 0.8.3 until you explicitly upgrade, thanks to the Cargo.lock file.)
  
## Best Practices

* It’s good style to place the opening curly bracket on the same line as the function declaration, adding one space in between.
* Run cargo check periodically as they write their program to make sure it compiles.
* Rust’s naming convention for constants is to use all uppercase with underscores between words. 
  
## <SLOGAN> Fearless Concurrency
