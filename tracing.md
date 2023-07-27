
### Tracing Notes

```
rg disable_everything
```

To take out the time stamps see the [fmt example](https://github.com/tokio-rs/tracing/blob/master/examples/examples/fmt.rs)

```rust
tracing_subscriber::fmt()
    // enable everything
    .with_max_level(tracing::Level::TRACE)
    // no time stamps
    .without_time()
    // sets this to be the default, global collector for this application.
    .init();
```
