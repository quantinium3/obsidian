---
id: Smart Pointers
aliases: []
tags: []
title: Smart Pointers
---

A pointer is a general concept for a variable that contains an address in memory. This address refers to, or "points at", some other data.

Smart Pointer on the other hand, are data structures that act like a pointer but also have additional metadata and capabilities. `String` and `vec<T>` are also smart pointers. Smart pointers are usually implemented using structs. Unlike ordinary structs, smart pointers implement the `Deref` and `Drop` traits. The `Deref` trait allows an instance of smart pointer struct to behave like reference. The `Drop` trait allows you to customize the code that's run when an instance of the smart pointer goes out of scope.

The most common smart pointers in std library are - 
- `Box<T>` for allocating values on the heap.
- `Rc<T>`, a references counting type that enables multiple ownership.
- `Ref<T>` and `RefMut<T>`, accessed through `RefCell<T>` a type that enforces the borrowing rules at runtime instead of compile time.

## **USING Box<T> to point to Data on the heap**
Boxes allow you to store data on the heap rather than the stack. What remains on the stack is the pointer to the heap data.

We'll use them in situations such as - 
- When you have a type whose size can’t be known at compile time and you want to use a value of that type in a context that requires an exact size
- When you have a large amount of data and you want to transfer ownership but ensure the data won’t be copied when you do so.
- When you want to own a value and you care only that it’s a type that implements a particular trait rather than being of a specific type

### **Using a `Box<T>` to store data on the heap**
```rust
fn main() {
    let b = Box::new(5); // Store the value 5 on the heap
    println!("b = {}", b); // Dereference the box to access the value
}
```
- `Box::new(5)` allocates memory on the heap to store the value 5.
- The variable b is a `Box<i32>` that points to this heap-allocated value.
- When you print `b`, Rust automatically dereferences the box to access the value inside.

### **Enabling recursive types with boxes**
Rust needs to know the size of types at compile time, but recursive types (like linked lists or trees) have an indeterminate size. `Box<T>` can be used to create recursive types by storing the recursive part on the heap.

```rust
enum List {
    Cons(i32, Box<List>), // Recursive part is boxed
    Nil, // Base case
}

fn main() {
    let list = List::Cons(1, Box::new(List::Cons(2, Box::new(List::Nil))));
}
```

`Box<List>` allows the `Cons` variant to hold another `List` without causing infinite size issues as rust knows the size of a pointer and it  doesn't change based on the amount of data it's pointing to.

The `Cons` variant needs the size of an `i32` plus the space to store the box’s pointer data. The `Nil` variant stores no values, so it needs less space than the `Cons` variant. We now know that any `List` value will take up the size of an `i32` plus the size of a box’s pointer data. By using a `box`, we’ve broken the infinite, recursive chain, so the compiler can figure out the size it needs to store a `List` value.

![[Pasted image 20250226131333.png]]

Boxes provide only the indirection and heap allocation; they don’t have any other special capabilities.They also don’t have the performance overhead that these special capabilities incur, so they can be useful in cases like the cons list where the indirection is the only feature we need.

The `Box<T>` type is a smart pointer because it implements the `Deref` trait, which allows `Box<T>` values to be treated like references. When a `Box<T>` value goes out of scope, the heap data that the box is pointing to is cleaned up as well because of the `Drop` trait implementation. 
