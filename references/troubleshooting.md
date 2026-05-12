# Gitee CLI Troubleshooting

Use this file when `gitee` commands fail or repository identity is unclear.

## CLI Not Installed

Check:

```bash
gitee --version
```

If missing, install with Cargo:

```bash
cargo install gitee-cli
```

Rust and Cargo installation notes live in `cargo.md` at the repository root.

## Missing Authentication

Check:

```bash
test -n "$GITEE_TOKEN"
```

If empty, ask the user to create a Gitee personal access token in the Gitee web UI and set it locally:

```bash
export GITEE_TOKEN="你的_令牌"
```

Never ask the user to paste the token into chat, and never commit tokens.

## Wrong Repository

Inspect remotes:

```bash
git remote -v
git branch -vv
```

For `https://gitee.com/owner/repo.git`, use:

```bash
gitee repo info owner repo
```

If a command expects a combined repository value, use `owner/repo`. Otherwise prefer separate `OWNER` and `REPO` positional arguments.

## Permission Or 404 Errors

Common causes:

- `GITEE_TOKEN` does not include the required permission.
- The repository is private and the token user cannot access it.
- Owner or repository name is misspelled.
- The API base is overridden incorrectly through `GITEE_API_BASE`.

Use a read-only command first:

```bash
gitee user info
gitee repo info <OWNER> <REPO>
```

## Help Language Or Output

The CLI supports language selection:

```bash
gitee --lang zh <COMMAND> --help
gitee --lang en <COMMAND> --help
```

If documentation and installed behavior disagree, trust the installed CLI help and update `references/command-reference.md`.

## Remote State Safety

Before destructive commands, confirm the target and intent with the user. This applies to:

- `gitee repo delete`
- `gitee issues close`
- `gitee pr close`
- `gitee pr merge`
- `gitee labels delete`
- `gitee wiki delete`
