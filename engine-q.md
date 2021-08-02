
##### parser_state.rs

```rust
pub type VarId = usize;
pub type DeclId = usize;
pub type BlockId = usize;

pub enum Type {
    Int,
    Bool,
    String,
    Block,
    ColumnPath,
    Duration,
    FilePath,
    Filesize,
    List(Box<Type>),
    Number,
    Table,
    Unknown,
}

struct ScopeFrame {
    vars: HashMap<Vec<u8>, VarId>,
    decls: HashMap<Vec<u8>, DeclId>,
}

pub struct ParserState {
    files: Vec<(String, usize, usize)>,
    file_contents: Vec<u8>,
    vars: Vec<Type>,
    decls: Vec<Declaration>,
    blocks: Vec<Block>,
    scope: Vec<ScopeFrame>,
}
```

##### parser.rs

```rust

pub struct Expression {
    pub expr: Expr,
    pub span: Span,
    pub ty: Type,
}

pub struct Block {
    pub stmts: Vec<Statement>,
}

pub struct VarDecl {
    var_id: VarId,
    expression: Expression,
}
```
