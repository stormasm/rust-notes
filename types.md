
### What is Any

[How to get the type name from `TypeId`?](https://users.rust-lang.org/t/how-to-get-the-type-name-from-typeid/75507)

I don't think this is possible. A type ID is just a hash computed from the various unspecified parts (field/variant names and types, layout, etc.) of a type. It inherently loses information. It only exists for comparing types for equality, but it is not reversible.

### References

- [Any](https://doc.rust-lang.org/std/any/index.html)
