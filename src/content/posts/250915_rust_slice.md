---
title: 'Rust Slice Type [T]'
description: 'The right mental model for a rust slice.'
pubDate: 2025-09-15
author: 'Fabian Binkert'
tags: ['Rust']
---
Rust’s slice type is a curious case. Unlike a vector (`Vec<T>`), a slice `[T]` doesn’t have its own memory layout. It’s a dynamically sized type, so its size isn’t known at compile time. To make things spicier, Rust terminology often blurs the line between a slice `[T]` and a reference to a slice `&[T]`. Colloquially, the latter is usually what people mean by “a slice of `T`”.

## Mental Model

The slice type `[T]` is often described as:
> A dynamically sized view into a contiguous sequence, `[T]`. ([source](https://doc.rust-lang.org/std/primitive.slice.html))

I find that phrasing can mislead: it suggests the slice itself carries a size, which conflicts with being unsized.

A better intuition: a slice `[T]` is an abstract “window shape” that doesn’t hold length. As an abstract type, it can’t be assigned to a variable:

```rust
// This will NOT compile
// error[E0277]: the size for values of type `[i32]` cannot be known at compilation time
let my_slice: [i32] = [1, 2, 3];
```

In practice, a slice `[T]` only exists behind a fat pointer that carries the missing length as metadata:

- `&[T]`, `&mut [T]`, `*const [T]`, `*mut [T]`, `Box<[T]>`, `Rc<[T]>`, `Arc<[T]>`

Key point: the length lives in the fat pointer, not inside `[T]`. "Inside `[T]`" doesn't even make much sense because remember, `[T]` is simply an abstract window shape.

## Slice Reference `&[T]`

By contrast, the slice reference `&[T]` has a concrete layout: a fat pointer with
- a pointer to the first element, and
- a length (in elements)

So `&[T]` is always two machine words on the target architecture. Because a bare `[T]` can’t be used directly, `&[T]` is what most people mean by “slice.”

Creating a slice reference:

```rust
let v: Vec<i32> = vec![10, 20, 30, 40];
let sv: &[i32] = &v;       // whole vector
```

## Conclusion

Mentally, treat `[T]` as an abstract “window shape” that holds no length. The length lives in the fat pointer. That’s why you can’t store a bare `[T]`, and why “slice” in practice almost always means `&[T]`.
