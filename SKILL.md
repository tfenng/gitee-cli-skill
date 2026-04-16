---
description: 当项目的远程仓库为 gitee.com 而非github时，使用此 skill 调用 gitee 命令管理仓库、Issue、PR、Releases、wiki、labels、 notifications 等相关资源
origin: user
---

## AI Skill: Gitee CLI (`gitee`)

### 1. 前提条件

#### 认证与配置

在开始使用前，**必须**配置访问令牌。推荐使用环境变量：

- **设置 Token**：在 Gitee 网页端"设置 -> 私人令牌"中生成一个令牌。
  ```bash
  # Linux / macOS
  export GITEE_TOKEN="你的_令牌"
  # Windows (CMD)
  set GITEE_TOKEN="你的_令牌"
  ```
- **可选设置**：
  - `GITEE_API_BASE`: 默认 `https://gitee.com/api/v5`
  - `LANG`: 中英文界面切换，`zh_CN.UTF-8` 为中文，`en` 为英文

### 2. 全局命令

```bash
gitee [OPTIONS] <COMMAND>

Options:
      --lang <LANG>  Language for help (en, zh) [env: GITEE_LANG=]
  -h, --help         打印帮助
  -V, --version      打印版本
```

### 3. 仓库管理 (`repo`)

#### 3.1 基本仓库管理 (`repo`)

##### repo list - 列出授权仓库
```bash
gitee repo list
```

##### repo create - 创建新仓库
```bash
gitee repo create [OPTIONS] <NAME>

Arguments:
  <NAME>  仓库名称

Options:
      --description <DESCRIPTION>  仓库描述（可选）
      --private                      是否私有
  -h, --help                         打印帮助
```

**示例：**
```bash
gitee repo create my-project --description "我的项目" --private
```

##### repo info - 查看仓库详情
```bash
gitee repo info <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

**示例：**
```bash
gitee repo info BearTony my-project
```

##### repo delete - 删除仓库
```bash
gitee repo delete <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

#### 3.2 扩展仓库管理 (`repo-ext`)

##### repo-ext fork - Fork 仓库
```bash
gitee repo-ext fork <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

##### repo-ext star - 收藏仓库
```bash
gitee repo-ext star <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

##### repo-ext unstar - 取消收藏
```bash
gitee repo-ext unstar <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

##### repo-ext watch - 关注仓库
```bash
gitee repo-ext watch <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

##### repo-ext unwatch - 取消关注
```bash
gitee repo-ext unwatch <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

### 4. Issue 管理 (`issues`)

#### 4.1 基本 Issue 管理 (`issues`)

##### issues list - 列出 Issue
```bash
gitee issues list [OWNER] [REPO]

Arguments:
  [OWNER]  仓库所有者（可选，不提供则列出所有 Issue）
  [REPO]   仓库名称（可选）
```

##### issues create - 创建 Issue
```bash
gitee issues create [OPTIONS] <OWNER> <REPO> <TITLE>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
  <TITLE>  Issue 标题

Options:
  -b, --body <BODY>  Issue 内容
  -h, --help         打印帮助
```

**示例：**
```bash
gitee issues create BearTony my-project "Bug报告：登录失败" --body "复现步骤：..."
```

##### issues close - 关闭 Issue
```bash
gitee issues close <OWNER> <REPO> <NUMBER>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  Issue 编号
```

#### 4.2 扩展 Issue 管理 (`issues-ext`)

##### issues-ext detail - 查看 Issue 详情
```bash
gitee issues-ext detail <OWNER> <REPO> <NUMBER>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  Issue 编号
```

##### issues-ext update - 更新 Issue
```bash
gitee issues-ext update [OPTIONS] <OWNER> <REPO> <NUMBER>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  Issue 编号

Options:
      --title <TITLE>    新标题
      --body <BODY>      新内容
      --state <STATE>    新状态 (open/closed)
  -h, --help             打印帮助
```

##### issues-ext comment - 为 Issue 添加评论
```bash
gitee issues-ext comment <OWNER> <REPO> <NUMBER> <BODY>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  Issue 编号
  <BODY>    评论内容
```

##### issues-ext list-comments - 列出 Issue 评论
```bash
gitee issues-ext list-comments <OWNER> <REPO> <NUMBER>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  Issue 编号
```

##### issues-ext milestone-list - 列出里程碑
```bash
gitee issues-ext milestone-list [OPTIONS] <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称

Options:
      --state <STATE>  里程碑状态
  -h, --help            打印帮助
```

##### issues-ext milestone-create - 创建里程碑
```bash
gitee issues-ext milestone-create [OPTIONS] <OWNER> <REPO> <TITLE>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
  <TITLE>  里程碑标题

Options:
      --description <DESCRIPTION>  里程碑描述
      --due-on <DUE_ON>            截止日期 (ISO 8601 格式)
  -h, --help                       打印帮助
```

### 5. 拉取请求管理 (`pr`)

#### 5.1 基本 PR 管理 (`pr`)

##### pr list - 列出 Pull Request
```bash
gitee pr list <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

##### pr create - 创建 Pull Request
```bash
gitee pr create [OPTIONS] <OWNER> <REPO> <TITLE>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
  <TITLE>  PR 标题

Options:
      --head <HEAD>     源分支 [默认: main]
      --base <BASE>     目标分支 [默认: master]
  -b, --body <BODY>      PR 描述
  -h, --help             打印帮助
```

**示例：**
```bash
gitee pr create BearTony my-project "添加新功能" --head feature-branch --base main --body "实现详情..."
```

##### pr close - 关闭 Pull Request
```bash
gitee pr close <OWNER> <REPO> <NUMBER>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  PR 编号
```

##### pr merge - 合并 Pull Request
```bash
gitee pr merge <OWNER> <REPO> <NUMBER>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  PR 编号
```

#### 5.2 扩展 PR 管理 (`pr-ext`)

##### pr-ext detail - 查看 PR 详情
```bash
gitee pr-ext detail <OWNER> <REPO> <NUMBER>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  PR 编号
```

##### pr-ext update - 更新 Pull Request
```bash
gitee pr-ext update [OPTIONS] <OWNER> <REPO> <NUMBER>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  PR 编号

Options:
      --title <TITLE>    新标题
      --body <BODY>      新描述
      --state <STATE>    新状态 (open/closed)
  -h, --help              打印帮助
```

##### pr-ext comment - 为 PR 添加评论
```bash
gitee pr-ext comment <OWNER> <REPO> <NUMBER> <BODY>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  PR 编号
  <BODY>    评论内容
```

##### pr-ext list-comments - 列出 PR 评论
```bash
gitee pr-ext list-comments <OWNER> <REPO> <NUMBER>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  PR 编号
```

##### pr-ext diff-files - 获取 PR 的差异文件
```bash
gitee pr-ext diff-files <OWNER> <REPO> <NUMBER>

Arguments:
  <OWNER>   仓库所有者
  <REPO>    仓库名称
  <NUMBER>  PR 编号
```

### 6. 标签管理 (`labels`)

##### labels list - 列出仓库标签
```bash
gitee labels list <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

##### labels create - 创建标签
```bash
gitee labels create [OPTIONS] <OWNER> <REPO> <NAME> <COLOR>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
  <NAME>   标签名称
  <COLOR>  标签颜色 (十六进制格式，如 FF0000)

Options:
  -d, --description <DESCRIPTION>  标签描述（可选）
  -h, --help                       打印帮助
```

**示例：**
```bash
gitee labels create BearTony my-project bug FF0000 --description "Bug 标签"
```

##### labels update - 更新标签
```bash
gitee labels update [OPTIONS] <OWNER> <REPO> <NAME>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
  <NAME>   当前标签名称

Options:
      --new-name <NEW_NAME>        新名称
      --color <COLOR>              新颜色
      --description <DESCRIPTION>  新描述
  -h, --help                       打印帮助
```

##### labels delete - 删除标签
```bash
gitee labels delete <OWNER> <REPO> <NAME>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
  <NAME>   标签名称
```

### 7. 用户管理 (`user`)

##### user info - 获取用户信息
```bash
gitee user info [USERNAME]

Arguments:
  [USERNAME]  用户名（可选，不提供则获取当前认证用户）
```

##### user search - 搜索用户
```bash
gitee user search <QUERY>

Arguments:
  <QUERY>  搜索关键词
```

### 8. 通知管理 (`notifications`)

##### notifications list - 列出通知
```bash
gitee notifications list
```

### 9. 文件管理 (`files`)

##### files get - 获取文件内容
```bash
gitee files get <OWNER> <REPO> <PATH>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
  <PATH>   文件路径
```

##### files list - 列出仓库文件
```bash
gitee files list [OPTIONS] <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称

Options:
      --path <PATH>  目录路径（可选）
  -h, --help         打印帮助
```

##### files search - 搜索文件内容
```bash
gitee files search [OPTIONS] <QUERY>

Arguments:
  <QUERY>  搜索关键词

Options:
      --owner <OWNER>  限定所有者（可选）
  -h, --help           打印帮助
```

### 10. 版本发布管理 (`releases`)

##### releases list - 列出版本
```bash
gitee releases list <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

##### releases create - 创建版本
```bash
gitee releases create [OPTIONS] <OWNER> <REPO> <TAG_NAME> <NAME>

Arguments:
  <OWNER>     仓库所有者
  <REPO>      仓库名称
  <TAG_NAME>  Git 标签名
  <NAME>      版本名称

Options:
  -b, --body <BODY>  版本描述
  -h, --help         打印帮助
```

**示例：**
```bash
gitee releases create BearTony my-project v1.0.0 "版本 1.0.0" --body "首发版本"
```

### 11. Wiki 管理 (`wiki`)

##### wiki list - 列出 Wiki 页面
```bash
gitee wiki list <OWNER> <REPO>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
```

##### wiki get - 获取 Wiki 页面
```bash
gitee wiki get <OWNER> <REPO> <SLUG>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
  <SLUG>   页面 slug（URL 标识）
```

##### wiki create - 创建 Wiki 页面
```bash
gitee wiki create <OWNER> <REPO> <TITLE> <BODY>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
  <TITLE>  页面标题
  <BODY>   页面内容（Markdown）
```

##### wiki delete - 删除 Wiki 页面
```bash
gitee wiki delete <OWNER> <REPO> <SLUG>

Arguments:
  <OWNER>  仓库所有者
  <REPO>   仓库名称
  <SLUG>   页面 slug（URL 标识）
```

### 12. 最佳实践

1. **指令优先**：当用户提出与 Gitee 交互的请求时，优先使用 `gitee` 命令解决，其次是网页操作。
2. **安全先行**：在执行任何操作前，检查环境变量 `GITEE_TOKEN` 是否已设置。
3. **步骤拆解**：对于复杂任务（如完整的 PR 工作流），将其分解为 `fork` -> `clone` -> `commit` -> `push` -> `pr create` 等步骤执行。
4. **善用帮助**：如果忘记具体子命令，运行 `gitee <子命令> --help` 获取帮助。
5. **路径完整**：在涉及 `--repo` 参数时，使用 `owner/repo-name` 的格式。

### 13. 常见工作流示例

#### 创建 Issue 并指派
```bash
# 1. 查看仓库信息
gitee repo info BearTony my-project

# 2. 创建 Issue
gitee issues create BearTony my-project "功能请求：添加导出功能" --body "希望添加导出为 CSV 的功能"

# 3. 查看 Issue
gitee issues-ext detail BearTony my-project 1
```

#### 完整 PR 工作流
```bash
# 1. Fork 仓库
gitee repo-ext fork original-owner original-repo

# 2. 克隆本地（需手动配置 git remote）
git clone https://gitee.com/your-name/original-repo.git
cd original-repo
git remote add upstream https://gitee.com/original-owner/original-repo.git

# 3. 创建特性分支
git checkout -b feature-branch

# 4. 提交代码
git add .
git commit -m "feat: add new feature"

# 5. 推送分支
git push -u origin feature-branch

# 6. 创建 PR
gitee pr create BearTony my-project "添加新功能" --head feature-branch --base main --body "实现了..."

# 7. 添加 PR 评论
gitee pr-ext comment BearTony my-project 1 "代码审查建议：..."

# 8. 合并 PR
gitee pr merge BearTony my-project 1
```

#### 管理标签
```bash
# 1. 列出仓库标签
gitee labels list BearTony my-project

# 2. 创建标签
gitee labels create BearTony my-project bug FF0000 --description "Bug 问题"

# 3. 更新标签颜色
gitee labels update BearTony my-project bug --color "FF5500"

# 4. 删除标签
gitee labels delete BearTony my-project bug
```
