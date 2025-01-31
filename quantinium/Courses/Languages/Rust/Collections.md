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


