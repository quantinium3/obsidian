---
id: Collections
aliases: []
tags: []
title: Collections
---

## Vectors
Vectors allow you to store more than one value in a single data structure that puts all the values next to each other in memory. Vectors can only store values of the same type. They are similar to vector in C++.

### Create a vector
```rust
let v: Vec<i32> = Vec::new();
```
Here we had to define the type cause we haven't put any value in the vector.

Generally rust compiler will infer the type of data that is stored inside the vector if put an element while defining the vector.
```rust
    let v = vec![1, 2, 3];
```
### Update a vector
We use the push method to push element to the back of the vector
```rust
    let mut v = Vec::new();

    v.push(5);
    v.push(6);
    v.push(7);
    v.push(8);
```
### Reading elements of a vector
In rust we have two way to get the value of a vector at an index - `[]`,`get()`. The vectors in rust at 0 indexed so first element is at index 0.

```rust
    let v = vec![1, 2, 3, 4, 5];

    let third: &i32 = &v[2];
    println!("The third element is {third}");

    let third: Option<&i32> = v.get(2);
    match third {
        Some(third) => println!("The third element is {third}"),
        None => println!("There is no third element."),
    }
```

### Iterating over the values in a vector
To iterate over elements in a vector we can use for loop to get a mutable or immutable reference of elements in a vector
```rust
    let v = vec![1, 2, 3, 4, 5];
    for i in &b {
        println!("{i}")
    }

    let mut v = vec![100, 32, 57];
    for i in t &mut v {
        *i += 50;
    }

```
Vectors (`Vec<T>`) implement the `iter()` method, which returns an iterator over references to the elements in the vector.
```rust
    let v = vec![1, 2, 3, 4, 5];
    for i in v.iter() {
        println!("{i}")
    }
```

### Using an enum to store multiple types
Vectors can only store values that are of the same type. This can be inconvenient; there are definitely use cases for needing to store a list of items of different types

```rust
    enum SpreadsheetCell {
        Int(i32),
        Float(f64),
        Text(String),
    }

    let row = vec![
        SpreadsheetCell::Int(3),
        SpreadsheetCell::Text(String::from("blue")),
        SpreadsheetCell::Float(10.12),
    ];
```

### Dropping a vector
Vector in rust implement the `Drop` trait i.e. when a vector goes out of scope it would be freed.

```rust
    {
        let v = vec![1, 2, 3, 4];

        // do stuff with v
    } // <- v goes out of scope and is freed here
```
