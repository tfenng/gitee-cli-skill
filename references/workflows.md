# Gitee Agent Workflows

Use this file for multi-step tasks. Keep read operations before write operations, and verify after changes.

## Resolve Repository Identity

```bash
git remote -v
```

For HTTPS remotes like `https://gitee.com/owner/repo.git`, use `owner` and `repo` as separate CLI arguments. If multiple remotes exist, prefer the remote used by the current branch:

```bash
git branch -vv
```

## Inspect A Repository

```bash
gitee repo info <OWNER> <REPO>
gitee issues list <OWNER> <REPO>
gitee pr list <OWNER> <REPO>
gitee releases list <OWNER> <REPO>
```

Summarize the relevant results instead of dumping raw command output unless the user asks for exact output.

## Create An Issue

1. Confirm target repository.
2. Draft title and body from the user's request.
3. Run:
   ```bash
   gitee issues create <OWNER> <REPO> "<TITLE>" --body "<BODY>"
   ```
4. Re-read the issue when an issue number is returned:
   ```bash
   gitee issues-ext detail <OWNER> <REPO> <NUMBER>
   ```

## Comment On Or Close An Issue

1. Inspect the issue:
   ```bash
   gitee issues-ext detail <OWNER> <REPO> <NUMBER>
   ```
2. Add a comment if requested:
   ```bash
   gitee issues-ext comment <OWNER> <REPO> <NUMBER> "<BODY>"
   ```
3. Closing changes remote state; confirm intent before:
   ```bash
   gitee issues close <OWNER> <REPO> <NUMBER>
   ```

## Create A Pull Request

1. Check local branch and remote:
   ```bash
   git status --short
   git branch --show-current
   git remote -v
   ```
2. Push the branch if needed:
   ```bash
   git push -u origin <BRANCH>
   ```
3. Create the PR:
   ```bash
   gitee pr create <OWNER> <REPO> "<TITLE>" --head <BRANCH> --base <BASE> --body "<BODY>"
   ```
4. Verify with:
   ```bash
   gitee pr list <OWNER> <REPO>
   ```

## Review Or Update A Pull Request

```bash
gitee pr-ext detail <OWNER> <REPO> <NUMBER>
gitee pr-ext list-comments <OWNER> <REPO> <NUMBER>
gitee pr-ext diff-files <OWNER> <REPO> <NUMBER>
```

Use comments for review feedback:

```bash
gitee pr-ext comment <OWNER> <REPO> <NUMBER> "<BODY>"
```

Merging or closing a PR changes remote state. Confirm before:

```bash
gitee pr merge <OWNER> <REPO> <NUMBER>
gitee pr close <OWNER> <REPO> <NUMBER>
```

## Publish A Release

1. Check existing releases and tags:
   ```bash
   gitee releases list <OWNER> <REPO>
   git tag --list
   ```
2. Confirm release name, tag, and notes.
3. Create:
   ```bash
   gitee releases create <OWNER> <REPO> <TAG_NAME> "<NAME>" --body "<BODY>"
   ```
4. Verify by listing releases again.

## Manage Labels

List before changing:

```bash
gitee labels list <OWNER> <REPO>
```

Create or update:

```bash
gitee labels create <OWNER> <REPO> bug FF0000 --description "Bug 问题"
gitee labels update <OWNER> <REPO> bug --color FF5500
```

Confirm before deletion:

```bash
gitee labels delete <OWNER> <REPO> bug
```
