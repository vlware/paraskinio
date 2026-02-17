# paraskinio
Versioned data of Café Paraskinio

## Diffing DOCX files

### Local diffs (terminal)

This repo uses a custom Git diff driver so `git diff` and `git log -p` show readable changes in `.docx` files.

**One-time setup** (requires [Pandoc](https://pandoc.org/)):

```bash
git config diff.docx.textconv "pandoc --from=docx --to=plain"
```

Then `git diff`, `git log -p`, and `git show --ext-diff` will show DOCX content as text.

### Diffs in GitHub PRs

GitHub does **not** run your local `textconv`, so PR “Files changed” would still show `.docx` as binary. To get readable diffs in PRs, the repo keeps a **Markdown copy** of each `.docx` (same base name, `.md`). GitHub diffs the `.md` file, so you see the real content changes.

**One-time setup** (requires [Pandoc](https://pandoc.org/)):

```bash
cp hooks/pre-commit hooks/post-commit .git/hooks/
chmod +x .git/hooks/pre-commit .git/hooks/post-commit
```

After that, whenever you commit a `.docx`, the hooks will create or update the matching `.md` in the same commit. PRs will show the diff of the `.md` (and you can use “View file” on the `.md` for a rendered view). Edit only the `.docx`; the `.md` is generated and should not be edited by hand.
