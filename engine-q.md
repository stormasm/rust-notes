
### Parser otherwise known as parser.rs

*Taking it from the top parse_file calls parse_block*

* parse_value takes a span and a shape
* parse_statement is called from parse_block
* parse_block is only called from the parser

methods that call parse_expression:   
* parse_block
* parse_statement
* parse_multispan_value

methods that call parse_block include :   
* parse_block_expression
* parse_full_column_path
* parse_file which is only called from main.rs
* parse_source which is only called from syntax_highlight.rs

##### parse_expression

**parse_call** is a very critical method and it really only gets called in one place namely in **parse_expression** and if you look at **parse_expression** you will note that besides signaling **parse_math_expression** its main job is to run **parse_call**

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

##### parser.rs enums

```rust

pub enum SyntaxShape {
    /// A specific match to a word or symbol
    Keyword(Vec<u8>, Box<SyntaxShape>),

    /// Any syntactic form is allowed
    Any,

    /// Strings and string-like bare words are allowed
    String,

    /// A dotted path to navigate the table
    ColumnPath,

    /// A dotted path to navigate the table (including variable)
    FullColumnPath,

    /// Only a numeric (integer or decimal) value is allowed
    Number,

    /// A range is allowed (eg, `1..3`)
    Range,

    /// Only an integer value is allowed
    Int,

    /// A filepath is allowed
    FilePath,

    /// A glob pattern is allowed, eg `foo*`
    GlobPattern,

    /// A block is allowed, eg `{start this thing}`
    Block,

    /// A table is allowed, eg `[[first, second]; [1, 2]]`
    Table,

    /// A table is allowed, eg `[first second]`
    List(Box<SyntaxShape>),

    /// A filesize value is allowed, eg `10kb`
    Filesize,

    /// A duration value is allowed, eg `19day`
    Duration,

    /// An operator
    Operator,

    /// A math expression which expands shorthand forms on the lefthand side, eg `foo > 1`
    /// The shorthand allows us to more easily reach columns inside of the row being passed in
    RowCondition,

    /// A general math expression, eg `1 + 2`
    MathExpression,

    /// A variable name
    Variable,

    /// A variable with optional type, `x` or `x: int`
    VarWithOptType,

    /// A signature for a definition, `[x:int, --foo]`
    Signature,

    /// A general expression, eg `1 + 2` or `foo --bar`
    Expression,
}

pub enum Operator {
    Equal,
    NotEqual,
    LessThan,
    GreaterThan,
    LessThanOrEqual,
    GreaterThanOrEqual,
    Contains,
    NotContains,
    Plus,
    Minus,
    Multiply,
    Divide,
    In,
    NotIn,
    Modulo,
    And,
    Or,
    Pow,
}

pub enum Expr {
    Bool(bool),
    Int(i64),
    Var(VarId),
    Call(Box<Call>),
    ExternalCall(Vec<u8>, Vec<Vec<u8>>),
    Operator(Operator),
    BinaryOp(Box<Expression>, Box<Expression>, Box<Expression>), //lhs, op, rhs
    Subexpression(BlockId),
    Block(BlockId),
    List(Vec<Expression>),
    Table(Vec<Expression>, Vec<Vec<Expression>>),
    Keyword(Vec<u8>, Span, Box<Expression>),
    String(String), // FIXME: improve this in the future?
    Signature(Box<Signature>),
    Garbage,
}

pub enum Import {}

pub enum Statement {
    Declaration(DeclId),
    Pipeline(Pipeline),
    Expression(Expression),
}
```

##### parser.rs structs

```rust

pub struct Block {
    pub stmts: Vec<Statement>,
}

pub struct Call {
    /// identifier of the declaration to call
    pub decl_id: DeclId,
    pub head: Span,
    pub positional: Vec<Expression>,
    pub named: Vec<(String, Option<Expression>)>,
}

pub struct Expression {
    pub expr: Expr,
    pub span: Span,
    pub ty: Type,
}

pub struct Pipeline {
    pub expressions: Vec<Expression>,
}

pub struct VarDecl {
    var_id: VarId,
    expression: Expression,
}
```
