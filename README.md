# paraskinio
Versioned data of Café Paraskinio

## Diffing DOCX files

This repo uses a custom Git diff driver so `git diff` and `git log -p` show readable changes in `.docx` files instead of binary diffs.

**One-time setup** (needs [Pandoc](https://pandoc.org/) installed):

```bash
git config diff.docx.textconv "pandoc --from=docx --to=plain"
```

After that, `git diff`, `git show`, and `git log -p` will show DOCX content as plain text. For `git show <commit>` use `git show --ext-diff <commit>` so the driver is used.
