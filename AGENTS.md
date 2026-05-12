# Repository Guidelines

## Project Structure & Module Organization

This repository contains documentation for a Gitee CLI skill, not an application package.

- `SKILL.md` is the primary skill definition. Update it when command behavior, supported subcommands, or agent guidance changes.
- `references/command-reference.md` contains detailed `gitee` command syntax.
- `references/workflows.md` contains multi-step agent workflows.
- `references/troubleshooting.md` contains authentication, permission, and remote URL troubleshooting.
- `agents/openai.yaml` contains UI metadata for skill hosts that support it.
- `README.md` explains installation and setup.
- `cargo.md` documents Rust and Cargo installation.
- `CLAUDE.md` provides Claude Code-specific guidance.

Keep `SKILL.md` concise. Put detailed command reference material in `references/` so agents can load it only when needed.

## Build, Test, and Development Commands

There is no build step for this repository. Use these checks while editing:

```bash
gitee --version
```

Verifies that the local Gitee CLI is installed.

```bash
gitee <subcommand> --help
```

Checks current command syntax before documenting it in `references/command-reference.md`.

```bash
git diff --check
```

Detects trailing whitespace and basic patch formatting issues.

## Coding Style & Naming Conventions

Write concise Markdown. Prefer short headings, direct instructions, and fenced code blocks for commands. Use backticks for command names, environment variables, and paths, such as `GITEE_TOKEN`, `owner/repo-name`, and `SKILL.md`.

Preserve the repository’s mixed Chinese and English style: Chinese is appropriate for user instructions and command explanations; English is acceptable for metadata, headings, and conventional repository files.

## Testing Guidelines

No automated test suite is currently defined. Validate docs by checking referenced commands against the installed `gitee` CLI where possible. For remote examples, avoid destructive operations unless the command is explicitly about deletion or closing.

When adding command examples, include required arguments and a realistic placeholder, for example:

```bash
gitee repo info owner my-project
```

## Commit & Pull Request Guidelines

Recent commits use short messages, often in Chinese, with occasional Conventional Commit prefixes such as `feat:` and `refactor`. Keep messages brief and action-oriented, for example `feat: 完善 issues 命令说明` or `fix skill.md`.

Pull requests should include a short summary, changed docs, and how command syntax was verified. Link related issues when available.

## Security & Configuration Tips

Never commit real Gitee tokens. Document authentication through environment variables only:

```bash
export GITEE_TOKEN="你的_令牌"
```

Most `gitee` commands use separate `<OWNER> <REPO>` arguments; use `owner/repo-name` only when a command explicitly requires a combined identifier. Call out destructive commands clearly.
