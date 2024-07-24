# rust_analyzer syntax error

the `rust_analyzer` lsp will show a syntax error in the `main.rs` file if the file is `[noeol]` - meaning it does not end with a final newline character.

the syntax error simply says "Syntax Error: Unmatched `}`", and is not helpful in diagnosing the actual problem.

in this minimal reproduction, the issue is triggered by the `.editorconfig` file.
for `*.rs` files, the `.editorconfig` file specifies `insert_final_newline = false`, which means that the file will *not* end with a newline character.

note: with my nvim config, i trigger `RustFmt` on save, which might be related to the end result / issue
(since it does have some way of dealing with final newlines, as far as i know), depending on how it interacts with the `.editorconfig`.
