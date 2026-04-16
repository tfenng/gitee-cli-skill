# Gitee CLi Skill

Gitee CLI (Rust版) 是码云（Gitee）的非官方命令行工具，通过 API 高效管理仓库、Issue、PR 等资源。
此技能专为 AI 编码助手设计，用于指导其使用该工具完成开发任务。

## 前置依赖

### Rust & Cargo 安装

详见 [cargo.md](./cargo.md)

### 安装 Gitee CLI

- **安装命令**：
  ```bash
  cargo install gitee-cli
  ```
- **验证安装**：
  ```bash
  gitee --version
  ```

## 此 skill 在 Claude 中的安装

```bash
git clone https://github.com/tfenng/gitee-cli-skill.git ~/.claude/skills/gitee-cli
```

验证安装：
进入claude 后
/skills # 列表中应出现 gitee-cli

## 使用说明

- **设置本机的环境变量**
  ### Linux / macOS
  ```bash
  export GITEE_TOKEN="你的_令牌"
  ```
  ### Windows (CMD)
  ```cmd
  set GITEE_TOKEN="你的_令牌"
  ```

- **重启 claude 后验证**：

  gitee.com上的远程库的关联资源操作，提示词示例：
  - "此项目的远程仓库还关联有哪些待办issues"
  - "创建一个 issues，仅 title:gitee-cli 测试成功"
  - "为刚才提交的分支创建一个 PR"
  - "创建一个新的 release"


## gitee-cli的补充信息与常见问题

- **社区驱动**：`gitee-cli` 是第三方工具，非官方出品。
- **错误排查**：遇到问题时，可以检查网络或 API 令牌权限，必要时可在官网查看 API 限制。
- **获取更多帮助**：更多高级用法可查阅[项目文档](https://docs.rs/crate/gitee-cli/0.9.0)。
- **高级集成**：该工具可作为 MCP 服务器，与 AI 环境集成，详见 `gitee install` 命令。