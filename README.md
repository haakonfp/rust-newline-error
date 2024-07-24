# rust_analyzer syntax error

the `rust_analyzer` lsp will show a syntax error in a `.rs` file if the file is `[noeol]` - meaning it does not end with a final newline character.

the syntax error is at the end of the file, and simply says "Syntax Error: Unmatched `}`".
Not exactly helpful in diagnosing the actual problem.

in this minimal reproduction, the issue is triggered by the `.editorconfig` file.
for `*.rs` files, the `.editorconfig` file specifies `insert_final_newline = false`, which means that the file will *not* end with a newline character.

note: with my nvim config, i trigger `RustFmt` on save, which might be related to the end result / issue
(since it does have some way of dealing with final newlines, afaik), depending on how it interacts with the `.editorconfig`.

fix: in this case, we can simply set `insert_final_newline = true` for `*.rs` files in the `.editorconfig` file.
if you don't have any other overrides, you can also go over and change each file type to `eol` in your editor.

---

i made this repo to showcase the issue, and to have a minimal reproduction of the problem.

my goal is to figure out where the syntax error is thrown in `rust_analyzer`, so we can make the error message more helpful and/or descriptive.
