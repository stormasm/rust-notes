
- [static-web-server](https://github.com/static-web-server/static-web-server)

To serve up a set of files like pics for example or my diary files
you need to do the following things which are not obvious and very
frustrating each time I come back to trying to figure out how to
get this to work so here goes :)


- This alias is located inside the [dotfile .rust](https://github.com/stormasm/dotfiles/blob/main/.rust)

```rust
alias sws='sws --port 3000'
```

- First of all you need to know the proper switches

```rust
sws -d pics -z
```

- There are two directories that you need to know about.
- The first directory is the top level directory which by default
is called *public*
- So you can skip the *-d* flag if everything lives in public
- In the above example everything lives in pics
- The *-z* flag is required
- The *-d* switch is the top level directory of where everything lives

### Pics Example

- So if your image files lives in

```rust
pics/album01
```

- This is how you fire up your web server

```rust
sws -d pics -z
```

- This is what your request looks like
- [all image files](http://localhost:3000/album01/)
- [one image file](http://localhost:3000/album01/IMG_3300.jpeg)

### Diary Example

- Assuming this time that you have a *public* directory and that
your diary files live in diary
- This is how you fire up your web server
- Go to the directory where your *public* folder lives like *tmp99*

```rust
sws -z --directory-listing-order 0
```

- This is what your request looks like
- [all diary files](http://localhost:3000/diary/)
- [one diary file](http://localhost:3000/diary/c24jsi.html)

#### Directory Listing

Note by default this is set to off so you need to add in the *-z* switch

      --directory-listing [<DIRECTORY_LISTING>]
          Enable directory listing for all requests ending with the slash character (‘/’) [env: SERVER_DIRECTORY_LISTING=] [default: false] [possible values: true, false]   

      --directory-listing-order <DIRECTORY_LISTING_ORDER>   
          Specify a default code number to order directory listing entries per `Name`, `Last modified` or `Size` attributes (columns). Code numbers supported: 0 (Name asc), 1 (Name desc), 2 (Last modified asc), 3 (Last modified desc), 4 (Size asc), 5 (Size desc). Default 6 (unordered) [env: SERVER_DIRECTORY_LISTING_ORDER=] [default: 6]

      --directory-listing-format <DIRECTORY_LISTING_FORMAT>   
          Specify a content format for directory listing entries. Formats supported: "html" or "json". Default "html" [env: SERVER_DIRECTORY_LISTING_FORMAT=] [default: html] [possible values: html, json]
