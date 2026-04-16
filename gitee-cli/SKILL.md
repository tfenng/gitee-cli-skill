## 🧠 AI Skill: Gitee CLI (`gitee`)

> Gitee CLI (Rust版) 是码云（Gitee）的非官方命令行工具，通过 API 高效管理仓库、Issue、PR 等资源。此技能专为 AI 编码助手设计，用于指导其使用该工具完成开发任务。

### 1. 环境要求与安装

#### 前提条件
- **Rust 环境**：需要安装 Rust，因为它包含了 `cargo` 包管理器。
- **安装命令**：
  ```bash
  cargo install gitee-cli
  ```
- **验证安装**：
  ```bash
  gitee --version
  ```

#### 认证与配置

在开始使用前，**必须**配置访问令牌。推荐使用环境变量：

- **设置 Token**：在 Gitee 网页端“设置 -> 私人令牌”中生成一个令牌。
  ```bash
  # Linux / macOS
  export GITEE_TOKEN="你的_令牌"
  # Windows (CMD)
  set GITEE_TOKEN="你的_令牌"
  ```
- **可选设置**：
  - `GITEE_API_BASE`: 默认 `https://gitee.com/api/v5`
  - `LANG`: 中英文界面切换，`zh_CN.UTF-8` 为中文

### 2. 核心命令参考

#### 仓库管理 (`repo`)
- `gitee repo list`：列出仓库。
- `gitee repo create --name <repo>`：创建新仓库。
- `gitee repo view [<repository>]`：查看仓库详情。
- `gitee repo delete <repo>`：删除仓库。
- `gitee repo fork <repo>`：Fork 仓库。
- `gitee repo search <keyword>`：全站搜索仓库。

#### Issue 管理 (`issues`)
- `gitee issues list`：列出 Issue。
- `gitee issues create`：创建新 Issue。
- `gitee issues view <number>`：查看 Issue 详情。
- `gitee issues comment <number>`：为 Issue 添加评论。
- `gitee issues close <number>`：关闭 Issue。

#### 拉取请求管理 (`pr`)
- `gitee pr list`：列出 Pull Request。
- `gitee pr create`：创建新 PR。
- `gitee pr view <number>`：查看 PR 详情。
- `gitee pr checkout <number>`：在本地检出一个 PR 进行测试。
- `gitee pr comment <number>`：为 PR 添加评论。
- `gitee pr merge <number>`：合并 PR。
- `gitee pr close <number>`：关闭 PR。

#### 其他重要命令
- `gitee files`：管理仓库文件（读/树/代码搜索）。
- `gitee releases`：管理版本发布。
- `gitee wiki`：管理 Wiki。
- `gitee labels`：管理标签。
- `gitee notifications`：获取通知。
- `gitee user`：管理用户信息。

### 3. 最佳实践

1. **指令优先**：当用户提出与 Gitee 交互的请求时，优先使用 `gitee` 命令解决，其次是网页操作。
2. **安全先行**：在执行任何操作前，检查环境变量 `GITEE_ACCESS_TOKEN` 是否已设置。
3. **步骤拆解**：对于复杂任务（如完整的 PR 工作流），将其分解为 `fork` -> `clone` -> `commit` -> `push` -> `pr create` 等步骤执行。
4. **善用帮助**：如果忘记具体子命令，建议用户运行 `gitee <子命令> --help` 获取帮助。
5. **路径完整**：在涉及 `--repo` 参数时，使用 `owner/repo-name` 的格式。

### 4. 补充信息与常见问题

- **社区驱动**：`gitee-cli` 是第三方工具，非官方出品。
- **错误排查**：遇到问题时，可以检查网络或 API 令牌权限，必要时可在官网查看 API 限制。
- **获取更多帮助**：更多高级用法可查阅[项目文档](https://docs.rs/crate/gitee-cli/0.9.0)。
- **高级集成**：该工具可作为 MCP 服务器，与 AI 环境集成，详见 `gitee install` 命令。

