
[discord](https://discord.com/channels/601130461678272522/614613939334152217/974703732128383036)

```rust
enum MyError {
    InvalidInput(String)
}

impl std::error::Error for MyError {
    ....
}
```

then your code can be

```rust
fn GetFoo(i: i64) -> Result<Foo, MyError> {
    match i {
        1 => Ok(Foo::A),
        2 => Ok(Foo::B),
        3 => Ok(Foo::C),
        _ => Err(MyError::InvalidInput("invalid input".to_string()))
    }
}
```
