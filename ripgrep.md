
### Find a pattern in a certain file

```rust
rg csv -g 'Cargo.toml'
```

[ref](https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md#manual-filtering-file-types)

[Fixed Strings](https://mariusschulz.com/blog/fast-searching-with-ripgrep#fixed-strings) when you want to search for this exact string and not have rg interpret it as a regex or whatever.

```rust
rg -F '$nu'
rg -F '$in'
```

To exclude searching in recursively lower directories
simply state the file or files you want to search for...

For example to only search *.go files in a particular directory

```
rg tsm1 *.go
```

```
rg \/data\/gen
```

To tell rg to use a regular expression put it in single quotes

```
rg 'init\('
rg '\[\[measurements\]\]'
```
