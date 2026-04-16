# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 概述

这是一个 Claude Code Skill 仓库，用于为 AI 编码助手提供 `gitee-cli` 工具的使用指导。当项目的远程仓库是 gitee.com 时，使用此 skill 来管理仓库、Issue、PR 等资源。

## 目录结构

- `gitee-cli/SKILL.md` — Claude Code 技能定义文件，定义 gitee 命令的使用方式
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
gitee repo list|create|view|delete|fork|search
gitee issues list|create|view|comment|close
gitee pr list|create|view|checkout|comment|merge|close
gitee files|releases|wiki|labels|notifications|user
```

## 注意事项

- 涉及 `--repo` 参数时，使用 `owner/repo-name` 格式
- 复杂任务（如完整 PR 工作流）应分解为多个步骤执行
- 运行 `gitee <子命令> --help` 获取详细帮助
