---
name: gitee-cli
description: 当当前项目托管在 gitee.com，或用户要求操作 Gitee 仓库、Issue、Pull Request、Release、Wiki、Label、通知、文件等资源时使用。通过 gitee CLI 和 git 完成仓库协作任务，并在需要时读取 references 中的命令参考和工作流。
---

# Gitee CLI Skill

Use this skill to operate Gitee-hosted repositories and related resources through the `gitee` command line tool. This is an agent workflow guide, not a full command manual.

## When To Use

Use this skill when:

- The repository remote URL contains `gitee.com`.
- The user asks to list, create, update, comment on, close, merge, or inspect Gitee Issues or Pull Requests.
- The user asks to manage Gitee repositories, releases, wiki pages, labels, notifications, users, or repository files.
- A GitHub-oriented workflow is requested but the project remote is hosted on Gitee.

Do not use this skill for GitHub, GitLab, or local-only git work unless the task explicitly involves Gitee.

## First Checks

1. Identify the repository remote:
   ```bash
   git remote -v
   ```
   Prefer `owner/repo` derived from the Gitee remote URL when the user does not provide it.

2. Confirm the CLI is available:
   ```bash
   gitee --version
   ```

3. Confirm authentication is configured before API operations:
   ```bash
   test -n "$GITEE_TOKEN"
   ```
   If missing, ask the user to set `GITEE_TOKEN`. Do not ask them to paste a token into chat.

4. For unfamiliar or version-sensitive syntax, run:
   ```bash
   gitee <command> --help
   ```

## Operating Principles

- Prefer `gitee` CLI commands for Gitee resources; use web browsing only when CLI coverage is insufficient.
- Use `owner repo` positional arguments where the CLI expects separate values; use `owner/repo-name` only where a command explicitly asks for a combined repository identifier.
- Show the user the intended action before destructive operations such as deleting repositories, deleting wiki pages, deleting labels, closing issues, closing PRs, or merging PRs.
- Break multi-step tasks into inspect, modify, verify phases. Example: list PR -> inspect details/comments -> act -> re-read PR.
- Do not invent missing command flags. Check `gitee <subcommand> --help` when uncertain.

## Reference Files

Load these files only when needed:

- `references/command-reference.md`: exact command syntax and examples for repo, issue, PR, label, release, wiki, file, notification, and user operations.
- `references/workflows.md`: common agent workflows such as triaging issues, creating PRs, reviewing PR comments, and publishing releases.
- `references/troubleshooting.md`: authentication, permission, remote URL, and API troubleshooting.

## Common Task Routing

- Need exact subcommand syntax: read `references/command-reference.md`.
- Need to complete a multi-step repository task: read `references/workflows.md`.
- Command fails due to auth, network, permissions, or unclear repo identity: read `references/troubleshooting.md`.

## Safety Checklist

Before making remote changes:

1. Confirm the target repository owner and name.
2. Confirm whether the action changes remote state.
3. For destructive or irreversible actions, get explicit user approval.
4. Run a read command after the change when possible to verify the result.
