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

## Types

# Scalar Types: 

* Rust has four primary scalar types: integers, floating-point numbers, Booleans, and characters.
* Signed numbers are stored using two’s complement representation.
* In debug build, compiler adds code to crash if there is an integer overflow happens. However, while compiling in release mode, program doesn't panic. Rust does not include checks for integer overflow that cause panics. Instead, if overflow occurs, Rust performs two’s complement wrapping. In short, values greater than the maximum value the type can hold “wrap around” to the minimum of the values the type can hold. In the case of a u8, the value 256 becomes 0, the value 257 becomes 1, and so on. The program won’t panic, but the variable will have a value that probably isn’t what you were expecting it to have. Relying on integer overflow’s wrapping behavior is considered an error.
* Rust will not automatically try to convert non-Boolean types to a Boolean.

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
