<div align="center">
  
<h2 id="claude-code-community-guide">Claude代码指南</h2>

*更新和贡献请访问[官方Claude代码文档](https://claude.ai/code)*

![Claude Code](https://img.shields.io/npm/v/@anthropic-ai/claude-code?label=Claude%20Code&logo=anthropic)
[![状态](https://img.shields.io/badge/Status-活跃中-brightgreen)](https://github.com/anthropics/claude-code)
[![许可证](https://img.shields.io/badge/License-Anthropic-orange)](https://claude.ai/code)


</div>

<div align="center">

<kbd>

| 章节                                    | 状态          |
|---------------------------------------------|------------------------------|
| Windows、Linux、MacOS安装指南 | ✅ |
| 技巧和小窍门                            | ✅ |
| MCP概述及使用方法              | ✅ |
| 社区指南                           | ✅ |
| 故障排除                            | ✅ |
| 最优使用Claude代码的方法| ✅ |

### 通过Discord使用Claude代码[点击这里!](https://github.com/zebbern/claude-code-discord)


</kbd>

#### [点击查看每日更新整理的Claude变更日志和新闻](https://github.com/zebbern/claude-code-guide/tree/main/Official%20Claude%20Releases)

</div>

---

<h3 id="content">目录</h3>

_快速链接:_ [安装](#quick-start) · [命令](#claude-commands) · [快捷键](#keyboard-shortcuts) · [MCP](#mcp-integration) · [故障排除](#help--troubleshooting)

- **[入门指南](#getting-started)**
  - [快速开始](#quick-start)
  - [初始设置](#initial-setup)

- **[配置与环境](#configuration--environment)**
  - [环境变量](#environment-variables)
  - [配置文件](#configuration-files)

- **[命令与使用](#commands--usage)**
  - [Claude命令](#claude-commands)
  - [速查表](#cheat-sheet)

- **[界面与输入](#interface--input)**
  - [键盘快捷键](#keyboard-shortcuts)
  - [Vim模式](#vim-mode)

- **[高级功能](#advanced-features)**
  - [子代理](#sub-agents)
  - [MCP集成](#mcp-integration)
  - [钩子系统](#hooks-system)

- **[安全与权限](#security--permissions)**
  - [危险模式](#dangerous-mode)
  - [安全最佳实践](#security-best-practices-main)

- **[自动化与集成](#automation--integration)**
  - [自动化与脚本](#automation--scripting-with-claude-code)
  - [自动PR审查](#auto-pr-review-inline-comments)
  - [问题分类](#issue-triage-suggest-labels--severity)

- **[帮助与故障排除](#help--troubleshooting)**
  - [安装问题](#installation--nodejs-issues)
  - [MCP问题](#mcp-model-context-protocol-issues)
  - [最佳实践](#best-practices)

- **[第三方集成](#third-party-integrations)**
  - [DeepSeek集成](#deepseek-integration)


---

<h1 id="getting-started">入门指南</h1>

**当Claude完成任务时启用声音提示:**
> 
> <kbd>claude config set --global preferredNotifChannel terminal_bell</kbd>
<h2 id="quick-start">快速开始</h2>

> [!TIP]
> **在终端中输入<mark>claude</mark>或<mark>npx claude</mark>来启动界面**
>
> **遇到问题请前往[帮助与故障排除](#help--troubleshooting)解决...**
```C
# Node.js 18+⭐️              
/*Universal Method       */ npm install -g @anthropic-ai/claude-code
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Windows
/* Via CMD               */ npm install -g @anthropic-ai/claude-code
/* Via Powershell        */ irm https://claude.ai/install.ps1 | iex
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# WSL/GIT
/* Via Terminal          */ npm install -g @anthropic-ai/claude-code
/* Via Terminal          */ curl -fsSL https://claude.ai/install.sh | bash
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# MacOS                  */ brew install node && npm install -g @anthropic-ai/claude-code
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Linux 
/* Via Terminal          */ sudo apt update && sudo apt install -y nodejs npm
/* Via Terminal          */ npm install -g @anthropic-ai/claude-code
/* Via Terminal          */ curl -fsSL https://claude.ai/install.sh | bash
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Arch                     
/* Via Terminal          */ yay -S claude-code*/ 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Docker 
/* Windows (CMD)         */ docker run -it --rm -v "%cd%:/workspace" -e ANTHROPIC_API_KEY="sk-your-key" node:20-slim bash -lc "npm i -g @anthropic-ai/claude-code && cd /workspace && claude"
/* macOS/Linux (bash/zsh)*/ docker run -it --rm -v "$PWD:/workspace" -e ANTHROPIC_API_KEY="sk-your-key" node:20-slim bash -lc 'npm i -g @anthropic-ai/claude-code && cd /workspace && claude'
/* No bash Fallback      */ docker run -it --rm -v "$PWD:/workspace" -e ANTHROPIC_API_KEY="sk-your-key" node:20-slim sh -lc 'npm i -g @anthropic-ai/claude-code && cd /workspace && claude'
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Check if claude is installed correctly
/* Linux                 */ which claude 
/* Windows               */ where claude
/* Universal             */ claude --version
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Common Management
/*claude config          */ Configure settings
/*claude mcp list        */ Setup MCP servers, you can also replace "list" with add/remove
/*claude /agents         */ Configure/Setup Subagents for different tasks
/*claude update          */ Update to latest
```

---

> [!Tip]
> <ins>**Open Project Via Terminal Into VS Code / Cursor**</ins>
>  ### $ - <kbd>cd /path/to/project</kbd>
>  ### $ - <kbd>code .</kbd>
> 
**Make sure you have the <mark>(Claude Code extension)</mark> installed in your VS Code / Cursor**

---

<h2 id="system-requirements">系统要求</h2>

> - 操作系统: macOS 10.15+, Ubuntu 20.04+/Debian 10+, 或 Windows 10/11 或 WSL

> - 硬件: 最低4GB内存，推荐8GB以上

> - 软件: Node.js 18+ 或 git 2.23+ (可选) & GitHub或GitLab CLI用于PR工作流(可选)

> - 网络: API调用需要网络连接

> - Node.js 18+


---

<h2 id="initial-setup">初始设置</h2>

> [!Tip]
> **从[Anthropic控制台](https://console.anthropic.com)获取API密钥**
>
> **不要提交真实密钥，请使用git忽略的文件、操作系统密钥存储或密钥管理器**
```C
# 通用方法
/* 开始登录流程                    */ claude /login
/* 设置长期有效的认证令牌  */ claude setup-token
----------------------------------------------------------------------------------------------------------------------------------
# Windows
/* 设置API密钥        */ set ANTHROPIC_API_KEY=sk-your-key-here-here
/* cmd掩码检查   */ echo OK: %ANTHROPIC_API_KEY:~0,8%***
/* 设置持久密钥 */ setx ANTHROPIC_API_KEY "sk-your-key-here-here"
/* cmd取消设置密钥      */ set ANTHROPIC_API_KEY=
----------------------------------------------------------------------------------------------------------------------------------
# Linux
/* 设置API密钥        */ export ANTHROPIC_API_KEY="sk-your-key-here-here"
/* 掩码检查       */ echo "OK: ${ANTHROPIC_API_KEY:0:8}***"
/* 移除会话密钥     */ unset ANTHROPIC_API_KEY
----------------------------------------------------------------------------------------------------------------------------------
# Powershell
/* ps会话设置         */ $env:ANTHROPIC_API_KEY = "sk-your-key-here-here"
/* ps掩码检查    */ "OK: $($env:ANTHROPIC_API_KEY.Substring(0,8))***"
/* ps持久化设置         */ [Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY","sk-your-key-here-here","User") 
/* ps轮换密钥          */ $env:ANTHROPIC_API_KEY = "sk-new-key"
/* ps移除密钥          */ Remove-Item Env:\ANTHROPIC_API_KEY
----------------------------------------------------------------------------------------------------------------------------------
# Other...
# persist-bash/*      */ echo 'export ANTHROPIC_API_KEY="sk-your-key-here-here"' >> ~/.bashrc && source ~/.bashrc
# persist-zsh /*      */ echo 'export ANTHROPIC_API_KEY="sk-your-key-here-here"' >> ~/.zshrc  && source ~/.zshrc
# persist-fish/*      */ fish -lc 'set -Ux ANTHROPIC_API_KEY sk-your-key-here-here'
----------------------------------------------------------------------------------------------------------------------------------
```

---

<h1 id="configuration--environment">配置与环境</h1>

<h2 id="environment-variables">环境变量</h2>

> **您也可以在settings.json文件的"env"键下设置这些变量以实现自动应用。**

> [!Important] 
> **Windows用户请将<kbd>export</kbd>替换为<kbd>set</kbd>或<kbd>setx</kbd>以实现永久设置**
```bash
# 环境变量开关(放入~/.bashrc或~/.zshrc)
export ANTHROPIC_API_KEY="sk-your-key-here-here"      # 作为X-Api-Key头发送的API密钥(交互式使用: /login)
export ANTHROPIC_AUTH_TOKEN="my-auth-token"           # 自定义Authorization头; Claude会自动添加"Bearer "前缀
export ANTHROPIC_CUSTOM_HEADERS="X-Trace-Id: 12345"   # 额外的请求头(格式: "名称: 值")

export ANTHROPIC_MODEL="claude-sonnet-4-20250514"                # 自定义使用的模型名称
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-20250514" # 默认Sonnet模型别名
export ANTHROPIC_DEFAULT_OPUS_MODEL="claude-opus-4-20250514"     # 默认Opus模型别名
export ANTHROPIC_SMALL_FAST_MODEL="haiku-model"                  # 后台任务使用的Haiku类模型(占位符)
export ANTHROPIC_SMALL_FAST_MODEL_AWS_REGION="REGION"            # 覆盖Bedrock上小型/快速模型的AWS区域(占位符)

export AWS_BEARER_TOKEN_BEDROCK="bedrock_..."         # Amazon Bedrock API密钥/令牌用于认证

export BASH_DEFAULT_TIMEOUT_MS=60000                  # 长时间运行的bash命令的默认超时(毫秒)
export BASH_MAX_TIMEOUT_MS=300000                     # 长时间运行的bash命令允许的最大超时(毫秒)
export BASH_MAX_OUTPUT_LENGTH=20000                   # bash输出中间截断前的最大字符数

export CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR=1     # (0或1)每个Bash命令后返回原始项目目录
export CLAUDE_CODE_API_KEY_HELPER_TTL_MS=600000       # 使用apiKeyHelper时刷新凭证的间隔(毫秒)
export CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL=1            # (0或1)跳过IDE扩展的自动安装
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=4096             # 大多数请求的最大输出token数

export CLAUDE_CODE_USE_BEDROCK=1                      # (0或1)使用Amazon Bedrock
export CLAUDE_CODE_USE_VERTEX=0                       # (0或1)使用Google Vertex AI
export CLAUDE_CODE_SKIP_BEDROCK_AUTH=0                # (0或1)跳过Bedrock的AWS认证(例如通过LLM网关)
export CLAUDE_CODE_SKIP_VERTEX_AUTH=0                 # (0或1)跳过Vertex的Google认证(例如通过LLM网关)

export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=0     # (0或1)禁用非必要流量(等同于下面的DISABLE_*)
export CLAUDE_CODE_DISABLE_TERMINAL_TITLE=0           # (0或1)禁用自动终端标题更新

export DISABLE_AUTOUPDATER=0                          # (0或1)禁用自动更新(覆盖autoUpdates设置)
export DISABLE_BUG_COMMAND=0                          # (0或1)禁用/bug命令
export DISABLE_COST_WARNINGS=0                        # (0或1)禁用成本警告消息
export DISABLE_ERROR_REPORTING=0                      # (0或1)选择退出Sentry错误报告
export DISABLE_NON_ESSENTIAL_MODEL_CALLS=0            # (0或1)禁用非关键路径的模型调用
export DISABLE_TELEMETRY=0                            # (0或1)选择退出Statsig遥测

export HTTP_PROXY="http://proxy:8080"                 # HTTP代理服务器URL
export HTTPS_PROXY="https://proxy:8443"               # HTTPS代理服务器URL

export MAX_THINKING_TOKENS=0                          # (0或1开启/关闭)强制模型的思考预算
export MCP_TIMEOUT=120000                             # MCP服务器启动超时(毫秒)
export MCP_TOOL_TIMEOUT=60000                         # MCP工具执行超时(毫秒)
export MAX_MCP_OUTPUT_TOKENS=25000                    # MCP工具响应中允许的最大token数(默认25000)

export USE_BUILTIN_RIPGREP=0                          # (0 or 1) set 0 to use system-installed rg instead of bundled one

export VERTEX_REGION_CLAUDE_3_5_HAIKU="REGION"        # Region override for Claude 3.5 Haiku on Vertex AI
export VERTEX_REGION_CLAUDE_3_5_SONNET="REGION"       # Region override for Claude 3.5 Sonnet on Vertex AI
export VERTEX_REGION_CLAUDE_3_7_SONNET="REGION"       # Region override for Claude 3.7 Sonnet on Vertex AI
export VERTEX_REGION_CLAUDE_4_0_OPUS="REGION"         # Region override for Claude 4.0 Opus on Vertex AI
export VERTEX_REGION_CLAUDE_4_0_SONNET="REGION"       # Region override for Claude 4.0 Sonnet on Vertex AI
export VERTEX_REGION_CLAUDE_4_1_OPUS="REGION"         # Region override for Claude 4.1 Opus on Vertex AI
```

<h2 id="global-config-options">全局配置选项</h2>

```bash
claude config set -g theme dark                               # 主题: dark | light | light-daltonized | dark-daltonized
claude config set -g preferredNotifChannel iterm2_with_bell   # 通知渠道: iterm2 | iterm2_with_bell | terminal_bell | notifications_disabled
claude config set -g autoUpdates true                         # 自动下载并安装更新 (重启后生效)
claude config set -g verbose true                             # 显示完整的bash/命令输出

claude config set -g includeCoAuthoredBy false                # 在git提交/PR中省略 "co-authored-by Claude"
claude config set -g forceLoginMethod console                 # 限制登录到Anthropic控制台 (API计费)
claude config set -g model "claude-3-5-sonnet-20241022"       # 默认模型覆盖
claude config set -g statusLine '{"type":"command","command":"~/.claude/statusline.sh"}'  # 自定义状态行

claude config set -g enableAllProjectMcpServers true              # 自动批准.mcp.json中的所有MCP服务器
claude config set -g enabledMcpjsonServers '["memory","github"]'  # 批准特定的MCP服务器
claude config set -g disabledMcpjsonServers '["filesystem"]'      # 拒绝特定的MCP服务器
```
> [!Important] 
> **Windows用户请将<kbd>export</kbd>替换为<kbd>set</kbd>**
```bash
export DISABLE_AUTOUPDATER=1                      # 全局关闭自动更新 (覆盖autoUpdates设置)
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1 # 禁用非必要流量 (等同于下面的DISABLE_*开关)
export DISABLE_TELEMETRY=1                        # 选择退出Statsig遥测
export DISABLE_ERROR_REPORTING=1                  # 选择退出Sentry错误报告
export DISABLE_BUG_COMMAND=1                      # 禁用/bug命令
export DISABLE_COST_WARNINGS=0                    # 保留成本警告 (设置为1隐藏)
export DISABLE_NON_ESSENTIAL_MODEL_CALLS=1        # 跳过非关键模型调用 (例如，风格文本等)

export CLAUDE_CODE_DISABLE_TERMINAL_TITLE=1       # 停止自动更新终端标题
export CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR=1 # 每个Bash命令后返回原始项目目录
export CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL=1        # 跳过IDE扩展的自动安装
export USE_BUILTIN_RIPGREP=0                      # 使用系统 'rg' (0) 而不是捆绑的 'rg'

export MAX_THINKING_TOKENS=0                      # (0或1开启/关闭) 强制模型的思考预算
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=4096         # 限制典型响应大小 (示例值)

export HTTP_PROXY="http://proxy.company:8080"     # HTTP代理 (如果需要)
export HTTPS_PROXY="https://proxy.company:8443"   # HTTPS代理 (如果需要)
```

<h2 id="configuration-files">配置文件</h2>

**(内存类型) Claude Code 提供了四种内存位置，采用分层结构，每种用途不同:**

| 内存类型                | 位置                                                                                                                                                | 用途                                             | 使用场景示例                                                    | 共享对象                     |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- | -------------------------------------------------------------------- | ------------------------------- |
| **企业策略**      | macOS: `/Library/Application Support/ClaudeCode/CLAUDE.md`<br />Linux: `/etc/claude-code/CLAUDE.md`<br />Windows: `C:\ProgramData\ClaudeCode\CLAUDE.md` | 由IT/DevOps管理的全组织范围的指令 | 公司编码标准、安全策略、合规要求 | 组织内的所有用户       |
| **项目内存**         | `./CLAUDE.md`                                                                                                                                           | 团队共享的项目指令            | 项目架构、编码标准、常见工作流程             | 通过源代码控制的团队成员 |
| **用户内存**            | `~/.claude/CLAUDE.md`                                                                                                                                   | 个人偏好，适用于所有项目               | 代码风格偏好、个人工具快捷键                 | 仅你自己 (所有项目)         |
| **项目内存 (本地)** | `./CLAUDE.local.md`                                                                                                                                     | 个人项目特定偏好               | *(已弃用，见下文)* 你的沙盒URL、首选测试数据     | 仅你自己 (当前项目)      |

>所有内存文件在启动时会自动加载到Claude Code的上下文中。层级较高的文件优先加载，为更具体的内存提供基础。

---

<h1 id="commands--usage">命令与使用</h1>

<h2 id="claude-commands">Claude 命令</h2>

| 命令                   | 用途                                                                                                                                      |
| :------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------- |
| `/add-dir`                | 添加额外的工作目录                                                                                                           |
| `/agents`                 | 管理用于特定任务的自定义AI子代理                                                                                             | 
| `/bug`                    | 报告错误 (将对话发送给Anthropic)                                                                                                |
| `/clear`                  | 清除对话历史                                                                                                                   |
| `/compact [instructions]` | 使用可选的焦点指令压缩对话                                                                                        |
| `/config`                 | 查看/修改配置                                                                                                                    |
| `/cost`                   | 显示令牌使用统计和计费信息 |
| `/doctor`                 | 检查Claude Code安装的健康状况                                                                                           |
| `/help`                   | 获取使用帮助                                                                                                                               |
| `/init`                   | 使用CLAUDE.md指南初始化项目                                                                                                      |
| `/login`                  | 切换Anthropic账户                                                                                                                    |
| `/logout`                 | 从您的Anthropic账户注销                                                                                                         |
| `/mcp`                    | 管理MCP服务器连接和OAuth认证                                                                                       |
| `/memory`                 | 编辑CLAUDE.md内存文件                                                                                                                  |
| `/model`                  | 选择或更改AI模型                                                                                                                |
| `/permissions`            | 查看或更新工具权限 |
| `/pr_comments`            | 查看拉取请求评论                                                                                                                   |
| `/review`                 | 请求代码审查                                                                                                                          |
| `/status`                 | 查看账户和系统状态                                                                                                             |
| `/terminal-setup`         | 为换行符安装Shift+Enter键绑定 (仅限iTerm2和VSCode)                                                                        |
| `/vim`                    | 进入vim模式以交替插入和命令模式                                                                                      |

<h2 id="command-line-flags">命令行标志</h2>

| 标志 / 命令                             | 描述                                                                                                                                              | 示例                                                     |
| :----------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------- |
| `-d, --debug`                              | 启用调试模式 (显示详细的调试输出)。  | `claude -d -p "query"`                   |
| `--include-partial-messages`                | 通过CLI标志支持部分消息流式传输  |
| `--mcp-debug`                               | [已弃用] MCP调试模式 (显示MCP服务器错误)。请改用 `--debug`。                                                                             | `claude --mcp-debug`                                        |
| `--verbose`                                 | 覆盖配置中的详细模式设置 (显示扩展日志记录/逐行输出)。                                                                | `claude --verbose`                                          |
| `-p, --print`                               | 打印响应并退出 (适用于管道输出)。                                                                                                     | `claude -p "query"`                                         |
| `--output-format <format>`                  | 输出格式 (仅适用于 `--print`): `text` (默认), `json` (单个结果), 或 `stream-json` (实时流式传输)。                              | `claude -p "query" --output-format json`                    |
| `--input-format <format>`                   | 输入格式 (仅适用于 `--print`): `text` (默认) 或 `stream-json` (实时流式传输输入)。                                                  | `claude -p --output-format stream-json --input-format stream-json` |
| `--replay-user-messages`                    | 将stdin中的用户消息重新发送回stdout以进行确认 — **仅适用于** `--input-format=stream-json` **和** `--output-format=stream-json`。 | `claude --input-format stream-json --output-format stream-json --replay-user-messages` |
| `--allowedTools`, `--allowed-tools <tools...>`  | 允许的工具名称列表，以逗号/空格分隔 (例如 `"Bash(git:*) Edit"`)。                                                                           | `--allowed-tools "Bash(git:*)" Edit"`                       |
| `--disallowedTools`, `--disallowed-tools <tools...>` | 拒绝的工具名称列表，以逗号/空格分隔 (例如 `"Bash(git:*) Edit"`)。                                                                            | `--disallowed-tools "Edit"`                                 |
| `--mcp-config <configs...>`                 | 从JSON文件或字符串加载MCP服务器 (空格分隔)。                                                                                          | `claude --mcp-config ./mcp-servers.json`                    |
| `--strict-mcp-config`                       | 仅使用 `--mcp-config` 中的MCP服务器，忽略其他MCP配置。                                                                             | `claude --mcp-config ./a.json --strict-mcp-config`          |
| `--append-system-prompt <prompt>`           | 将系统提示附加到默认系统提示 (在打印模式下很有用)。                                                                              | `claude -p --append-system-prompt "Do X then Y"`            |
| `--permission-mode <mode>`                  | 会话的权限模式 (选项包括 `acceptEdits`, `bypassPermissions`, `default`, `plan`)。                                                 | `claude --permission-mode plan`                             |
| `--permission-prompt-tool <tool>`           | 指定一个MCP工具来处理非交互模式下的权限提示。                                                                               | `claude -p --permission-prompt-tool mcp_auth_tool "query"`  |
| `--fallback-model <model>`                  | 当默认模型过载时，启用自动回退到指定模型 (注意: 仅适用于 `--print`，请参阅帮助)。                                 | `claude -p --fallback-model claude-haiku-20240307 "query"`  |
| `--model <model>`                            | 当前会话的模型。接受别名，如 `sonnet`/`opus` 或完整的模型名称 (例如 `claude-sonnet-4-20250514`)。                               | `claude --model sonnet`                                     |
| `--settings <file-or-json>`                  | 从JSON文件或JSON字符串加载其他设置。                                                                                              | `claude --settings ./settings.json`                         |
| `--add-dir <directories...>`                 | 允许工具访问的额外目录。                                                                                                          | `claude --add-dir ../apps ../lib`                           |
| `--ide`                                      | 如果只有一个有效的IDE可用，则在启动时自动连接到IDE。                                                                        | `claude --ide`                                              |
| `-c, --continue`                             | 继续当前目录中最近的对话。                                                                                          | `claude --continue`                                         |
| `-r, --resume [sessionId]`                   | 恢复对话；提供会话ID或交互式选择一个。                                                                                 | `claude -r "abc123"`                                        |
| `--session-id <uuid>`                        | 为对话使用特定的会话ID (必须是有效的UUID)。                                                                                   | `claude --session-id 123e4567-e89b-12d3-a456-426614174000`  |
| `--dangerously-skip-permissions`             | Bypass all permission checks (only for trusted sandboxes).                                                                                               | `claude --dangerously-skip-permissions`                     |
| `-v, --version`                              | Show the installed `claude` CLI version.                                                                                                                 | `claude --version`                                          |
| `-h, --help`                                 | Display help / usage.                                                                                                                                     | `claude --help`                                             |


> The `--output-format json` flag is particularly useful for scripting and automation, allowing you to parse Claude's responses programmatically.

<h2 id="cheat-sheet">Cheat Sheet</h2>

```md
## Claude Cheat Sheet 
# Basics / interactive
claude                                 # Start interactive REPL
claude "explain this project"          # Start REPL seeded with a prompt
claude -p "summarize README.md"        # Non-interactive print mode (SDK-backed)
cat logs.txt | claude -p "explain"     # Pipe input to Claude and exit
claude -c                              # Continue most recent conversation (alias for --continue)
claude -r "<session-id>" "finish this" # Resume specific session by ID (alias for --resume)
claude --model claude-sonnet-4-20250514# Pick model for this run
claude --max-turns 3 -p "lint this"    # Cap agentic turns in print mode
claude --replay-user-messages          # Replay user messages to stdout for debugging / SDK workflows

# Update & install
claude update                          # Manually update Claude Code
claude doctor                          # Diagnose install/version & setup
claude install                         # Start native binary installer (beta)
claude migrate-installer               # Migrate from global npm to local installer

# Config: interactive wizard + direct ops
claude config                          # Interactive config wizard
claude config get <key>                # Get value (e.g., claude config get theme)
claude config set <key> <val>          # Set value (e.g., claude config set theme dark)
claude config add <key> <vals…>        # Append to array-type keys (e.g., claude config add env DEV=1)
claude config remove <key> <vals…>     # Remove items from list-type keys
claude config list                     # Show all current settings for project (project scope is default)

# Example project-scoped settings
claude config set model "claude-3-5-sonnet-20241022"   # Override default model for this project
claude config set includeCoAuthoredBy false            # Disable "co-authored-by Claude" byline in git/PRs
claude config set forceLoginMethod claudeai            # Restrict login flow: claudeai | console
claude config set enableAllProjectMcpServers true      # Auto-approve all MCP servers from .mcp.json
claude config set defaultMode "acceptEdits"            # Set default permission mode
claude config set disableBypassPermissionsMode disable # Prevent bypassPermissions mode (example key)

# Manage list settings (project scope)
claude config add enabledMcpjsonServers github         # Approve a specific MCP server from .mcp.json
claude config add enabledMcpjsonServers memory         # Add another
claude config remove enabledMcpjsonServers memory      # Remove one entry
claude config add disabledMcpjsonServers filesystem    # Explicitly reject a specific MCP server

# 全局范围（使用 -g 或 --global）
claude config set -g autoUpdates false                 # 全局关闭自动更新
claude config set --global preferredNotifChannel iterm2_with_bell
claude config set -g theme dark                        # 主题：dark | light | light-daltonized | dark-daltonized
claude config set -g verbose true                      # 在所有地方显示完整的 bash/命令输出
claude config get -g theme                             # 确认全局值

# MCP（模型上下文协议）管理
claude mcp                          # 启动 MCP 向导 / 配置 MCP 服务器
claude mcp list                     # 列出已配置的 MCP 服务器
claude mcp get <name>               # 显示服务器的详细信息
claude mcp remove <name>            # 移除服务器
claude mcp add <name> <command> [args...]                 # 添加本地 stdio 服务器
claude mcp add --transport sse <name> <url>               # 添加远程 SSE 服务器
claude mcp add --transport http <name> <url>              # 添加远程 HTTP 服务器
claude mcp add <name> --env KEY=VALUE -- <cmd> [args...]  # 向服务器命令传递环境变量
claude mcp add --transport sse private-api https://api.example/mcp \
  --header "Authorization: Bearer TOKEN"                  # 添加带有认证头的服务器
claude mcp add-json <name> '<json>'                       # 通过 JSON 块添加服务器
claude mcp add-from-claude-desktop                        # 从 Claude Desktop 导入服务器
claude mcp reset-project-choices                          # 重置对项目 .mcp.json 服务器的批准
claude mcp serve                                          # 将 Claude Code 本身作为 MCP stdio 服务器运行

# 其他有用的标志（打印 / SDK 模式）
claude --add-dir ../apps ../lib                     # 添加额外的工作目录
claude --allowedTools "Bash(git log:*)" "Read"      # 允许列出的工具而无需权限提示
claude --disallowedTools "Edit"                     # 禁止列出的工具而无需权限提示
claude --append-system-prompt "Custom instruction"  # 附加到系统提示（仅与 -p 一起使用）
claude -p "query" --output-format json --input-format stream-json  # 控制脚本的输入输出格式
claude --verbose                                    # 详细日志记录（逐轮）
claude --dangerously-skip-permissions               # 跳过权限提示（谨慎使用）

# 快速验证 / 注意事项
# - 项目范围是 'claude config' 的默认值；使用 -g/--global 影响所有项目。
# - 设置优先级：企业 > CLI 参数 > 本地项目 > 共享项目 > 用户 (~/.claude)。
# - 仅对列表类型键（例如 enabledMcpjsonServers）使用 'add' / 'remove'。
# - CLI 参考和发布说明是标志和最新添加的权威来源。
```

---

<h1 id="interface--input">Interface & Input</h1>

<h2 id="keyboard-shortcuts">Keyboard Shortcuts</h2>

| Shortcut         | Description                        | Context                    |
| :--------------- | :--------------------------------- | :------------------------- |
| `Ctrl+C`         | Cancel current input or generation | Standard interrupt         |
| `Ctrl+D`         | Exit Claude Code session           | EOF signal                 |
| `Ctrl+L`         | Clear terminal screen              | Keeps conversation history |
| `上/下箭头` | 导航命令历史记录           | 调用以前的输入     |
| `Esc` + `Esc`    | 编辑上一条消息              | 双击 Esc 进行修改    |

<h3 id="multiline-input">多行输入</h3>

| 方法           | 快捷键       | 上下文                           |
| :--------------- | :------------- | :-------------------------------- |
| 快速退出     | `\` + `Enter`  | 适用于所有终端            |
| macOS 默认    | `Option+Enter` | macOS 默认                  |
| 终端设置   | `Shift+Enter`  | `/terminal-setup` 后           |
| 控制序列 | `Ctrl+J`       | 多行输入的回车符 |
| 粘贴模式       | 直接粘贴 | 用于代码块、日志             |

<h3 id="quick-commands">快速命令</h3>

| 快捷键     | 描述                        | 注意事项                                                     |
| :----------- | :--------------------------------- | :-------------------------------------------------------- |
| `#` 开头 | 内存快捷方式添加到 CLAUDE.md | 提示文件选择                                |
| `/` 开头 | 斜杠命令                      |  

<h2 id="vim-mode">Vim 模式</h2>

> [!Note]
>  使用 `/vim` 命令启用 Vim 风格编辑，或通过 `/config` 永久配置。

<h3 id="vim-mode-switching">Vim 模式切换</h3>

| 命令 | 动作                      | 来自模式 |
| :------ | :-------------------------- | :-------- |
| `Esc`   | 进入 NORMAL 模式           | INSERT    |
| `i`     | 在光标前插入        | NORMAL    |
| `I`     | 在行首插入 | NORMAL    |
| `a`     | 在光标后插入         | NORMAL    |
| `A`     | 在行尾插入       | NORMAL    |
| `o`     | 在下方打开行             | NORMAL    |
| `O`     | 在上方打开行             | NORMAL    |

<h3 id="vim-navigation">Vim 导航</h3>

| 命令         | 动作                    |
| :-------------- | :------------------------ |
| `h`/`j`/`k`/`l` | 左/下/上/右移动   |
| `w`             | 下一个单词                 |
| `e`             | 单词末尾              |
| `b`             | 上一个单词             |
| `0`             | 行首         |
| `$`             | 行尾              |
| `^`             | 第一个非空白字符 |
| `gg`            | 输入开头        |
| `G`             | 输入末尾              |

<h3 id="vim-editing">Vim 编辑</h3>

| 命令        | 动作                  |
| :------------- | :---------------------- |
| `x`            | 删除字符        |
| `dd`           | 删除行             |
| `D`            | 删除到行尾   |
| `dw`/`de`/`db` | 删除单词/到末尾/向后 |
| `cc`           | 更改行             |
| `C`            | 更改到行尾   |
| `cw`/`ce`/`cb` | 更改单词/到末尾/向后 |
| `.`            | 重复上次更改      |

> [!Tip]
> 在终端设置中配置您偏好的换行行为。运行 `/terminal-setup` 为 iTerm2 和 VS Code 终端安装 Shift+Enter 绑定。

<h2 id="command-history">命令历史记录</h2>

> Claude Code 为当前会话维护命令历史记录：
```
* 历史记录按工作目录存储
* 使用 `/clear` 命令清除
* 使用上/下箭头导航（参见上面的键盘快捷键）
* **Ctrl+R**：在历史记录中反向搜索（如果终端支持）
* **注意**：历史扩展（`!`）默认禁用
```

---

<h1 id="advanced-features">高级功能</h1>

<h2 id="thinking-keywords">思考关键词</h2>

> [!Note]
> **通过在您的提示中添加以下关键词之一，为 Claude 争取额外的预回答规划时间。**
> **顺序（最低 → 最高）令牌消耗**
> <table><tr><td>
> 
> > **<kbd>think</kbd> -------------> 最低**
> 
> > **<kbd>think hard</kbd>**
> 
> > **<kbd>think harder</kbd>**
> 
> > **<kbd>ultrathink</kbd> --------> 最高**
> 
> </td></tr></table>

<h3 id="this-makes-claude-spend-more-time">这让 Claude 花费更多时间：</h3>

1. **Planning the solution**
2. #### breaking down steps
3. #### weighing alternatives/trade-offs
4. #### checking constraints & edge cases
> > #### Higher levels usually increase **latency** and **token usage** pick the smallest that works.


<h5 id="thinking-examples">Examples</h5>

```md
# Small boost
claude -p "Think. Outline a plan to refactor the auth module."

# Medium boost
claude -p "Think harder. Draft a migration plan from REST to gRPC."

# Max boost
claude -p "Ultrathink. Propose a step-by-step strategy to fix flaky payment tests and add guardrails."
```

<h2 id="sub-agents">Sub Agents</h2>

> Sub‑Agents are purpose‑built helpers with their **own prompts, tools, and isolated context windows**. Treat this like a "mixture‑of‑experts" you **compose** per repo.

**When to use them**
> - You need high signal responses (plans, reviews, diffs) without side quests.
> - You want version‑controlled prompts and tool policies alongside the codebase.
> - You work in PR‑driven teams and want scoped edits by role.

<h3 id="each-sub-agent-has-its-own-context">每个子代理都有自己的上下文</h3>

**为你的阵容设计规则**
> - 为每个代理定义**一个明确的职责**。
> - 为该角色保留**最少**的工具集。
> - 分析/审查任务优先选择**只读**代理。
> - 尽可能少地赋予代理编辑权限。

<img width="700" height="160" alt="image" src="https://github.com/user-attachments/assets/42767417-20aa-4bd4-aaf2-cfa0e515b54b" />

*Caption: Agents selection UI in the terminal.*

<h3 id="configure-agents">配置代理</h3>

> 将代理**保留在项目中**，以便它们与仓库一起进行版本控制，并通过 PR 进行演进。

<h3 id="agents-quick-start">代理快速启动</h3>

> 更新 CLI 并打开代理面板
```bash
claude update
/agents
```

<h3 id="create-your-core-agents">创建你的核心代理</h3>

> - **规划者** (只读): 将功能/问题转化为小的、可测试的任务；输出任务列表或 plan.md。
> - **代码生成器** (可编辑): 实现任务；仅限于 `src/` + `tests/`。
> - **测试员** (只读或补丁): 编写 *一个* 失败的测试或最小的复现。
> - **评审员** (只读): 留下结构化的评审意见；从不编辑。
> - **文档** (可编辑): 仅更新 `README.md`/`docs/`。

***策略**提示：对于具有编辑能力的代理，优先选择**补丁输出**，以便更改通过您的常规 Git 工作流进行。*

<img width="700" height="173" alt="image" src="https://github.com/user-attachments/assets/84bc80de-35b8-4ef7-9b27-f74f7d4a51f9" />

*Caption: Choose only the tools an agent truly needs (e.g., advisory vs editing access).*

<h3 id="example-prompts">示例提示</h3>

> 保持提示简短、可测试且特定于仓库。将它们签入 `agents/`：

<img width="700" height="217" alt="image" src="https://github.com/user-attachments/assets/b4f92591-ff5c-4775-aec2-051f145b9616" />

*Caption: Example prompt for a **test‑coverage‑analyzer** agent.*

**tester.prompt.md (sample)**
```
Role: Write a single, focused failing test for the specific scenario I describe.
Scope: Only create/modify tests under tests/. Do not change src/.
Output: A brief rationale + a unified diff or patch.
If the scenario is unclear, ask exactly one clarifying question.
```

<h3 id="expected-output">预期输出</h3>

> 你的测试代理应该生成一个小的差异或补丁以及一个简短的理由：

<img width="700" height="273" alt="image" src="https://github.com/user-attachments/assets/839151ce-02c9-4283-a53b-9dd105802ada" />

*Caption: Example response from the **test‑coverage‑analyzer** agent.*

<h3 id="why-this-shift-matters">为什么这种转变很重要</h3>

**操作优势**
> - **更少的上下文切换**：你保持在一种思维模式中；代理完成其余工作。
> - **更清晰的 PR**：狭窄的提示 + 有限的工具 → 更小、可审查的差异。
> - **更少的回归**：测试员/审查员代理在合并前发现漏洞。
> - **可重复性**：提示 + 策略存在于仓库中并随分支一起传播。

**安全与治理**
> - 按路径限制写入访问（例如，`src/`、`tests/`、`docs/`）。
> - 优先选择只读分析高风险区域。
> - 将助手输出记录/提交为补丁以进行可审计性。

<h3 id="a-mindset-shift">思维转变</h3>

**做**
> - 将代理视为具有职位描述的队友。
> - 从只读开始；**最后**授予写入权限。
> - 将提示保留在版本控制中，并通过 PR 进行迭代。

**不要**
> - 要求一个代理在一个回合中完成计划、编码和测试。
> - 授予全面的写入权限。
> - 当你只要求一个测试时，接受多文件差异。

<h2 id="mcp-integration">MCP集成</h2>

<h3 id="understanding-mcp-model-context-protocol">理解MCP（模型上下文协议）</h3>

#### 什么是MCP？
> MCP通过连接到外部服务、数据库、API和工具（文件系统、Puppeteer、GitHub、Context7等）来扩展Claude的功能。


###### **MCP架构：**
```
Claude Code ←→ MCP协议 ←→ MCP服务器 ←→ 外部服务
```

<h3 id="mcp-setup--configuration">MCP 设置与配置</h3>

###### 基本 MCP 命令
```bash
claude mcp                   # 交互式 MCP 配置
claude mcp list              # 列出已配置的服务器            
claude mcp add <name> <cmd>  # 添加新服务器
claude mcp remove <name>     # 移除服务器
```

###### MCP 配置文件位置
```bash
~/.claude.json      # 全局文件
`.mcp.json`         # 项目范围的服务器存储在项目根目录下的文件中
```

<h3 id="popular-mcp-servers">常用 MCP 服务器</h3>

#### 开发工具
```bash
# npm install -g git-mcp-server         

# claude mcp add git "git-mcp-server"
# claude mcp add github "github-mcp-server --token $GITHUB_TOKEN"
```

#### 数据库集成  
```bash
npm install -g postgres-mcp-server               
npm install -g mysql-mcp-server                  
npm install -g sqlite-mcp-server               

# 设置示例可能如下所示：
# export POSTGRES_URL="postgresql://user:password@localhost:5432/mydb"
# claude mcp add postgres "postgres-mcp-server --url $POSTGRES_URL"
```

#### MCP 工具权限

```bash
# 允许特定的 MCP 工具 
claude --allowedTools "mcp__git__commit,mcp__git__push"

# 允许来自特定服务器的所有工具
claude --allowedTools "mcp__postgres__*"

# 与内置工具结合使用
claude --allowedTools "Edit,View,mcp__git__*"
```

<h2 id="hooks-system">钩子系统</h2>

> 本页面提供了在 Claude Code 中实现钩子的参考文档。

<Tip>
  有关包含示例的快速入门指南，请参阅 [Claude Code 钩子入门](/en/docs/claude-code/hooks-guide)。
</Tip>

<h3 id="hooks-configuration">配置</h3>

Claude Code 钩子在您的 [设置文件](/en/docs/claude-code/settings) 中配置：

* `~/.claude/settings.json` - 用户设置
* `.claude/settings.json` - 项目设置
* `.claude/settings.local.json` - 本地项目设置（不提交）
* 企业管理策略设置

#### 结构

钩子按匹配器组织，每个匹配器可以有多个钩子：

```json
{
  "hooks": {
    "EventName": [
      {
        "matcher": "ToolPattern",
        "hooks": [
          {
            "type": "command",
            "command": "your-command-here"
          }
        ]
      }
    ]
  }
}
```

* **matcher**: 匹配工具名称的模式，区分大小写（仅适用于 `PreToolUse` 和 `PostToolUse`）
  * 简单字符串精确匹配：`Write` 仅匹配 Write 工具
  * 支持正则表达式：`Edit|Write` 或 `Notebook.*`
  * 使用 `*` 匹配所有工具。您也可以使用空字符串 (`""`) 或留空 `matcher`。
* **hooks**: 当模式匹配时执行的命令数组
  * `type`: 目前仅支持 `"command"`
  * `command`: 要执行的 bash 命令（可以使用 `$CLAUDE_PROJECT_DIR` 环境变量）
  * `timeout`: (可选) 命令应运行多长时间（秒），然后取消该特定命令。

对于不使用匹配器的事件，如 `UserPromptSubmit`、`Notification`、`Stop` 和 `SubagentStop`，您可以省略匹配器字段：

```json
{
  "hooks": {
    "UserPromptSubmit": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "/path/to/prompt-validator.py"
          }
        ]
      }
    ]
  }
}
```

#### 项目特定的钩子脚本

您可以使用环境变量 `CLAUDE_PROJECT_DIR`（仅当 Claude Code 启动钩子命令时可用）来引用存储在项目中的脚本，确保它们无论 Claude 的当前目录如何都能正常工作：

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "$CLAUDE_PROJECT_DIR/.claude/hooks/check-style.sh"
          }
        ]
      }
    ]
  }
}
```

<h3 id="hook-events">钩子事件</h3>

#### PreToolUse

在 Claude 创建工具参数之后、处理工具调用之前运行。

**常用匹配器：**

* `Task` - 子代理任务（参见 [子代理文档](/en/docs/claude-code/sub-agents)）
* `Bash` - Shell 命令
* `Glob` - 文件模式匹配
* `Grep` - 内容搜索
* `Read` - 文件读取
* `Edit`、`MultiEdit` - 文件编辑
* `Write` - 文件写入
* `WebFetch`、`WebSearch` - Web 操作

#### PostToolUse

在工具成功完成之后立即运行。

识别与 PreToolUse 相同的匹配器值。

#### Notification

当 Claude Code 发送通知时运行。在以下情况下发送通知：

1. Claude 需要您的权限才能使用工具。示例：“Claude 需要您的权限才能使用 Bash”
2. 提示输入已空闲至少 60 秒。“Claude 正在等待您的输入”

#### UserPromptSubmit

在用户提交提示后、Claude 处理之前运行。这允许您根据提示/对话添加额外上下文、验证提示或阻止某些类型的提示。

#### Stop

当主 Claude Code 代理完成响应时运行。如果由于用户中断而停止，则不运行。

#### SubagentStop

当 Claude Code 子代理（任务工具调用）完成响应时运行。

#### PreCompact

在 Claude Code 即将运行压缩操作之前运行。

**匹配器：**

* `manual` - 从 `/compact` 调用
* `auto` - Invoked from auto-compact (due to full context window)

#### SessionStart

当 Claude Code 启动新会话或恢复现有会话时运行（目前在底层确实会启动新会话）。对于加载开发上下文（如现有问题或代码库的最新更改）很有用。

**匹配器：**

* `startup` - 从启动调用
* `resume` - 从 `--resume`、`--continue` 或 `/resume` 调用
* `clear` - 从 `/clear` 调用

<h3 id="hook-input">钩子输入</h3>

钩子通过 stdin 接收 JSON 数据，其中包含会话信息和事件特定数据：

```typescript
{
  // Common fields
  session_id: string
  transcript_path: string  // 对话 JSON 的路径
  cwd: string              // 钩子被调用时的工作目录

  // Event-specific fields
  hook_event_name: string
  ...
}
```

#### PreToolUse 输入

`tool_input` 的确切 schema 取决于工具。

```json
{
  "session_id": "abc123",
  "transcript_path": "/Users/.../.claude/projects/.../00893aaf-19fa-41d2-8238-13269b9b3ca0.jsonl",
  "cwd": "/Users/...",
  "hook_event_name": "PreToolUse",
  "tool_name": "Write",
  "tool_input": {
    "file_path": "/path/to/file.txt",
    "content": "file content"
  }
}
```

#### PostToolUse 输入

`tool_input` 和 `tool_response` 的确切 schema 取决于工具。

```json
{
  "session_id": "abc123",
  "transcript_path": "/Users/.../.claude/projects/.../00893aaf-19fa-41d2-8238-13269b9b3ca0.jsonl",
  "cwd": "/Users/...",
  "hook_event_name": "PostToolUse",
  "tool_name": "Write",
  "tool_input": {
    "file_path": "/path/to/file.txt",
    "content": "file content"
  },
  "tool_response": {
    "filePath": "/path/to/file.txt",
    "success": true
  }
}
```

#### Notification 输入

```json
{
  "session_id": "abc123",
  "transcript_path": "/Users/.../.claude/projects/.../00893aaf-19fa-41d2-8238-13269b9b3ca0.jsonl",
  "cwd": "/Users/...",
  "hook_event_name": "Notification",
  "message": "Task completed successfully"
}
```

#### UserPromptSubmit 输入

```json
{
  "session_id": "abc123",
  "transcript_path": "/Users/.../.claude/projects/.../00893aaf-19fa-41d2-8238-13269b9b3ca0.jsonl",
  "cwd": "/Users/...",
  "hook_event_name": "UserPromptSubmit",
  "prompt": "Write a function to calculate the factorial of a number"
}
```

#### Stop 和 SubagentStop 输入

当 Claude Code 因停止钩子而继续运行时，`stop_hook_active` 为 true。检查此值或处理 transcript 以防止 Claude Code 无限期运行。

```json
{
  "session_id": "abc123",
  "transcript_path": "~/.claude/projects/.../00893aaf-19fa-41d2-8238-13269b9b3ca0.jsonl",
  "hook_event_name": "Stop",
  "stop_hook_active": true
}
```

#### PreCompact 输入

对于 `manual`，`custom_instructions` 来自用户传递给 `/compact` 的内容。对于 `auto`，`custom_instructions` 为空。

```json
{
  "session_id": "abc123",
  "transcript_path": "~/.claude/projects/.../00893aaf-19fa-41d2-8238-13269b9b3ca0.jsonl",
  "hook_event_name": "PreCompact",
  "trigger": "manual",
  "custom_instructions": ""
}
```

#### SessionStart 输入

```json
{
  "session_id": "abc123",
  "transcript_path": "~/.claude/projects/.../00893aaf-19fa-41d2-8238-13269b9b3ca0.jsonl",
  "hook_event_name": "SessionStart",
  "source": "startup"
}
```

<h3 id="hook-output">钩子输出</h3>

钩子有两种方式将输出返回给 Claude Code。输出会传达是否阻塞以及应向 Claude 和用户显示的任何反馈。

#### 简单：退出代码

钩子通过退出代码、stdout 和 stderr 传达状态：

* **退出代码 0**：成功。`stdout` 在转录模式 (CTRL-R) 下显示给用户，`UserPromptSubmit` 和 `SessionStart` 除外，其中 `stdout` 会添加到上下文中。
* **退出代码 2**：阻塞错误。`stderr` 会反馈给 Claude 自动处理。请参阅下面的每个钩子事件行为。
* **其他退出代码**：非阻塞错误。`stderr` 会显示给用户，并继续执行。

<Warning>
  提醒：如果退出代码为 0，Claude Code 不会看到 `stdout`，`UserPromptSubmit` 钩子除外，其中 `stdout` 作为上下文注入。
</Warning>

##### 退出代码 2 行为

| 钩子事件         | 行为                                                           |
| ------------------ | ------------------------------------------------------------------ |
| `PreToolUse`       | 阻塞工具调用，向 Claude 显示 stderr                       |
| `PostToolUse`      | 向 Claude 显示 stderr（工具已运行）                          |
| `Notification`     | 不适用，仅向用户显示 stderr                                     |
| `UserPromptSubmit` | 阻塞提示处理，擦除提示，仅向用户显示 stderr |
| `Stop`             | 阻塞停止，向 Claude 显示 stderr                            |
| `SubagentStop`     | 阻塞停止，向 Claude 子代理显示 stderr                   |
| `PreCompact`       | 不适用，仅向用户显示 stderr                                     |
| `SessionStart`     | 不适用，仅向用户显示 stderr                                     |

#### 高级：JSON 输出

钩子可以在 `stdout` 中返回结构化 JSON，以实现更复杂的控制：

##### 常见 JSON 字段

所有钩子类型都可以包含这些可选字段：

```json
{
  "continue": true, // 钩子执行后 Claude 是否应继续（默认：true）
  "stopReason": "string" // 当 continue 为 false 时显示的消息
  "suppressOutput": true, // 在转录模式下隐藏 stdout（默认：false）
}
```

如果 `continue` 为 false，Claude 在钩子运行后停止处理。

* 对于 `PreToolUse`，这与 `"permissionDecision": "deny"` 不同，后者仅阻塞特定的工具调用并向 Claude 提供自动反馈。
* 对于 `PostToolUse`，这与 `"decision": "block"` 不同，后者提供自动反馈给 Claude。
* 对于 `UserPromptSubmit`，这会阻止提示被处理。
* 对于 `Stop` 和 `SubagentStop`，这优先于任何 `"decision": "block"` 输出。
* 在所有情况下，`"continue" = false` 优先于任何 `"decision": "block"` 输出。

`stopReason` 伴随 `continue`，并向用户显示原因，不向 Claude 显示。

##### `PreToolUse` 决策控制

`PreToolUse` 钩子可以控制工具调用是否继续。

* `"allow"` 绕过权限系统。`permissionDecisionReason` 会显示给用户，但不会显示给 Claude。（*已弃用的 `"approve"` 值 + `reason` 具有相同的行为。*）
* `"deny"` 阻止工具调用执行。`permissionDecisionReason` 会显示给 Claude，并向用户显示。（*`"block"` 值 + `reason` 具有相同的行为。*）
* `"ask"` 要求用户在 UI 中确认工具调用。


```json
{
  "hookSpecificOutput": {
    "hookEventName": "PreToolUse",
    "permissionDecision": "allow" | "deny" | "ask",
    "permissionDecisionReason": "我的理由在这里（显示给用户）"
  },
  "decision": "approve" | "block" | undefined, // PreToolUse 已弃用但仍受支持
  "reason": "决策解释" // PreToolUse 已弃用但仍受支持
}
##### `PostToolUse` 决策控制

`PostToolUse` 钩子可以控制工具调用是否继续。

```json
{
  "decision": "block" | undefined,
  "reason": "决策解释"
}
```

##### `UserPromptSubmit` 决策控制

`UserPromptSubmit` 钩子可以控制用户提示是否被处理。

* `"block"` 阻止提示被处理。提交的提示会从上下文中擦除。`"reason"` 会显示给用户，但不会添加到上下文中。
* `undefined` 允许提示正常进行。`"reason"` 被忽略。
* `"hookSpecificOutput.additionalContext"` 如果未被阻止，则将字符串添加到上下文中。

```json
{
  "decision": "block" | undefined,
  "reason": "决策解释",
  "hookSpecificOutput": {
    "hookEventName": "UserPromptSubmit",
    "additionalContext": "我的附加上下文在这里"
  }
}
```

##### `Stop`/`SubagentStop` 决策控制

`Stop` 和 `SubagentStop` 钩子可以控制 Claude 是否必须继续。

* `"block"` 阻止 Claude 停止。您必须填充 `reason`，以便 Claude 知道如何继续。
* `undefined` 允许 Claude 停止。`reason` 被忽略。

```json
{
  "decision": "block" | undefined,
  "reason": "当 Claude 被阻止停止时必须提供"
}
```

##### `SessionStart` 决策控制

`SessionStart` 钩子允许您在会话开始时加载上下文。

* `"hookSpecificOutput.additionalContext"` 将字符串添加到上下文中。

```json
{
  "hookSpecificOutput": {
    "hookEventName": "SessionStart",
    "additionalContext": "我的附加上下文在这里"
  }
}
```

##### 退出代码示例：Bash 命令验证

```python
#!/usr/bin/env python3
import json
import re
import sys

# Define validation rules as a list of (regex pattern, message) tuples
VALIDATION_RULES = [
    (
        r"\\bgrep\\b(?!.*\\|)",
        "使用 'rg' (ripgrep) 代替 'grep' 以获得更好的性能和功能",
    ),
    (
        r"\\bfind\\s+\\S+\\s+-name\\b",
        "使用 'rg --files | rg pattern' 或 'rg --files -g pattern' 代替 'find -name' 以获得更好的性能",
    ),
]


def validate_command(command: str) -> list[str]:
    issues = []
    for pattern, message in VALIDATION_RULES:
        if re.search(pattern, command):
            issues.append(message)
    return issues


try:
    input_data = json.load(sys.stdin)
except json.JSONDecodeError as e:
    print(f"Error: Invalid JSON input: {e}", file=sys.stderr)
    sys.exit(1)

tool_name = input_data.get("tool_name", "")
tool_input = input_data.get("tool_input", {})
command = tool_input.get("command", "")

if tool_name != "Bash" or not command:
    sys.exit(1)

# Validate the command
issues = validate_command(command)

if issues:
    for message in issues:
        print(f"• {message}", file=sys.stderr)
    # Exit code 2 blocks tool call and shows stderr to Claude
    sys.exit(2)
```

##### JSON 输出示例：UserPromptSubmit 添加上下文和验证

<Note>
  对于 `UserPromptSubmit` 钩子，您可以使用以下任一方法注入上下文：

  * 退出代码 0 并带 stdout：Claude 会看到上下文（`UserPromptSubmit` 的特殊情况）
  * JSON 输出：提供对行为的更多控制
</Note>

```python
#!/usr/bin/env python3
import json
import sys
import re
import datetime

# Load input from stdin
try:
    input_data = json.load(sys.stdin)
except json.JSONDecodeError as e:
    print(f"Error: Invalid JSON input: {e}", file=sys.stderr)
    sys.exit(1)

prompt = input_data.get("prompt", "")

# 检查敏感模式
sensitive_patterns = [
    (r"(?i)\\b(password|secret|key|token)\\s*[:=]", "Prompt contains potential secrets"),
]

for pattern, message in sensitive_patterns:
    if re.search(pattern, prompt):
        # Use JSON output to block with a specific reason
        output = {
            "decision": "block",
            "reason": "违反安全策略：{message}。请重新表述您的请求，不要包含敏感信息。"
        }
        print(json.dumps(output))
        sys.exit(0)

# 将当前时间添加到上下文
context = f"当前时间：{datetime.datetime.now()}"
print(context)

"""
The following is also equivalent:
print(json.dumps({
  "hookSpecificOutput": {
    "hookEventName": "UserPromptSubmit",
    "additionalContext": context,
  },
}))
"""

# 允许提示与附加上下文一起进行
sys.exit(0)
```

##### JSON 输出示例：PreToolUse 带审批

```python
#!/usr/bin/env python3
import json
import sys

# Load input from stdin
try:
    input_data = json.load(sys.stdin)
except json.JSONDecodeError as e:
    print(f"Error: Invalid JSON input: {e}", file=sys.stderr)
    sys.exit(1)

tool_name = input_data.get("tool_name", "")
tool_input = input_data.get("tool_input", {})

# 示例：自动批准文档文件的文件读取
if tool_name == "Read":
    file_path = tool_input.get("file_path", "")
    if file_path.endswith((".md", ".mdx", ".txt", ".json")):
        # Use JSON output to auto-approve the tool call
        output = {
            "decision": "approve",
            "reason": "文档文件自动批准",
            "suppressOutput": True  # 在转录模式下不显示
        }
        print(json.dumps(output))
        sys.exit(0)

# 对于其他情况，让正常的权限流程继续
sys.exit(0)
```

### 使用 MCP 工具

Claude Code 钩子与 [模型上下文协议 (MCP) 工具](/en/docs/claude-code/mcp) 无缝协作。当 MCP 服务器提供工具时，它们会以特殊的命名模式出现，您可以在钩子中匹配这些模式。

#### MCP 工具命名

MCP 工具遵循 `mcp__<server>__<tool>` 模式，例如：

* `mcp__memory__create_entities` - 内存服务器的创建实体工具
* `mcp__filesystem__read_file` - 文件系统服务器的读取文件工具
* `mcp__github__search_repositories` - GitHub 服务器的搜索工具

#### 为 MCP 工具配置钩子

您可以针对特定的 MCP 工具或整个 MCP 服务器：

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "mcp__memory__.*",
        "hooks": [
          {
            "type": "command",
            "command": "echo '内存操作已启动' >> ~/mcp-operations.log"
          }
        ]
      },
      {
        "matcher": "mcp__.*__write.*",
        "hooks": [
          {
            "type": "command",
            "command": "/home/user/scripts/validate-mcp-write.py"
          }
        ]
      }
    ]
  }
}
```

### 示例

<Tip>
  有关包括代码格式化、通知和文件保护在内的实用示例，请参阅入门指南中的 [更多示例](/en/docs/claude-code/hooks-guide#more-examples)。
</Tip>

### 安全注意事项

#### 免责声明

**使用风险自负**：Claude Code 钩子会在您的系统上自动执行任意 shell 命令。通过使用钩子，您承认：

* 您对您配置的命令负全部责任
* 钩子可以修改、删除或访问您的用户帐户可以访问的任何文件
* 恶意或编写不当的钩子可能导致数据丢失或系统损坏
* Anthropic 不提供任何担保，也不对因使用钩子而造成的任何损害承担任何责任
* 您应该在生产环境中使用之前，在安全环境中彻底测试钩子

在将任何钩子命令添加到您的配置之前，请务必审查并理解它们。

## 安全最佳实践

以下是编写更安全的钩子的一些关键实践：

1. **验证和清理输入** - 永远不要盲目信任输入数据
2. **始终引用 shell 变量** - 使用 `"$VAR"` 而不是 `$VAR`
3. **阻止路径遍历** - 检查文件路径中的 `..`
4. **使用绝对路径** - 为脚本指定完整路径（使用 `$CLAUDE_PROJECT_DIR` 作为项目路径）
5. **跳过敏感文件** - 避免 `.env`、`.git/`、密钥等

#### 配置安全

直接编辑设置文件中的钩子不会立即生效。Claude Code：

1. 在启动时捕获钩子的快照
2. 在整个会话中使用此快照
3. 如果钩子被外部修改，则发出警告
4. 需要在 `/hooks` 菜单中进行审查才能应用更改

这可以防止恶意钩子修改影响您当前的会话。

### 钩子执行详情

* **超时**：默认执行限制为 60 秒，可按命令配置。
  * 单个命令的超时不会影响其他命令。
* **并行化**：所有匹配的钩子并行运行
* **环境**：在当前目录中运行，使用 Claude Code 的环境
  * `CLAUDE_PROJECT_DIR` 环境变量可用，并包含项目根目录的绝对路径
* **输入**：通过 stdin 的 JSON
* **输出**：
  * PreToolUse/PostToolUse/Stop：进度显示在转录中 (Ctrl-R)
  * Notification：仅记录到调试 (`--debug`)

### 调试

#### 基本故障排除

如果您的钩子不起作用：

1. **检查配置** - 运行 `/hooks` 查看您的钩子是否已注册
2. **验证语法** - 确保您的 JSON 设置有效
3. **测试命令** - 首先手动运行钩子命令
4. **检查权限** - 确保脚本可执行
5. **审查日志** - 使用 `claude --debug` 查看钩子执行详情

常见问题：

* **引号未转义** - 在 JSON 字符串中使用 `\"`
* **匹配器错误** - 检查工具名称是否完全匹配（区分大小写）
* **找不到命令** - 对脚本使用完整路径

#### 高级调试

对于复杂的钩子问题：

1. **检查钩子执行** - 使用 `claude --debug` 查看详细的钩子执行
2. **验证 JSON 模式** - 使用外部工具测试钩子输入/输出
3. **检查环境变量** - 验证 Claude Code 的环境是否正确
4. **测试边缘情况** - 尝试使用不寻常的文件路径或输入来测试钩子
5. **监控系统资源** - 检查钩子执行期间的资源耗尽情况
6. **使用结构化日志记录** - 在您的钩子脚本中实现日志记录

#### 调试输出示例

使用 `claude --debug` 查看钩子执行详情：

```
[DEBUG] Executing hooks for PostToolUse:Write
[DEBUG] Getting matching hook commands for PostToolUse with query: Write
[DEBUG] Found 1 hook matchers in settings
[DEBUG] Matched 1 hooks for query "Write"
[DEBUG] Found 1 hook commands to execute
[DEBUG] Executing hook command: <Your command> with timeout 60000ms
[DEBUG] Hook command completed with status 0: <Your stdout>
```

进度消息显示在转录模式 (Ctrl-R) 中，显示：

* 正在运行哪个钩子
* 正在执行的命令
* 成功/失败状态
* 输出或错误消息

---

# 安全与权限

#### 工具权限模式
```bash
# 允许特定工具（读/编辑文件）
claude --allowedTools "Edit,Read"

# 允许工具类别，包括 Bash（但仍受限于以下范围）
claude --allowedTools "Edit,Read,Bash"

# 范围权限（所有 git 命令）
claude --allowedTools "Bash(git:*)"

# 多个范围（git + npm）
claude --allowedTools "Bash(git:*),Bash(npm:*)"
```

### 危险模式

> [!Warning]
> 切勿在生产系统、共享机器或任何包含重要数据的系统中使用
> 仅在隔离环境（如 **Docker 容器**）中使用，使用此模式可能导致数据丢失并损害您的系统！
> 
> `claude --dangerously-skip-permissions`

## 安全最佳实践

### 限制性启动

### 保护敏感数据

- **保持 `~/.claude.json` 私有 (`chmod 600`)。**
- **优先使用环境变量而不是纯文本来存储 API 密钥。**
- 使用 `--strict-mcp-config` 仅从指定的配置文件加载 MCP 服务器

# 自动化与集成

## 使用 Claude Code 进行自动化与脚本编写

> 您可以复制/粘贴的 GitHub Actions :p

1. **在您的组织/仓库上安装 Claude GitHub App**（Actions 在 PR/issue 上评论所需）。
2. 在您的仓库中，添加一个秘密 **`ANTHROPIC_API_KEY`** 设置 → 秘密和变量 → Actions → 新仓库秘密
3. 将以下工作流复制到 **`.github/workflows/`**。
4. 打开一个**测试 PR**（或新问题）以查看它们运行。

> [!TIP]
> 当您长期采用 Actions 时，请将其固定到发布标签（例如 `@v1`）。下面的代码片段使用分支标签是为了可读性。

<h2 id="auto-pr-review-inline-comments">自动 PR 审查（内联评论）</h2>

> **在 PR 打开或更新时，立即创建结构化审查（带内联评论）。**

**文件：** `.github/workflows/claude-pr-auto-review.yml`

```yaml
name: Auto review PRs
on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

permissions:
  contents: read
  pull-requests: write

jobs:
  auto-review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 1

      - name: Claude PR review
        uses: anthropics/claude-code-action@main
        with:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
          # Claude 将获取差异并留下内联评论
          direct_prompt: |
            审查此拉取请求的差异，以检查正确性、可读性、测试、性能和开发体验。
            优先提供具体的、可操作的建议。在相关的地方使用内联评论。
          # 运行期间允许的 GitHub 工具：
          allowed_tools: >-
            mcp__github__get_pull_request_diff,
            mcp__github__create_pending_pull_request_review,
            mcp__github__add_comment_to_pending_review,
            mcp__github__submit_pending_pull_request_review
```

<h2 id="security-review-on-every-pr">每次 PR 上的安全审查</h2>

> **运行有针对性的安全扫描，并将发现的问题直接评论到 PR 上。**

**文件：** `.github/workflows/claude-security-review.yml`

```yaml
name: Security Review
on:
  pull_request:

permissions:
  contents: read
  pull-requests: write

jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          ref: ${{ github.event.pull_request.head.sha || github.sha }}
          fetch-depth: 2

      - name: Claude Code Security Review
        uses: anthropics/claude-code-security-review@main
        with:
          claude-api-key: ${{ secrets.ANTHROPIC_API_KEY }}
          comment-pr: true
          # 可选：
          # 排除目录："docs,examples"
          # claudecode-timeout: "20"
          # claude-model: "claude-3-5-sonnet-20240620"
```

<h2 id="issue-triage-suggest-labels--severity">问题分类（建议标签和严重性）</h2>

> **当新问题打开时，Claude 会建议标签/严重性并发布整洁的分类评论。您可以通过翻转一个标志来启用**自动应用标签**。**

**文件：** `.github/workflows/claude-issue-triage.yml`

```yaml
name: Claude Issue Triage
on:
  issues:
    types: [opened, edited, reopened]

permissions:
  contents: read
  issues: write

jobs:
  triage:
    runs-on: ubuntu-latest
    env:
      CLAUDE_MODEL: claude-3-5-sonnet-20240620
    steps:
      - name: Collect context & similar issues
        id: gather
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          TITLE="${{ github.event.issue.title }}"
          BODY="${{ github.event.issue.body }}"
          # 按标题词进行简单的相似搜索
          Q=$(echo "$TITLE" | tr -dc '[:alnum:] ' | awk '{print $1" "$2" "$3" "$4}')
          gh api -X GET search/issues -f q="repo:${{ github.repository }} is:issue $Q" -f per_page=5 > similars.json
          echo "$TITLE" > title.txt
          echo "$BODY" > body.txt

      - name: 请求 Claude 进行分类 JSON
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          cat > payload.json << 'JSON'
          {
            "model": "${{ env.CLAUDE_MODEL }}",
            "max_tokens": 1500,
            "system": "你是一名务实的分类工程师。要具体，对重复项要谨慎。",
            "messages": [{
              "role": "user",
              "content": [{
                "type":"text",
                "text":"根据问题和类似的候选，生成带有键的严格 JSON：labels（字符串数组）、severity（以下之一：low、medium、high、critical）、duplicate_url（字符串或空）、comment_markdown（简短字符串）。不要包含任何额外的键。"
              },
              {"type":"text","text":"Issue title:\n"},
              {"type":"text","text": "$(cat title.txt)" },
              {"type":"text","text":"\n\nIssue body:\n"},
              {"type":"text","text": "$(cat body.txt)" },
              {"type":"text","text":"\n\nSimilar issues (JSON):\n"},
              {"type":"text","text": "$(cat similars.json)" }]
            }]
          }
          JSON
          # 安全注入文件
          jq --arg title "$(cat title.txt)" '.messages[0].content[2].text = $title' payload.json \
          | jq --arg body "$(cat body.txt)" '.messages[0].content[4].text = $body' \
          | jq --arg sims "$(cat similars.json)" '.messages[0].content[6].text = $sims' > payload.final.json

          curl -s https://api.anthropic.com/v1/messages \
            -H "x-api-key: $ANTHROPIC_API_KEY" \
            -H "anthropic-version: 2023-06-01" \
            -H "content-type: application/json" \
            -d @payload.final.json > out.json
          jq -r '.content[0].text' out.json > triage.json || echo '{}' > triage.json
          # 验证 JSON 以避免发布垃圾信息
          jq -e . triage.json >/dev/null 2>&1 || echo '{"labels":[],"severity":"low","duplicate_url":"","comment_markdown":"(triage failed to parse)"}' > triage.json

      - name: 应用标签（可选）
        if: ${{ false }} # 翻转为 `true` 以自动应用标签
        uses: actions/github-script@v7
        with:
          script: |
            const triage = JSON.parse(require('fs').readFileSync('triage.json','utf8'))
            if (triage.labels?.length) {
              await github.rest.issues.addLabels({
                owner: context.repo.owner,
                repo: context.repo.repo,
                issue_number: context.issue.number,
                labels: triage.labels
              })
            }

      - name: 发布分类评论
        uses: actions/github-script@v7
        with:
          script: |
            const fs = require('fs')
            const triage = JSON.parse(fs.readFileSync('triage.json','utf8'))
            const md = `### 🤖 分类
            - **建议标签：** ${triage.labels?.join(', ') || '—'}
            - **严重性：** ${triage.severity || '—'}
            ${triage.duplicate_url ? `- **可能的重复项：** ${triage.duplicate_url}\n` : ''}
            ---
            ${triage.comment_markdown || ''}`
            await github.rest.issues.createComment({
              owner: context.repo.owner,
              repo: context.repo.repo,
              issue_number: context.issue.number,
              body: md
            })
```

> [!NOTE]
> 默认情况下，分类工作流会发布**建议评论**。如果您希望自动应用标签，请将“应用标签”步骤翻转为 `true`。
>
> ### 配置与自定义
> - **模型选择**：在所示位置设置 `CLAUDE_MODEL`（例如，`claude-3-5-sonnet-20240620`）。
> - **秘密**：`ANTHROPIC_API_KEY` 是必需的。内置的 `GITHUB_TOKEN` 足以发布评论和应用标签。
> - **权限**：每个工作流都声明了其所需的最低权限（`pull-requests: write` 和/或 `issues: write`）。仅当您的组织需要更严格的策略时才进行调整。
> - **范围**：在触发器上使用 `paths:` 过滤器来限制工作流的运行时间（例如，仅适用于 `/src` 或排除 `/docs`）。
>
> ### 故障排除
> 首先检查 **Actions 日志**——大多数问题是缺少秘密/权限或 YAML 块缩进错误。
> - **PR 上没有评论出现**：验证 Claude GitHub App 是否已安装，并且工作流具有 `pull-requests: write` 权限。
> - **应用标签时出现 403 错误**：确保作业或步骤具有 `issues: write` 权限。默认的 `GITHUB_TOKEN` 必须有权访问此仓库。
> - **Anthropic API 错误**：确认 `ANTHROPIC_API_KEY` 已在仓库（或组织）级别设置且未过期。
> - **“YAML 格式不正确”**：验证间距——每个嵌套级别两个空格；没有制表符。


---

<h1 id="help--troubleshooting">Help & Troubleshooting</h1>

> [!TIP]
> **问：`claude` 未找到，但 `npx claude` 可以工作？**
> > **答：您的 `PATH` 缺少 npm 全局 bin。请参阅 [`Windows`](#windowspath) 或 [`Linux`](#linuxpath) 的 `PATH` 问题部分**
>
> **问：需要哪个 Node.js 版本？** 
> > **答：Node.js **18+**（最好是 **20+**）。使用 `node --version` 检查。
>
> **问：在哪里查看日志**  
> > **答：运行 `claude doctor` 和 `claude --verbose`，诊断窗口将指向日志位置。
>
> **问：编辑 PATH 后需要重启吗？** 
> > **答：无需重启，但您<mark>必须</mark>打开一个<mark>新</mark>终端窗口。

<table><td>
  
<h2 id="debug-quick-commands">调试快速命令</h2>

*检查 `claude doctor` 的输出，了解日志位置和环境检查。*

> [!Note]
> 
> ```bash
> claude                  # 打开 Claude UI（如果在 PATH 中）
> claude --version        # 显示 CLI 版本（例如 1.0.xx）
> claude update           # 更新 CLI（如果支持）
> 
> claude doctor           # 打开诊断/调试窗口
> npx claude /doctor      # 打开诊断/调试窗口
> 
> claude --debug          # 启动带有诊断的 Claude
> claude --verbose        # 详细日志记录
> 
> where claude            # Windows（cmd）
> which claude            # macOS/Linux（bash/zsh）
> 
> npm bin -g              # Linux 验证全局 bin 路径
> npm prefix -g           # Windows 验证全局 bin 路径
> ```


</td></table>

<table><td>

<h2 id="linuxpath">PATH 临时修复</h2>

**您的 **PATH** 可能不包含全局 npm bin 目录。**

> [!Note]
> 
> #### Windows (CMD)：
> ```bash
> set PATH=%USERPROFILE%\AppData\Roaming\npm;C:\Program Files\nodejs;%PATH%
> where claude
> claude --debugg
> ```
> #### Windows (PowerShell)：
> ```powershell
> $env:Path = "$env:USERPROFILE\AppData\Roaming\npm;C:\Program Files\nodejs;$env:Path"
> where claude
> claude --debugg
> ```
> #### Linux/MacOS (bash/zsh) 
> ```bash
> export PATH="$(npm config get prefix)/bin:$HOME/.local/bin:$PATH"
> which claude
> claude doctor
> ```

</td></table>


<table><td>

<h2 id="windowspath">Windows PATH 永久修复</h2>

**将 `<you>` 替换为您自己的 Windows 用户名（不带尖括号）**

- **开始 → 输入：<kbd>环境变量</kbd>**
- **打开 <kbd>编辑系统环境变量</kbd> → <kbd>环境变量</kbd>**
- **在 <kbd>用户变量</kbd> <mark><you></mark> 下选择 `Path` → `编辑` → `新建` 添加：**

```path
C:\Users\<you>\AppData\Roaming\npm
C:\Program Files\nodejs</kbd>
```
> **可选添加位置：**
```path
C:\Users\<you>\.claude\local\bin
C:\Users\<you>\.local\bin
```
- **删除重复项、任何包含 `%PATH%` 的条目以及多余的引号 (`"`)。单击 `OK`。**
- **打开一个新的命令提示符/PowerShell 并验证：**
```C
where claude
claude doctor
```

> [!Tip]
> ### Optional Run directly (when PATH is broken)
> 
> > **Windows (PowerShell/cmd)**
> ```powershell
> "%USERPROFILE%\AppData\Roaming\npm\claude.cmd" --version
> "%USERPROFILE%\AppData\Roaming\npm\claude.cmd" doctor
> ```
> > **Or via npx:**
> ```
> npx claude doctor
> ```


</td></table>

<table><td>

<h3 id="installation--nodejs-issues">安装 / Node.js 问题</h3>

**必须是 Node 18+（推荐 20+）**
```bash
node --version
```
**干净卸载**  
```bash                         
npm uninstall -g @anthropic-ai/claude-code    
```
**全新安装**
```bash
npm install  -g @anthropic-ai/claude-code 
```

</td></table>

<table><td>

<h3 id="authentication-issues">身份验证问题</h3>
> *验证您的 Anthropic API 密钥是否可用于 CLI。*

**PowerShell (Windows)：**
```powershell
echo $env:ANTHROPIC_API_KEY
claude -p "test" --verbose
```

**bash/zsh (macOS/Linux)：**
```bash
echo $ANTHROPIC_API_KEY
claude -p "test" --verbose
```
*如果变量为空，请为您的 shell/配置文件设置它，或使用您的操作系统密钥链/秘密管理器。*

</td></table>

<table><td>

<h3 id="permission--allowed-tools-issues">权限 / 允许的工具问题</h3>

**检查权限**
```bash
claude config get allowedTools
```
**重置权限**
```bash
claude config set allowedTools "[]"
```
**Minimal safe set (example)**
```bash
claude config set allowedTools '["Edit","View"]'
```

</td></table>

<table><td>

<h3 id="mcp-model-context-protocol-issues">MCP（模型上下文协议）问题</h3>

> **调试 MCP 服务器**
```bash
claude --mcp-debug
```
> **列出并删除 MCP 服务器**
```bash
claude mcp list
claude mcp remove <server-name>
```

</td></table>

<table><td>

<h2 id="full-clean-reinstall-windows--powershell">完全干净重新安装（Windows / PowerShell）</h2>

> [!Caution]
>  **以下将删除您用户配置文件下的 Claude Code 二进制文件、缓存和配置**


> 1) 卸载全局 npm 包
```powershell
npm uninstall -g @anthropic-ai/claude-code
```

> 2) 删除剩余的 shim 文件
```powershell
Remove-Item -LiteralPath "$env:USERPROFILE\AppData\Roaming\npm\claude*" -Force -ErrorAction SilentlyContinue
Remove-Item -LiteralPath "$env:USERPROFILE\AppData\Roaming\npm\node_modules\@anthropic-ai\claude-code" -Recurse -Force -ErrorAction SilentlyContinue
```

> 3) 删除缓存的安装程序和本地文件
```powershell
Remove-Item -LiteralPath "$env:USERPROFILE\.claude\downloads\*" -Recurse -Force -ErrorAction SilentlyContinue
Remove-Item -LiteralPath "$env:USERPROFILE\.claude\local\bin\claude.exe" -Force -ErrorAction SilentlyContinue
Remove-Item -LiteralPath "$env:USERPROFILE\.claude\local" -Recurse -Force -ErrorAction SilentlyContinue
```

> 4) 删除配置和项目本地文件
```powershell
Remove-Item -LiteralPath "$env:USERPROFILE\.claude.json" -Force -ErrorAction SilentlyContinue
Remove-Item -LiteralPath "$env:USERPROFILE\.claude" -Recurse -Force -ErrorAction SilentlyContinue
```
> 5) 重新安装
```powershell
npm install -g @anthropic-ai/claude-code
```


</td></table>

<table><td>

<h2 id="one-shot-health-check-copypaste">一次性健康检查（复制/粘贴）</h2>

**Windows (PowerShell)：**
```powershell
Write-Host "`n=== Node & npm ==="; node --version; npm --version
Write-Host "`n=== Where is claude? ==="; where claude
Write-Host "`n=== Try doctor ==="; try { claude doctor } catch { Write-Host "claude not on PATH" }
Write-Host "`n=== API key set? ==="; if ($env:ANTHROPIC_API_KEY) { "Yes" } else { "No" }
```

**macOS/Linux (bash/zsh)：**
```bash
echo "=== Node & npm ==="; node --version; npm --version
echo "=== Where is claude? ==="; which claude || echo "claude not on PATH"
echo "=== Try doctor ==="; claude doctor || true
echo "=== API key set? ==="; [ -n "$ANTHROPIC_API_KEY" ] && echo Yes || echo No
```



</td></table>

---

<table><td>

<h2 id="appendix-useful-paths">附录：有用路径</h2>

- **Windows npm 全局 bin：** `C:\Users\<you>\AppData\Roaming\npm`
- **Windows Node.js：** `C:\Program Files\nodejs`
- **Claude 本地数据 (Win)：** `C:\Users\<you>\.claude\`
- **Claude 配置 (Win)：** `C:\Users\<you>\.claude.json`
- **macOS/Linux npm 全局 bin：** `$(npm config get prefix)/bin`（通常是 `/usr/local/bin` 或 `$HOME/.npm-global/bin`）



</td></table>


## 最佳实践

> 针对 Claude Code CLI 和交互式 REPL 的安全、快速和正确使用精选指南。此处所有命令和标志均与截至 **2025 年 8 月 23 日** 的当前 Anthropic 文档匹配。

<h2 id="effective-prompting">有效提示</h2>

```bash
# 良好：具体且详细
claude "审查 UserAuth.js 中的安全漏洞，重点关注 JWT 处理"

# 糟糕：模糊
claude "检查我的代码"
```

提示：`claude "query"` 启动交互式 REPL，并预设您的提示；`claude -p "query"` 运行**打印模式**（非交互式）并退出。

---

<h2 id="security-best-practices-main">安全最佳实践</h2>

1. **以最小权限开始**
   - 优先在 CLI 或设置文件中明确允许和拒绝。
   ```bash
   # 仅允许本次运行所需权限
   claude --allowedTools "Read" "Grep" "LS" "Bash(npm run test:*)"
   ```
   或在 `.claude/settings.json` 提交项目策略：
   ```json
   {
     "permissions": {
       "allow": ["Read", "Grep", "LS", "Bash(npm run test:*)"],
       "deny":  ["WebFetch", "Bash(curl:*)", "Read(./.env)", "Read(./secrets/**)"]
     }
   }
   ```

2. **正确处理秘密**
   - 在 SDK/自动化流程中使用环境变量：
   ```bash
   export ANTHROPIC_API_KEY="your_key"   # 用于 SDK/打印模式
   ```
   - 在交互式 REPL 中，优先使用 `/login` 而不是硬编码令牌。
   - 在设置中拒绝访问敏感文件（替换旧的 `ignorePatterns`）：
   ```json
   { "permissions": { "deny": ["Read(./.env)", "Read(./.env.*)", "Read(./secrets/**)"] } }
   ```

3. **定期审计权限**
   ```bash
   # 项目设置
   claude config list
   claude config get permissions.allow
   claude config get permissions.deny

   # 全局设置
   claude config list -g
   ```

4. **避免在生产环境中使用绕过模式**
   - 在隔离/开发沙箱之外，**不要**使用 `--dangerously-skip-permissions`。
   - 对于无人值守的运行，将狭窄的 `--allowedTools` 与 `--disallowedTools` 和项目设置结合使用。

---

<h2 id="performance-tips">性能提示</h2>

1. **在自动化中使用机器可读的输出**
   ```bash
   claude -p "summarize this error log" --output-format json
   # 有效值：text | json | stream-json
   ```

2. **限制非交互式工作**
   ```bash
   claude -p "run type checks and summarize failures" --max-turns 3
   # 也可以选择限制思考：
   export MAX_THINKING_TOKENS=20000
   ```

3. **保持会话整洁**
   ```bash
   # 仅保留最近的会话（默认为 30 天）
   claude config set -g cleanupPeriodDays 20
   ```

4. **限制上下文范围**
   ```bash
   # 仅授予对相关路径的访问权限，以减少扫描/噪音
   claude --add-dir ./services/api ./packages/ui
   ```

5. **选择正确的模型**
   - CLI 别名：`--model sonnet` 或 `--model opus`（该系列的最新版本）。
   - 为了在设置中实现可重现性，请固定完整的模型 ID（例如，`"claude-3-5-sonnet-20241022"`）。

---

<h2 id="monitoring--alerting">监控与警报</h2>

**1) 健康检查**  
使用内置的 **doctor** 命令验证安装和环境。
```bash
# 每 15 分钟
*/15 * * * * /usr/local/bin/claude doctor >/dev/null 2>&1 || \
mail -s "Claude Code doctor failed" admin@company.com </dev/null
```

**2) 日志分析批处理作业**
```bash
# 每日分析，带非交互式 JSON 输出（打印模式）
0 6 * * * tail -1000 /var/log/app.log | \
claude -p "Analyze errors, regressions, and suspect patterns; output JSON." \
--output-format json > /tmp/daily-analysis.json
```

**3) 遥测（可选）**  
Claude Code 发送 OpenTelemetry 指标/事件。在设置/环境变量中设置导出器（例如，OTLP），并发送到您的可观测性堆栈（Datadog、Honeycomb、Prometheus/Grafana 等）。

---

<h2 id="collaboration-best-practices">协作最佳实践</h2>

<h3 id="team-workflows">团队工作流</h3>

**1) 分享版本化配置**
```jsonc
// .claude/settings.json (checked into the repo)
{
  "permissions": {
    "allow": ["Read", "Grep", "LS", "Bash(npm run lint)", "Bash(npm run test:*)"],
    "deny":  ["WebFetch", "Read(./.env)", "Read(./.env.*)", "Read(./secrets/**)"]
  },
  // 如果需要可重现性，在此处固定模型，使用完整的模型 ID：
  "model": "claude-3-5-sonnet-20241022"
}
```

**2) 文档自动化**
```bash
# 使用明确的任务更新文档
claude "Update README.md to reflect the latest API endpoints and examples."
claude "Generate TypeScript types from schema.prisma and write to /types."
```

**3) 代码审查标准**
```bash
# 使用受限工具审查本地差异
git fetch origin main
git diff origin/main...HEAD > /tmp/diff.patch
claude --allowedTools "Read" "Grep" "Bash(git:*)" \
  "Review /tmp/diff.patch using team standards:
   - 安全最佳实践
   - 性能考量
   - 代码风格合规性
   - 测试覆盖率充分性"
```

<h3 id="knowledge-sharing">知识共享</h3>

**1) 项目运行手册**
```bash
claude "Create a deployment runbook for this app: steps, checks, rollback."
claude "Document onboarding for new developers: setup, commands, conventions."
```

**2) 架构文档**
```bash
claude "Update architecture docs to reflect new microservices."
claude "Create sequence diagrams for the authentication flow."
```

> 提示：将持久上下文保存在项目根目录的 **CLAUDE.md** 中。在 REPL 中，使用 `/memory` 管理它，并使用 `@path` 将文件内容导入到提示中。

---

<h2 id="common-pitfalls-to-avoid">要避免的常见陷阱</h2>

<h3 id="security-pitfalls">安全</h3>

**❌ 不要**
- 在生产系统上使用 `--dangerously-skip-permissions`
- 在命令/配置中硬编码密钥
- 授予过于宽泛的权限（例如，`Bash(*)`）
- 不必要地以提升的权限运行

<h2 id="common-pitfalls">常见误区</h2>

**✅ 正确做法**
- 将密钥存储在环境变量和凭证助手中
- 从最小的 `permissions.allow` 开始，逐步扩展
- 使用 `claude config list` / `claude config get` 进行审计
- 在容器/虚拟机中隔离高风险操作

<h3 id="performance-pitfalls">性能</h3>

**❌ 不要**
- 在只需要一个包时加载整个单体仓库
- 为简单任务耗尽思考/轮次预算
- 忽略会话清理

**✅ 要**
- 使用 `--add-dir` 获取聚焦上下文
- 使用 `--max-turns` 和 `MAX_THINKING_TOKENS` 进行适当调整
- 设置 `cleanupPeriodDays` 以修剪旧会话

<h3 id="workflow-pitfalls">工作流程</h3>

**❌ 不要**
- 跳过项目上下文 (`CLAUDE.md`)
- 使用模糊的提示
- 忽略错误/日志
- 未经测试就自动化

**✅ 要**
- 维护和更新 `CLAUDE.md`
- 在提示中具体且目标明确
- 酌情通过日志/OTel进行监控
- 首先在安全环境中测试自动化

---

<h1 id="third-party-integrations">Third-Party Integrations</h1>

<h2 id="deepseek-integration">DeepSeek集成</h2>

1. ###### 已安装Claude Code
```
npm install -g @anthropic-ai/claude-code
```

2. ###### 配置环境变量
```bash
export ANTHROPIC_BASE_URL=https://api.deepseek.com/anthropic
export ANTHROPIC_AUTH_TOKEN=${YOUR_API_KEY}
export ANTHROPIC_MODEL=deepseek-chat
export ANTHROPIC_SMALL_FAST_MODEL=deepseek-chat
```

3. ###### 现在您只需启动 `claude`

从[Deepseek官方文档](https://api-docs.deepseek.com/guides/anthropic_api)中查找更多信息

