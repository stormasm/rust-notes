
```rust
alias ct='cargo test'
```

### To see a list of all of the flags for cargo test

```rust
ct --help
```

## Datafusion Testing Examples

### To see a list of test targets first run this command

```
ct --test
```

### Then to see the output of just one test

```rust
ct --test filename testname
ct --test tpcds_planning tpcds_physical_q98
```

To test a specific module:

cargo test physical_plan::

Note here the key is the name of the module and then the "::" afterwards...

This is for example with datafusion

```rust
alias ctpp='cnr physical_plan::'
```
