
### Destructuring assignment

* [From the Rust RFC Book](https://rust-lang.github.io/rfcs/2909-destructuring-assignment.html#Summary)
* [Javascript example](https://www.freecodecamp.org/news/how-to-use-destructuring-in-javascript-to-write-cleaner-more-powerful-code-9d1b38794050/#:~:text=Destructuring%20is%20the%20process%20of,an%20Object%20or%20an%20Array.)

By getting back the structure you are able to dive into it and get the values

* [all_in_one.rs](https://github.com/influxdata/influxdb_iox/blob/main/influxdb_iox/src/commands/run/all_in_one.rs#L473)

```
pub async fn command(config: Config) -> Result<()> {
    let SpecializedConfig {
        compactor_run_config,
        catalog_dsn,
        querier_config,
    } = config.specialize();

    let metrics = Arc::new(metric::Registry::default());

    let catalog = catalog_dsn
        .get_catalog("iox-all-in-one", Arc::clone(&metrics))
        .await?;
```

### Turn off doc test

```rust
# these next two lines turn off doc tests
[lib]
doctest = false
```

[How to opt out of running a doc test](https://stackoverflow.com/questions/32429369/how-to-opt-out-of-running-a-doc-test)
