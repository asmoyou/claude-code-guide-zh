# 变更日志

## 1.0.124

- 设置`CLAUDE_BASH_NO_LOGIN`环境变量为1或true可跳过BashTool的登录shell
- 修复Bedrock和Vertex环境变量将所有字符串评估为真值的问题
- 权限被拒绝时不再向Claude告知允许的工具列表
- 修复了Bash工具权限检查中的安全漏洞
- 改进了VSCode扩展对大文件的处理性能

## 1.0.123

- Bash权限规则现在支持匹配输出重定向(例如`Bash(python:*)`匹配`python script.py > output.txt`)
- 修复了否定短语(如"don't think")意外触发思考模式的问题
- 修复了令牌流传输期间的渲染性能下降问题
- 新增SlashCommand工具，使Claude能够调用您的斜杠命令。https://docs.claude.com/en/docs/claude-code/slash-commands#SlashCommand-tool
- 增强了BashTool环境快照日志记录
- 修复了在无头会话中恢复对话时有时会不必要地启用思考模式的错误
- 将--debug日志迁移到文件，便于跟踪和过滤

## 1.0.120

- 修复了输入延迟问题，在大提示下尤为明显
- 改进了VSCode扩展命令注册表和会话对话框的用户体验
- 增强了会话对话框的响应速度和视觉反馈
- 通过移除工作树支持检查修复了IDE兼容性问题
- 修复了Bash工具权限检查可能被前缀匹配绕过的安全漏洞

## 1.0.119

- 修复了Windows下进入交互模式时进程视觉上冻结的问题
- 通过headersHelper配置支持MCP服务器的动态标头
- 修复了无头会话中思考模式不起作用的问题
- 修复了斜杠命令现在能正确更新允许的工具而非替换它们

## 1.0.117

- 添加Ctrl-R历史搜索功能，可像bash/zsh一样回忆之前的命令
- 修复了输入延迟问题，在Windows上尤为明显
- 在acceptEdits模式下将sed命令添加到自动允许的命令中
- 修复了Windows PATH比较对驱动器字母大小写不敏感的问题
- 在/add-dir输出中添加权限管理提示

## 1.0.115

- 通过增强视觉效果改进了思考模式的显示
- 输入/t可在提示中临时禁用思考模式
- 改进了glob和grep工具的路径验证
- 显示简化的后工具钩子输出以减少视觉混乱
- 修复了加载状态完成时的视觉反馈
- Improve UI consistency for permission request dialogs

## 1.0.113

- Deprecated piped input in interactive mode
- Move Ctrl+R keybinding for toggling transcript to Ctrl+O

## 1.0.112

- Transcript mode (Ctrl+R): Added the model used to generate each assistant message
- Addressed issue where some Claude Max users were incorrectly recognized as Claude Pro users
- Hooks: Added systemMessage support for SessionEnd hooks
- Added `spinnerTipsEnabled` setting to disable spinner tips
- IDE: Various improvements and bug fixes

## 1.0.111

- /model now validates provided model names
- Fixed Bash tool crashes caused by malformed shell syntax parsing

## 1.0.110

- /terminal-setup command now supports WezTerm
- MCP: OAuth tokens now proactively refresh before expiration
- Fixed reliability issues with background Bash processes

## 1.0.109

- SDK: Added partial message streaming support via `--include-partial-messages` CLI flag

## 1.0.106

- Windows: Fixed path permission matching to consistently use POSIX format (e.g., `Read(//c/Users/...)`)

## 1.0.97

- Settings: /doctor now validates permission rule syntax and suggests corrections

## 1.0.94

- Vertex: add support for global endpoints for supported models
- /memory command now allows direct editing of all imported memory files
- SDK: Add custom tools as callbacks
- Added /todos command to list current todo items

## 1.0.93

- Windows: Add alt + v shortcut for pasting images from clipboard
- Support NO_PROXY environment variable to bypass proxy for specified hostnames and IPs

## 1.0.90

- Settings file changes take effect immediately - no restart required

## 1.0.88

- Fixed issue causing "OAuth authentication is currently not supported"
- Status line input now includes `exceeds_200k_tokens`
- Fixed incorrect usage tracking in /cost.
- Introduced `ANTHROPIC_DEFAULT_SONNET_MODEL` and `ANTHROPIC_DEFAULT_OPUS_MODEL` for controlling model aliases opusplan, opus, and sonnet.
- Bedrock: Updated default Sonnet model to Sonnet 4

## 1.0.86

- Added /context to help users self-serve debug context issues
- SDK: Added UUID support for all SDK messages
- SDK: Added `--replay-user-messages` to replay user messages back to stdout

## 1.0.85

- Status line input now includes session cost info
- Hooks: Introduced SessionEnd hook

## 1.0.84

- Fix tool_use/tool_result id mismatch error when network is unstable
- Fix Claude sometimes ignoring real-time steering when wrapping up a task
- @-mention: Add ~/.claude/\* files to suggestions for easier agent, output style, and slash command editing
- Use built-in ripgrep by default; to opt out of this behavior, set USE_BUILTIN_RIPGREP=0

## 1.0.83

- @-mention: Support files with spaces in path
- New shimmering spinner

## 1.0.82

- SDK: Add request cancellation support
- SDK: New additionalDirectories option to search custom paths, improved slash command processing
- Settings: Validation prevents invalid fields in .claude/settings.json files
- MCP: Improve tool name consistency
- Bash: Fix crash when Claude tries to automatically read large files

## 1.0.81

- Released output styles, including new built-in educational output styles "Explanatory" and "Learning". Docs: https://docs.claude.com/en/docs/claude-code/output-styles
- Agents: Fix custom agent loading when agent files are unparsable

## 1.0.80

- UI improvements: Fix text contrast for custom subagent colors and spinner rendering issues

## 1.0.77

- Bash tool: Fix heredoc and multiline string escaping, improve stderr redirection handling
- SDK: Add session support and permission denial tracking
- Fix token limit errors in conversation summarization
- Opus Plan Mode: New setting in `/model` to run Opus only in plan mode, Sonnet otherwise

## 1.0.73

- MCP: Support multiple config files with `--mcp-config file1.json file2.json`
- MCP: Press Esc to cancel OAuth authentication flows
- Bash: Improved command validation and reduced false security warnings
- UI: Enhanced spinner animations and status line visual hierarchy
- Linux: Added support for Alpine and musl-based distributions (requires separate ripgrep installation)

## 1.0.72

- Ask permissions: have Claude Code always ask for confirmation to use specific tools with /permissions

## 1.0.71

- Background commands: (Ctrl-b) to run any Bash command in the background so Claude can keep working (great for dev servers, tailing logs, etc.)
- Customizable status line: add your terminal prompt to Claude Code with /statusline

## 1.0.70

- Performance: Optimized message rendering for better performance with large contexts
- Windows: Fixed native file search, ripgrep, and subagent functionality
- Added support for @-mentions in slash command arguments

## 1.0.69

- Upgraded Opus to version 4.1

## 1.0.68

- Fix incorrect model names being used for certain commands like `/pr-comments`
- Windows: improve permissions checks for allow / deny tools and project trust. This may create a new project entry in `.claude.json` - manually merge the history field if desired.
- Windows: improve sub-process spawning to eliminate "No such file or directory" when running commands like pnpm
- Enhanced /doctor command with CLAUDE.md and MCP tool context for self-serve debugging
- SDK: Added canUseTool callback support for tool confirmation
- Added `disableAllHooks` setting
- Improved file suggestions performance in large repos

## 1.0.65

- IDE: Fixed connection stability issues and error handling for diagnostics
- Windows: Fixed shell environment setup for users without .bashrc files

## 1.0.64

- Agents: Added model customization support - you can now specify which model an agent should use
- Agents: Fixed unintended access to the recursive agent tool
- Hooks: Added systemMessage field to hook JSON output for displaying warnings and context
- SDK: Fixed user input tracking across multi-turn conversations
- Added hidden files to file search and @-mention suggestions

## 1.0.63

- Windows: Fixed file search, @agent mentions, and custom slash commands functionality

## 1.0.62

- Added @-mention support with typeahead for custom agents. @<your-custom-agent> to invoke it
- Hooks: Added SessionStart hook for new session initialization
- /add-dir command now supports typeahead for directory paths
- Improved network connectivity check reliability

## 1.0.61

- Transcript mode (Ctrl+R): Changed Esc to exit transcript mode rather than interrupt
- Settings: Added `--settings` flag to load settings from a JSON file
- Settings: Fixed resolution of settings files paths that are symlinks
- OTEL: Fixed reporting of wrong organization after authentication changes
- Slash commands: Fixed permissions checking for allowed-tools with Bash
- IDE: Added support for pasting images in VSCode MacOS using ⌘+V
- IDE: Added `CLAUDE_CODE_AUTO_CONNECT_IDE=false` for disabling IDE auto-connection
- Added `CLAUDE_CODE_SHELL_PREFIX` for wrapping Claude and user-provided shell commands run by Claude Code

## 1.0.60

- You can now create custom subagents for specialized tasks! Run /agents to get started

## 1.0.59

- SDK: Added tool confirmation support with canUseTool callback
- SDK: Allow specifying env for spawned process
- Hooks: Exposed PermissionDecision to hooks (including "ask")
- Hooks: UserPromptSubmit now supports additionalContext in advanced JSON output
- Fixed issue where some Max users that specified Opus would still see fallback to Sonnet

## 1.0.58

- Added support for reading PDFs
- MCP: Improved server health status display in 'claude mcp list'
- Hooks: Added CLAUDE_PROJECT_DIR env var for hook commands

## 1.0.57

- 添加了对斜杠命令中指定模型的支持
- 改进了权限消息，帮助Claude理解允许的工具
- 修复：移除终端换行中bash输出的尾随换行符

## 1.0.56

- Windows：在支持终端VT模式的Node.js版本上启用了shift+tab模式切换
- 修复了WSL IDE检测问题
- 修复了awsRefreshHelper对.aws目录的更改未被捕获的问题

## 1.0.55

- 明确了Opus 4和Sonnet 4模型的知识截止时间
- Windows：修复了Ctrl+Z崩溃问题
- SDK：添加了捕获错误日志的能力
- 添加了--system-prompt-file选项以在打印模式下覆盖系统提示

## 1.0.54

- 钩子：添加了UserPromptSubmit钩子和当前工作目录到钩子输入
- 自定义斜杠命令：添加了参数提示到前言
- Windows：OAuth使用45454端口并正确构建浏览器URL
- Windows：模式切换现在使用alt + m，计划模式正确渲染
- Shell：切换到内存中的shell快照以修复文件相关错误

## 1.0.53

- 更新了@-mention文件截断从100行到2000行
- 添加了AWS令牌刷新的辅助脚本设置：awsAuthRefresh（用于前台操作如aws sso login）和awsCredentialExport（用于后台操作，带有STS-like响应）。

## 1.0.52

- 添加了对MCP服务器指令的支持

## 1.0.51

- 添加了对原生Windows的支持（需要Git for Windows）
- 通过环境变量AWS_BEARER_TOKEN_BEDROCK添加了对Bedrock API密钥的支持
- 设置：/doctor现在可以帮助你识别和修复无效的设置文件
- `--append-system-prompt`现在可以在交互模式下使用，不仅仅是--print/-p。
- 将自动压缩警告阈值从60%提高到80%
- 修复了处理带空格的用户目录的shell快照问题
- OTEL资源现在包括os.type、os.version、host.arch和wsl.version（如果在Windows子系统Linux上运行）
- 自定义斜杠命令：修复了子目录中的用户级命令
- 计划模式：修复了子任务拒绝的计划会被丢弃的问题

## 1.0.48

- 修复了v1.0.45中应用有时会在启动时冻结的错误
- 为Bash工具添加了基于命令输出最后5行的进度消息
- 为MCP服务器配置添加了变量扩展支持
- 将shell快照从/tmp移动到~/.claude以提高Bash工具调用的可靠性
- 改进了Claude Code在WSL中运行时的IDE扩展路径处理
- 钩子：添加了PreCompact钩子
- Vim模式：添加了c、f/F、t/T命令

## 1.0.45

- 重新设计了搜索(Grep)工具，新增了工具输入参数和功能
- 禁用了笔记本文件的IDE差异功能，修复了"Timeout waiting after 1000ms"错误
- 通过强制执行原子写入修复了配置文件损坏问题
- 将提示输入撤销快捷键更新为Ctrl+\_以避免破坏现有的Ctrl+U行为，匹配zsh的撤销快捷键
- 停止钩子：修复了/clear后的转录路径，并修复了循环以工具调用结束时触发的问题
- 自定义斜杠命令：恢复了基于子目录的命令名称命名空间。例如，.claude/commands/frontend/component.md现在是/frontend:component，而不是/component。

## 1.0.44

- 新的/export命令可让您快速导出对话以供分享
- MCP：现在支持resource_link工具结果
- MCP：工具注释和工具标题现在显示在/mcp视图中
- 将Ctrl+Z更改为挂起Claude Code。通过运行`fg`恢复。提示输入撤销现在是Ctrl+U。

## 1.0.43

- 修复了主题选择器过度保存的错误
- 钩子：添加了EPIPE系统错误处理

## 1.0.42

- 为`/add-dir`命令添加了波浪号(`~`)扩展支持

## 1.0.41

- 钩子：将停止钩子触发拆分为Stop和SubagentStop
- 钩子：为每个命令启用了可选的超时配置
- 钩子：在钩子输入中添加了"hook_event_name"
- 修复了MCP工具在工具列表中显示两次的错误
- 在`tool_decision`事件中为Bash工具新增了工具参数JSON

## 1.0.40

- 修复了当设置`NODE_EXTRA_CA_CERTS`时导致API连接错误UNABLE_TO_GET_ISSUER_CERT_LOCALLY的错误

## 1.0.39

- 在OpenTelemetry日志中新增了活动时间指标

## 1.0.38

- 发布了钩子功能。特别感谢社区在https://github.com/anthropics/claude-code/issues/712中的输入。文档：https://docs.claude.com/en/docs/claude-code/hooks

## 1.0.37

- 移除了通过 ANTHROPIC_AUTH_TOKEN 或 apiKeyHelper 设置 `Proxy-Authorization` 标头的能力

## 1.0.36

- 网络搜索现在会考虑今天的日期作为上下文
- 修复了 stdio MCP 服务器在退出时未正确终止的错误

## 1.0.35

- 新增对 MCP OAuth 授权服务器发现的支持

## 1.0.34

- 修复了导致出现 MaxListenersExceededWarning 的内存泄漏问题

## 1.0.33

- 改进了日志功能，支持会话 ID
- 新增提示输入撤销功能（Ctrl+Z 和 vim 的 'u' 命令）
- 计划模式改进

## 1.0.32

- 更新了 litellm 的回环配置
- 新增 forceLoginMethod 设置以跳过登录选择界面

## 1.0.31

- 修复了当 ~/.claude.json 文件包含无效 JSON 时会被重置的错误

## 1.0.30

- 自定义斜杠命令：运行 bash 输出、@ 提及文件、使用思考关键词启用思考模式
- 改进了文件路径自动补全，支持文件名匹配
- 在 Ctrl-r 模式中新增时间戳，并修复了 Ctrl-c 的处理
- 增强了对 jq 正则表达式的支持，支持带管道和 select 的复杂过滤器

## 1.0.29

- 改进了光标导航和渲染中对中日韩字符的支持

## 1.0.28

- 修复了在历史记录导航过程中斜杠命令选择器显示的问题
- 在上传前调整图像大小以防止API大小限制错误
- 新增对配置目录的XDG_CONFIG_HOME支持
- 内存使用的性能优化
- 在OpenTelemetry日志中新增属性（terminal.type、language）

## 1.0.27

- 现已支持可流式传输的HTTP MCP服务器
- 远程MCP服务器（SSE和HTTP）现已支持OAuth
- MCP资源现在可以通过@提及
- 新增/resume斜杠命令以在Claude Code内切换对话

## 1.0.25

- 斜杠命令：将“project”和“user”前缀移至描述中
- 斜杠命令：提高了命令发现的可靠性
- 改进了对Ghostty的支持
- 提高了网络搜索的可靠性

## 1.0.24

- 改进了/mcp输出
- 修复了设置数组被覆盖而非合并的错误

## 1.0.23

- 发布TypeScript SDK：导入@anthropic-ai/claude-code开始使用
- 发布Python SDK：pip install claude-code-sdk开始使用

## 1.0.22

- SDK：将`total_cost`重命名为`total_cost_usd`

## 1.0.21

- 改进了对使用制表符缩进的文件的编辑
- 修复了tool_use无匹配tool_result错误的问题
- 修复了退出Claude Code后stdio MCP服务器进程残留的错误

## 1.0.18

- Added --add-dir CLI argument for specifying additional working directories
- Added streaming input support without require -p flag
- Improved startup performance and session storage performance
- Added CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR environment variable to freeze working directory for bash commands
- Added detailed MCP server tools display (/mcp)
- MCP authentication and permission improvements
- Added auto-reconnection for MCP SSE connections on disconnect
- Fixed issue where pasted content was lost when dialogs appeared

## 1.0.17

- We now emit messages from sub-tasks in -p mode (look for the parent_tool_use_id property)
- Fixed crashes when the VS Code diff tool is invoked multiple times quickly
- MCP server list UI improvements
- Update Claude Code process title to display "claude" instead of "node"

## 1.0.11

- Claude Code现在也可通过Claude Pro订阅使用
- 新增/upgrade命令，便于平滑切换到Claude Max计划
- 改进了通过API密钥及Bedrock/Vertex/外部认证令牌进行身份验证的UI
- 改进了shell配置错误处理
- 改进了压缩过程中的待办事项处理

## 1.0.10

- 新增Markdown表格支持
- 改进了流式传输性能
- 修复了Claude有时无法看到命令完整输出的错误
- 修复了Claude无法看到命令完整输出的问题
- 修复了Claude有时无法看到命令完整输出的错误

## 1.0.8

- 修复了使用CLOUD_ML_REGION时Vertex AI区域回退的问题
- 将默认otel间隔从1秒增加到5秒
- 修复了MCP_TIMEOUT和MCP_TOOL_TIMEOUT未被遵守的边界情况
- 修复了搜索工具不必要请求权限的回归问题
- 新增对非英语语言触发思考模式的支持
- 改进了压缩UI
- 修复了Claude有时无法看到命令完整输出的错误
- 修复了Claude无法看到命令完整输出的问题
- 修复了Claude有时无法看到命令完整输出的错误

## 1.0.7

- 将/allowed-tools重命名为/permissions
- 将allowedTools和ignorePatterns从.claude.json迁移到settings.json
- 弃用claude config命令，改为直接编辑settings.json
- 修复了--dangerously-skip-permissions在--print模式下有时不生效的bug
- 改进了/install-github-app的错误处理
- 错误修复、UI优化及工具可靠性改进
- 修复了Claude有时无法看到命令完整输出的错误
- 修复了Claude无法看到命令完整输出的问题
- 修复了Claude有时无法看到命令完整输出的错误

## 1.0.6

- Improved edit reliability for tab-indented files
- Respect CLAUDE_CONFIG_DIR everywhere
- Reduced unnecessary tool permission prompts
- Added support for symlinks in @file typeahead
- Bugfixes, UI polish, and tool reliability improvements
- 修复了Claude有时无法看到命令完整输出的错误
- 修复了Claude无法看到命令完整输出的问题
- 修复了Claude有时无法看到命令完整输出的错误

## 1.0.4

- Fixed a bug where MCP tool errors weren't being parsed correctly
- 修复了Claude有时无法看到命令完整输出的错误
- 修复了Claude无法看到命令完整输出的问题
- 修复了Claude有时无法看到命令完整输出的错误

## 1.0.1

- Added `DISABLE_INTERLEAVED_THINKING` to give users the option to opt out of interleaved thinking.
- Improved model references to show provider-specific names (Sonnet 3.7 for Bedrock, Sonnet 4 for Console)
- Updated documentation links and OAuth process descriptions
- 修复了Claude有时无法看到命令完整输出的错误
- 修复了Claude无法看到命令完整输出的问题
- 修复了Claude有时无法看到命令完整输出的错误

## 1.0.0

- Claude Code is now generally available
- Introducing Sonnet 4 and Opus 4 models
- 修复了Claude有时无法看到命令完整输出的错误
- 修复了Claude无法看到命令完整输出的问题
- 修复了Claude有时无法看到命令完整输出的错误

## 0.2.125

- Breaking change: Bedrock ARN passed to `ANTHROPIC_MODEL` or `ANTHROPIC_SMALL_FAST_MODEL` should no longer contain an escaped slash (specify `/` instead of `%2F`)
- Removed `DEBUG=true` in favor of `ANTHROPIC_LOG=debug`, to log all requests
- 修复了Claude有时无法看到命令完整输出的错误
- 修复了Claude无法看到命令完整输出的问题
- 修复了Claude有时无法看到命令完整输出的错误

## 0.2.117

- 重大变更：--print JSON 输出现在返回嵌套消息对象，以便在引入新元数据字段时保持向前兼容
- 新增 settings.cleanupPeriodDays 设置
- 新增 CLAUDE_CODE_API_KEY_HELPER_TTL_MS 环境变量
- 新增 --debug 调试模式

## 0.2.108

- 现在可以在 Claude 工作时发送消息以实时引导 Claude
- 新增 BASH_DEFAULT_TIMEOUT_MS 和 BASH_MAX_TIMEOUT_MS 环境变量
- 修复了 -p 模式下思考模式不起作用的错误
- 修复了 /cost 报告中的回归问题
- 弃用 MCP 向导界面，改用其他 MCP 命令
- 许多其他错误修复和改进

## 0.2.107

- CLAUDE.md 文件现在可以导入其他文件。在 ./CLAUDE.md 中添加 @path/to/file.md 以在启动时加载额外文件

## 0.2.106

- MCP SSE 服务器配置现在可以指定自定义标头
- 修复了 MCP 权限提示有时显示不正确的错误

## 0.2.105

- Claude 现在可以搜索网页
- 将系统和账户状态移至 /status 命令
- 为 Vim 添加了单词移动键绑定
- 改进了启动、待办事项工具和文件编辑的延迟

## 0.2.102

- 提高了思考模式触发的可靠性
- 改进了对图像和文件夹的 @mention 可靠性
- 现在可以在一个提示中粘贴多个大块内容

## 0.2.100

- 修复了由堆栈溢出错误导致的崩溃
- 使数据库存储变为可选；缺少数据库支持将禁用 --continue 和 --resume

## 0.2.98

- 修复了自动压缩运行两次的问题

## 0.2.96

- Claude Code 现在也可以通过 Claude Max 订阅使用 (https://claude.ai/upgrade)

## 0.2.93

- 使用 "claude --continue" 和 "claude --resume" 可从上次中断的地方恢复对话
- Claude 现在可以使用待办事项列表来帮助保持专注和更有条理

## 0.2.82

- 新增对 --disallowedTools 的支持
- 为保持一致性重命名工具：LSTool -> LS，View -> Read 等

## 0.2.75

- 在 Claude 工作时按 Enter 可排队发送额外消息
- 可直接将图片文件拖入或复制/粘贴到提示中
- 使用 @ 提及文件可直接将其加入上下文
- 使用 `claude --mcp-config <path-to-file>` 运行一次性 MCP 服务器
- 改进了文件名自动补全性能

## 0.2.74

- 新增对动态生成 API 密钥刷新的支持（通过 apiKeyHelper），TTL 为 5 分钟
- Task 工具现在可执行写入操作并运行 bash 命令

## 0.2.72

- 更新加载动画，以显示已加载的令牌和工具使用情况

## 0.2.70

- 网络命令（如 curl）现在可供 Claude 使用
- Claude 现在可并行运行多个网络查询
- 在自动接受模式下，按一次 ESC 即可立即中断 Claude

## 0.2.69

- 通过改进 Select 组件行为修复 UI 故障
- 增强终端输出显示，改进文本截断逻辑

## 0.2.67

- 共享项目权限规则可保存在 .claude/settings.json 中

## 0.2.66

- 打印模式 (-p) 现在通过 --output-format=stream-json 支持流式输出
- 修复了粘贴可能意外触发内存或 bash 模式的问题

## 0.2.63

- 修复了MCP工具被重复加载导致工具调用错误的问题

## 0.2.61

- 使用 vim 风格键位（j/k）或 bash/emacs 快捷键（Ctrl+n/p）快速导航菜单
- 增强图像检测，使剪贴板粘贴功能更可靠
- 修复了 ESC 键可能导致对话历史选择器崩溃的问题

## 0.2.59

- 可直接将图像复制并粘贴到提示中
- 改进了 bash 和 fetch 工具的进度指示器
- 修复了非交互模式（-p）的若干错误

## 0.2.54

- 以“#”开头快速添加到记忆
- 按 ctrl+r 查看长工具结果的完整输出
- 新增对 MCP SSE 传输的支持

## 0.2.53

- 新增网页获取工具，让 Claude 可以查看您粘贴的 URL
- 修复了 JPEG 检测的错误

## 0.2.50

- 新增 MCP “project” 作用域，现在可将 MCP 服务器添加到 .mcp.json 文件并提交到仓库

## 0.2.49

- 重命名 MCP 服务器作用域：原“project”作用域现为“local”，原“global”作用域现为“user"

## 0.2.47

- 按 Tab 自动补全文件和文件夹名称
- 按 Shift + Tab 切换文件编辑的自动接受
- 自动压缩对话以实现无限长度（通过 /config 开关）

## 0.2.44

- 让 Claude 制定计划：只需说“think”、“think harder”或“ultrathink”即可进入思考模式

## 0.2.41

- 现在可通过 MCP_TIMEOUT 环境变量配置 MCP 服务器启动超时
- MCP 服务器启动不再阻塞应用启动

## 0.2.37

- 新增 /release-notes 命令，可随时查看发行说明
- `claude config add/remove` 命令现在接受以逗号或空格分隔的多个值

## 0.2.36

- 使用 `claude mcp add-from-claude-desktop` 从 Claude Desktop 导入 MCP 服务器
- 使用 `claude mcp add-json <n> <json>` 以 JSON 字符串形式添加 MCP 服务器

## 0.2.34

- 文本输入支持 Vim 绑定 - 通过 /vim 或 /config 启用

## 0.2.32

- 交互式 MCP 设置向导：运行 "claude mcp add" 以分步界面添加 MCP 服务器
- 修复了一些 PersistentShell 问题

## 0.2.31

- 自定义斜杠命令：.claude/commands/ 目录中的 Markdown 文件现在会作为自定义斜杠命令出现，用于将提示插入对话
- MCP 调试模式：使用 --mcp-debug 标志运行以获取有关 MCP 服务器错误的更多信息

## 0.2.30

- 添加了 ANSI 颜色主题以获得更好的终端兼容性
- 修复了斜杠命令参数未正确发送的问题
- （仅限 Mac）API 密钥现在存储在 macOS 钥匙串中

## 0.2.26

- 新的 /approved-tools 命令用于管理工具权限
- 单词级差异显示以提高代码可读性
- 斜杠命令的模糊匹配

## 0.2.21

- /commands 的模糊匹配
