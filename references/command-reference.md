# Gitee CLI Command Reference

Use this file when exact `gitee` syntax is needed. Prefer checking `gitee <subcommand> --help` if the installed CLI version may differ.

## Global

```bash
gitee [OPTIONS] <COMMAND>
gitee --version
gitee --lang zh <COMMAND>
```

Environment:

- `GITEE_TOKEN`: required for authenticated API operations.
- `GITEE_API_BASE`: optional API base, default `https://gitee.com/api/v5`.
- `GITEE_LANG`: optional help language, usually `zh` or `en`.

## Repository

```bash
gitee repo list
gitee repo create <NAME> --description "<DESCRIPTION>" --private
gitee repo info <OWNER> <REPO>
gitee repo delete <OWNER> <REPO>
```

Extended repository operations:

```bash
gitee repo-ext fork <OWNER> <REPO>
gitee repo-ext star <OWNER> <REPO>
gitee repo-ext unstar <OWNER> <REPO>
gitee repo-ext watch <OWNER> <REPO>
gitee repo-ext unwatch <OWNER> <REPO>
```

## Issues

```bash
gitee issues list [OWNER] [REPO]
gitee issues create <OWNER> <REPO> "<TITLE>" --body "<BODY>"
gitee issues close <OWNER> <REPO> <NUMBER>
```

Extended issue operations:

```bash
gitee issues-ext detail <OWNER> <REPO> <NUMBER>
gitee issues-ext update <OWNER> <REPO> <NUMBER> --title "<TITLE>" --body "<BODY>" --state open
gitee issues-ext update <OWNER> <REPO> <NUMBER> --state closed
gitee issues-ext comment <OWNER> <REPO> <NUMBER> "<BODY>"
gitee issues-ext list-comments <OWNER> <REPO> <NUMBER>
gitee issues-ext milestone-list <OWNER> <REPO> --state open
gitee issues-ext milestone-create <OWNER> <REPO> "<TITLE>" --description "<DESCRIPTION>" --due-on "2026-12-31"
```

## Pull Requests

```bash
gitee pr list <OWNER> <REPO>
gitee pr create <OWNER> <REPO> "<TITLE>" --head <HEAD_BRANCH> --base <BASE_BRANCH> --body "<BODY>"
gitee pr close <OWNER> <REPO> <NUMBER>
gitee pr merge <OWNER> <REPO> <NUMBER>
```

Extended PR operations:

```bash
gitee pr-ext detail <OWNER> <REPO> <NUMBER>
gitee pr-ext update <OWNER> <REPO> <NUMBER> --title "<TITLE>" --body "<BODY>" --state open
gitee pr-ext comment <OWNER> <REPO> <NUMBER> "<BODY>"
gitee pr-ext list-comments <OWNER> <REPO> <NUMBER>
gitee pr-ext diff-files <OWNER> <REPO> <NUMBER>
```

## Labels

```bash
gitee labels list <OWNER> <REPO>
gitee labels create <OWNER> <REPO> <NAME> <COLOR> --description "<DESCRIPTION>"
gitee labels update <OWNER> <REPO> <NAME> --new-name <NEW_NAME> --color <COLOR> --description "<DESCRIPTION>"
gitee labels delete <OWNER> <REPO> <NAME>
```

Use six-character hex colors without `#`, for example `FF0000`.

## Users And Notifications

```bash
gitee user info
gitee user info <USERNAME>
gitee user search <QUERY>
gitee notifications list
```

## Files

```bash
gitee files get <OWNER> <REPO> <PATH>
gitee files list <OWNER> <REPO> --path <PATH>
gitee files search <QUERY> --owner <OWNER>
```

## Releases

```bash
gitee releases list <OWNER> <REPO>
gitee releases create <OWNER> <REPO> <TAG_NAME> "<NAME>" --body "<BODY>"
```

Example:

```bash
gitee releases create owner my-project v1.0.0 "版本 1.0.0" --body "首发版本"
```

## Wiki

```bash
gitee wiki list <OWNER> <REPO>
gitee wiki get <OWNER> <REPO> <SLUG>
gitee wiki create <OWNER> <REPO> "<TITLE>" "<BODY>"
gitee wiki delete <OWNER> <REPO> <SLUG>
```

Deletion is destructive; confirm with the user before running it.
