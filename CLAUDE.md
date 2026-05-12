# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 概述

这是一个 Claude Code Skill 仓库，用于为 AI 编码助手提供 `gitee-cli` 工具的使用指导。当项目的远程仓库是 gitee.com 时，使用此 skill 来管理仓库、Issue、PR 等资源。

## 目录结构

- `SKILL.md` — 技能入口文件，定义触发条件、agent 工作流和安全规则
- `references/command-reference.md` — `gitee` 子命令速查
- `references/workflows.md` — Issue、PR、Release 等常见任务流程
- `references/troubleshooting.md` — 认证、权限、远程地址等排错指南
- `agents/openai.yaml` — skill UI 元数据
- `README.md` — 安装与使用说明

## 环境要求

- Rust 环境（`cargo` 包管理器）
- 安装 `gitee-cli`：```bash
  cargo install gitee-cli
  ```

## 认证配置

必须设置 `GITEE_TOKEN` 环境变量（在 Gitee 网页端"设置 -> 私人令牌"生成）：
```bash
export GITEE_TOKEN="你的令牌"
```

## 常用命令

```bash
gitee repo list|create|info|delete
gitee issues list|create|close
gitee issues-ext detail|update|comment|list-comments
gitee pr list|create|close|merge
gitee pr-ext detail|update|comment|list-comments|diff-files
gitee files|releases|wiki|labels|notifications|user
```

## 注意事项

- 优先通过 `git remote -v` 判断当前仓库是否托管在 gitee.com
- 多数 `gitee` 命令使用分离的 `<OWNER> <REPO>` 参数；仅在命令明确要求时使用 `owner/repo-name`
- 复杂任务（如完整 PR 工作流）应分解为多个步骤执行
- 运行 `gitee <子命令> --help` 获取详细帮助
- 删除、关闭、合并等远程状态变更操作前，先向用户确认目标与意图
