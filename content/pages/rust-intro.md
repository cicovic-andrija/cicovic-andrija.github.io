---
title: "Rust Introduction"
date: "2023-02-05T11:39:40Z"
categories: ["software"]
tags: ["rust", "programming", "books", "references"]
draft: false
---

This post is a summary of several chapters from "The Rust Programming Lanuage" book. These notes were
written while I was learning the basics and trying out the language by implementing a parser combinator library called
_[libparse](https://github.com/cicovic-andrija/libparse)_. I eventually managed to write a simple CSV parser for another
project, and in the process I wrote these instruction bullets on how to use the basic features of the language.

This is not a summary of the whole book, but rather the first half, which covers common programming concepts and
idioms of Rust. Later chapters of the book, those describing the concurrency model, low-level programming, and other
advanced topics, are not included here because they deal with more specialized technical areas, require previous
knowledge in these areas, and due to their complexity don't work well with the format I wanted to use. At the time of
writing, the complete book was available for reading on the [Rust website](https://doc.rust-lang.org/stable/book/);
it is an excellent gateway into the Rust ecosystem.

## About Rust

- Compiled, statically typed language.
- Expression-based language.
- Offers strong memory safety guarantees.
- Supports some functional and OOP constructs.
- Strives to provide zero-cost abstractions.
- No concept of null values.

## Common Programming Concepts

- Variables are immutable by default.
- Use the `let` keyword to declare a variable.
- Use the `mut` keyword to specify that the variable is mutable.
- Use the `const` keyword to declare a constant.
- The type of the constant must be annotated.
- Naming convention: constants are usually named like BUFFER_SIZE.
- Use the `let` keyword to declare a variable that shadows an existing variable with the same name.
- Use shadowing to change the type of the value, but reuse the name.
- The type of a variable cannot be changed with assignment (for mutable variables).
- Use the type annotation to specify the type of a variable: `let n: i32 = 42;`.
- Scalar types: integers (2's complement), floating-point numbers (IEEE-754), booleans (`true`/`false`) and characters.
- Primitive compound types: tuples and arrays.
- The `isize` and `usize` integer types represent the native word width on the target architecture.
- Use `isize` or `usize` for indexing of collections.
- Use a type suffix to specify the type of an integer constant: `57u8`.
- Use the underscore as a visual separator: `1_000_000`.
- Character type `char` is 4 bytes long and represents a Unicode Scalar Value (`U+0000-U+D7FF` or `U+E000-U+10FFFF`).
- Use tuples for fix-length, variable-type compound values: `let x: (i32, f64) = (42, 3.14);`.
- Tuples can be destructured, or accessed by using a `.` (period) with zero-indexing: `x.0`.
- The tuple without any values `()` is a special type called "unit type" with only one value `()` called "unit value",
  returned by expressions if they don't return any other value.
- Use arrays for fix-length, same-type compund values: `let a = [1, 2, 3];`.
- Array syntax: specify size explicitly: `let a: [i32, 2] = [1, 2];`, same value initialization `42`: `let a = [42; 3]`,
  indexing: `a[0]`.
- Runtime performs index-out-of-bound checking.
- Programming constructs: statements and expressions. Statements do not return a value. Expressions evaluate to
  a resulting value.
- Expressions do not end with semicolons, otherwise they would be considered as statements and would not return a value.
- A new scope block created with `{` and `}` is an expression as well and evaluates to the last expression in the block.
- Use the `fn` statement to declare a function.
- The `main` function is the program entry point.
- Naming convention: functions are named using snake_case.
- Function parameters and return type must have type annotations: `fn f(a: i32, c: char) -> i32 {}`.
- Use the `if` / `else` expression for conditional branching: `let n = if b { 1 } else { 2 };`.
- Use the `loop` (infinite), `while` (conditional) and `for` (iteration) keywords for various kinds of loops.
- Use the `break` statement to break out of the (innermost) loop.
- Use the  `continue` statement to jump to the beginning of the (innermost) loop.
- Use labeled loops for more complex control flow: `'label_name: loop { break 'label_name; }`.
- Use the `break` statement to return a value out of the loop: `let a = loop { break 3; }`.
- Use the `for` loop for iterating a collection: `for elem in collection {}`.
- Use `//` to begin a comment that ends at the end of the line.

## Ownership

- Rust does not have a garbage collector.
- Each value in Rust has an owner.
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped automatically.
- Types that deal with dynamic memory implement a special function `drop`, which the runtime calls automatically when
  the owner goes out of scope.
- Runtime will never make a "shallow" copy of data types that allocate dynamic memory, it will perform a move operation,
  making the original owner invalid.
- Runtime will never automatically create a "deep" copy of data - any automatic copy can be assumed to be inexpensive.
- "Deep" copy must be implemented by a programmer - `clone` function by convention.
- Values of types that store all data on the stack can be copied between variables. These types implement the `Copy`
  trait, provided by the language.
- Data type annotation prefixed with a `&` declares a reference.
- Create a reference to borrow data without giving ownership away.
- The scope of a reference ends at the last point where reference is used, thanks to Non-Lexical Lifetime (NLL) analysis
  performed by the compiler.
- References don't have ownership of the data, they are read-only by default, and the referenced value will not be
  dropped once reference goes out of scope.
- Prefix `&mut` creates a mutable reference, which are not allowed to co-exist with any other references (mutable or
  immutable) that are still in-scope.
- Runtime guarantees that all references refer to valid data.
- Use slices (special kind of reference) to reference a contiguous sequence of elements in a collection.
- Notation `[s..e]` refers to elements starting with index `s` and ending with index `e-1`.
- Notations `[..e]` and `[s..]` start with `0` and end with data length, respectively.

## Structs

- Use the `struct` keyword to define a new struct data type.
- Use the dot notation to access individual fields.
- Struct instances can be mutable, but there is no way to mark only certain fields as mutable.
- Use field init. shorthand to initialize struct fields with same-name variables.
- Use the struct update syntax `..struct1` to create a new struct instance from an existing one.
- Use tuple structs to strongly type tuples: `struct Point(i32, i32);`.
- Use unit-like structs to define types without state: `struct AlwaysEqual;`.
- Structs can contain references, but then instances require a lifetime parameter.
- Use the `impl` keyword to start an implementation block for a data type: `impl Point {}`.
- There can be multiple `impl` blocks for the same type.
- Use `self` / `&self` / `&mut self` as a first function parameter to define a method that can be called on a struct
  instance.
- The `self` shorthand is an alias for `self: Self`, where `Self` is itself an alias of a type that the `impl`
  block is for.
- Use the dot notation to call a method on an instance. Rust uses automatic referencing and dereferencing to call a
  method that takes ownership, or a reference, or a mutable reference - call syntax is always the same.
- It's possible to have a method with the same name as one of the struct's fields.
- Non-method functions defined in an `impl` block are called associated functions; they don't operate on instance level
  like methods, but are associated with the whole type.
- Use the `Type1::function1()` notation to call an associated function.

## Enums and Pattern Matching

- Use the `enum` keyword to define an enumeration type: `enum IPAddrType { V4, V6 }`.
- Use the `Enum1::variant1` notation to specify an enum variant in code.
- Enum variants can have an associated value of a specific type: `enum IPAddr { V4(String) }`. Different variants of the
  same enum can have associated values of different data types.
- There is a variety of ways to specify the data type of an enum variant.
- Methods can be written for enums, the same way as for structs.
- Use the `Option<T>` generic enum provided by the standard library, and included in the prelude together with its
  variants `None` and `Some(T)`, for null handling.
- Use the `match` control flow structure to execute code blocks based on an expressive pattern matching mechanism and
  compiler-time safety checks to validate that all possible cases are handled.
- Each `match` arm is an expression, and the result of the executed arm will be the result of the whole `match`
  expression.
- Arms of the `match` expression are evaluated in order, and the first one that matches the given expression will be
  executed.
- Use the `if let` notation to match only one pattern and ignore the rest: `if let Some(n) = optionN {  }`. Note that by
  using the `if let` the exhaustive checking that `match` enforces is lost. The `else` block is supported with `if let`.

## Rust Tools and The Module System

- Rust installation and upgrade tool: `rustup`.
- Compiler: `rustc`.
- Advanced build system and package manager: `cargo`.
- The module system includes concepts such as scope, packages, crates, modules, paths, etc.
- The module system is closely tied to the `cargo` build system.
- Package consists of one or more crates and a `Cargo.toml` crate descriptor.
- Crate can be built into a binary executable (contain the `main` function) or into a library.
- Package can contain at most one library crate.
- Crate root is a source file that the compiler starts from and makes up the root module of the crate.
- By convention, `src/main.rs` is the crate root of the binary crate that has tha same name as the package.
- By convention, `src/lib.rs` is the crate root of the library crate that has tha same name as the package.
- Package can have multiple binary crates by placing files in the `src/bin` directory, each file will be a crate root
  for a separate binary crate.
- Modules let the programmer control the organization, scope and privacy of code.
- To declare a module `module1`, in the crate root use `mod module1;` / `mod module1 {}`.
- The compiler will look for module code in three places: 1) inline, in the block of code following the declaration,
  2) in `src/module1.rs`, 3) in `src/module1/mod.rs` (deprecated).
- To declare a submodule `sub1`, in any file that belongs to `module1` use `mod sub1;` / `mod sub1 {}`.
- The compiler will look for submodule code in three places: 1) inline, in the block of code following the declaration,
  2) in `src/module1/sub1.rs`, 3) in `src/module1/sub1/mod.rs` (deprecated).
- Path is a full name of an identifier, e.g. type, for example: `crate::module1::sub1::Type1`.
- All identifiers in a module are private from it's parent module's perspective, and cannot be accessed with its path by
  default. However, identifiers in a parent module are accessible by default from child modules.
- Use `pub mod` instead of `mod` to make the module public, so parent modules can try to refer to it.
- Use the `pub` keyword before any declaration to make the identifier public.
- Making a module public does not make any identifier in it public, it must be done explicitly.
- Making a struct public doesn't make any of its fields public, it must be done explicitly for each field.
- Making an enum public makes all variants public.
- Use the `use` keyword to bring an identifier into  scope: `use crate::module1::sub1::Type1;`, then refer to `Type1`
  within the scope instead of using the long path. Identifier is visible only in the current scope, it is not visible in
  inner scopes. Privacy rules apply.
- The `crate` "module" is the fictitious root module that represents the current crate, and it sits at the root of the
  module tree when referring to an identifier from the current create by its absolute path. When referring to an
  identifier from another crate, path starts with the actual name of the crate.
- Paths can be relative, in which case they start with `self`, `super` or an identifier from the current module.
- Rust standard library is a crate called `std`, e.g.: `use std::collections::HashMap;`.
- Use `use` with `as` to define an alias: `use std::io::Result as IoResult;`.
- Use nested paths to combine imports: `use std::io::{self, Write};`.
- Use the glob operator to bring all public paths into scope: `use std::collections::*;`.
- Use `pub use` to re-export an identifiers from some child module in this module: `pub use crate::module1::FooBar;`.
- Declaring a module once, somewhere in the module tree, is enough for the compiler to know that that module needs to be
  built, there is no need to declare the module in every file in which the module will be referenced.

## Strings
- String represents a UTF-8 encoded sequence of Unicode characters.
- Strings are implemented as a growable, mutable, owned collection of bytes that can be interpreted as text
  (type `String` is a wrapper around vector of bytes - `Vec<u8>`).
- Type `String` is part of the standard library, but string slices, which have alias `str`, are part of the core
  language.
- Use the `+` operator to concatenate two `String`s.
- _Deref coercion_, performed by the compiler, enables transparent conversion from `&str` to `&str[..]`.
- Use the `format!` macro to make string by formatting values of other types.
- Type `String` doesn't support indexing because it would be indexing of individual bytes, not characters, and because
  it would not be a O(1) complexity operation, but O(n).
- There are three relevant ways (levels) to look at strings:
  - Strings are byte sequences.
  - Strings are sequences of scalar values (Unicode Scalar Value characters).
  - Grapheme clusters - the closest thing to what is commonly known as letters, but not quite the same.
- Rust provides different ways of interpreting raw byte data stored as part of a string.
- It is possible to create string slices, but runtime will panic if the slice starts or ends in the middle of a
  character encoding.

## Error Handling and Debugging

- The concept of exceptions does not exist.
- Recoverable and unrecoverable errors (result in program being stopped).
- Use the `panic!` macro to print a failure message, unwind the stack and stop the program.
- Add `panic = abort` to the `[profile]` section in `Cargo.toml` to compile the binary to abort immediately instead of
  doing the stack unwind when `panic!` occurs.
- Set environment variable `RUST_BACKTRACE` to anything other than `0` for `panic!` to print the stack trace as well
  (debugging symbols are needed).
- Use the `Result<T, E>` generic enum provided by the standard library, and included in the prelude, to hold either a
  result type object or an error type object, associated with the `Ok` and `Err` enum variants, respectively. Combines
  well with pattern matching.
- Use the `?` unary operator on a `Result<T, E>` operand to either evaluate to the `T` value, in case of the `Ok`
  variant, or to break out of the function and return the `Err` variant holding the `E` value, in case of the `Err`
  variant. Function's return type must be `Result` with the error type `E` or a type to which `E` can be converted.
- The `?` operator can also be used with the `Option<T>` enum (or any other type that implements the `FromResidual`
  trait).

## Generic Types and Traits
- Use `<` and `>` to declare generic functions: `fn largest<T>(list: &[T]) -> T {}`.
- Use `<` and `>` to define generic types: `struct Point<T> { x: T, y: T }`, `enum Option<T> { Some(T), None }`.
- Use type parameters in method definitions to define methods for all concrete types: `impl<T> Point<T> {}`.
- Specify a type to define methods for a specific concrete type: `impl Point<f32> {}`.
- Methods can be generic as well, independently from their type.
- There is no performance penalty for using generics - compiler performs monomorphization.
- Use traits to define functionality that one or more types can implement, i.e. to define shared behavior in an abstract
  way.
- Use trait bounds to specify that a generic type must be a type that implements requested behavior.
- Use the `trait` keyword to define a trait: `trait Summary { fn summarize(&self) -> String; }`.
- Use the `impl Trait1 for Type1 {}` notation to implement trait-declared methods for a type.
- The trait must be brought into scope as well as the type in order to call a trait-declared method.
- A trait can be implemented on a type only if either the trait or the type, or both, are local to the current crate.
- Methods can have a body when defined in a trait, as a way of providing default implementation.
- Default implementations can call other trait methods, even if they don't have a default implementation.
- Use traits as function parameters: `fn notify(item: &impl Summary) {}`. The `impl Trait1` notation is just a syntax
  shorthand for using trait bounds.
- Use trait bounds to constrain type parameters: `fn notify<T: Summary>(item &T) {}`.
- Use multiple types in trait bounds: `fn notify(item: &impl(Summary + Display)) {}`,
  `fn notify<T: Summary + Display>(item &T) {}`.
- Handle many trait bounds for clearer code by using the `where` notation:
  `fn some_fun<T, U>(t: &T, u: &U) -> i32 where T: Display + Clone, U: Close + Debug {}`.
- Use traits as return types of functions: `-> impl Trait1` (very useful with closures and iterators, where the type is
  generated by the compiler and thus unknown). However, this syntax is only possible in cases where exactly one type
  that implements `Trait1` can be returned from the function, due to implementation constraints in the compiler.
- Use trait bounds to conditionally implement methods for only a subset of types:
  `impl<T: Display + PartialOrd> Point<T> {}`.
- Use trait bounds to conditionally implement a trait for more than one type (blanked implementations for a generic type
  `T`): `impl<T: Display> ToString for T {}`, a feature extensively used in the Rust standard library. The `ToString`
  trait, for example, enables code such as `let s = 3.to_string();`.

## Lifetimes

- Runtime guarantees that all references refer to valid data.
- Lifetimes are generic parameters that ensure references are valid as long as they are needed.
- Every reference has a life time - the scope for which that reference is valid.
- Lifetimes can be, and usually are, implicit and inferred.
- Lifetime annotations, usually called just lifetimes (which is just creating confusion) describe the relationship of
  the life times of multiple references to each other, without actually affecting life times of those references.
- Use `'` (apostrophe) to annotate references with lifetimes: `&'a i32`, `&'a mut i32`...
- Naming convention: lifetimes identifiers are usually short, often one-character lowercase names like `'a` or `'b`.
- References annotated with the same lifetime (e.g. `'a`), must both live as long as that generic lifetime (`'a`).
- Use generic lifetimes in functions: `fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {}`. This reads as "the
  returned reference will be valid as long as both references that are passed at the call site are valid". On the call
  site, generic lifetime `'a` will get the concrete lifetime  that is equal to the smaller lifetime (narrower scope) of
  the lifetimes of `x` and `y`.
- Lifetimes are necessary instructions from the programmer that help the compiler's borrow checker to do its job.
- References that are struct fields must be lifetime-annotated, thus the struct type must have a generic lifetime
  parameter.
- _Lifetime elision rules_ - common lifetime usage patterns programmed into the compiler's reference analyzer that
  enable the compiler to deterministically assign lifetimes to references in certain common cases, without the
  programmer's input.
- Use the `&'static` notation to declare that a reference has static lifetime, i.e. the reference _can_ live for the
  entire duration of the program.

## Automated Tests

- Test is a function that's annotated with the `test` attribute: `#[test]`.
- Use the `panic!`, `assert!`, `assert_eq!`, `assert_ne!` macros to fail and conditionally fail the test.
- Annotate a test function with the `should_panic` attribute if it is expected for the function to panic (e.g. negative
  tests): `#[should_panic]`.
- Tests can return `Result<T, E>`, where `Err` variant indicates test failure.
- Use `cargo test` command to run tests in various ways (run `cargo test --help`).
- Messages written to stdout in test functions will not be shown by default when tests are run with `cargo test`.
- Annotate a test function with the `ignore` attribute to avoid running the test, unless the `--ignored` or
  `--include-ignored` option is passed to `cargo test`: `#[ignore]`.
- Annotate a module with `#[cfg(test)]` to only build the module when running tests with `cargo` (when module is part of
  a crate, e.g. for unit tests).
- Create the `tests` directory next to the `src` directory in the project root for integration tests; no need to
  annotate test modules in this case.
- Each file in the `tests` directory will be compiled as a separate crate.
- To use submodules in the `tests` directory (e.g. code sharing), place them in `tests/{submodule-name}/mod.rs`.

## Functional Programming: Closures

- Closures are anonymous functions that can be saved in a variable or passed as arguments to other functions, with the
  ability to capture values from the scope in which they're defined.
- Use the `| {param-list} | { {body} }` notation to define closures.
- If closure body consists of one expression, block braces can be omitted.
- Values can be captured by taking ownership, borrowing and borrowing mutably, based on the way value is used in the
  closure body. Borrowing happens at the point of closure definition, and ends after the last closure call.
- Use the `move` keyword before the parameter list to force taking ownership of captured values instead of borrowing.
- `Fn` traits (3) enforce the rules of what closure can do with the caputed values, and closures can implement one, two
  or all three of the `Fn` traits in additive fashion:
  - `FnOnce` trait applies to closures that can be called at least once, which is true for all closures, however, if the
    closure doesn't implement any other `Fn` trait, it can then be called at most once (this is because such closures
    take ownership of at least one value from their environment).
  - `FnMut` applies to closures that don't move captured values out of their body, but they do mutate captured values,
    and these closures can be called more than once.
  - `Fn` applies to closures that don't move captured values out of the body and don't mutate captured values, and these
    closures can be called more than once without mutating their environment (important in concurrent programming).
- Functions can also satisfy `Fn` traits in cases where nothing needs to be captured from the environment.

## Functional Programming: Iterators

- Use iterator to perform a task on a sequence of items in turn.
- Iterators are lazy, they have no effect until a method that consumes them is called.
- All iterators implement the `Iterator` trait from the standard library that declares that the method `next` must be
implemented to return the next item in the sequence.
- Use `iter` (returns references), `into_iter` (returns owned values), `iter_mut` (returns mutable references) to create
iterators for standard library types.
- _Consuming adaptors_ are functions that take ownership of iterators and use them up by repeatedly calling the `next`
  method to use up the next item.
- _Iterator adaptors_ are functions that take ownership of iterators and produce other iterators with specific behavior.
