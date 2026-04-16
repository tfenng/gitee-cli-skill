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
  - "创建一个 issues，仅 title:gitee-cli 测试成功"
  - "为刚才提交的分支创建一个 PR"
  - "创建一个新的 release"
