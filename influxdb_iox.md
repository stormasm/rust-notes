
Initially to start up postgresql when you reboot the machine....

```rust
brew services start postgresql
```

instructions are here:
https://github.com/influxdata/influxdb_iox/tree/main/iox_catalog

If this is not installed go ahead and do it...

```rust
cargo install sqlx-cli

DATABASE_URL=postgres:///iox_shared sqlx database create
```
Run these commands at the top level influxdb_iox

```rust
cargo run -q -- catalog setup
cargo run -- catalog topic update iox-shared
```
Then cd iox_catalog and run

```rust
cargo test or cnr
```
