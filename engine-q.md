
* [engine-q datastructures](./enqine-q-ds.md)

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

#### parse_expression

**parse_call** is a very critical method and it really only gets called in one place namely in **parse_expression** and if you look at **parse_expression** you will note that besides signaling **parse_math_expression** its main job is to run **parse_call**
