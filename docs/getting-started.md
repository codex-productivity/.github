# 开始使用 Codex Productivity

先按需要选择工具，再添加项目管理、账号或标题能力。阅读[组织首页](https://github.com/codex-productivity)可了解各工具用途，阅读[体系架构](architecture.md)可了解调用与数据边界。

## 安装前

- 已安装并配置好 Codex CLI。
- 已安装 Git、Python 3.11 或更新版本，以及 [uv](https://docs.astral.sh/uv/)；常用命令需在 `PATH` 中。
- 本系列主要面向本地终端工作流，当前以 macOS 使用环境为主；Shell 集成示例使用 Bash。各工具的平台能力以对应仓库说明为准。
- 八个工具源码仓库目前为私有。需要读取所选应用及其共享依赖仓库的权限，才能安装。

以下命令使用 GitHub SSH 访问应用源码。共享依赖固定到完整 Git commit，依赖 URL 可能使用 HTTPS；应在本机正确配置相应 Git 认证，或采用各仓库说明中的 HTTPS 到 SSH 转换。不要在安装 URL、命令记录或文档中写入令牌。

## 按场景安装

### 便捷启动 Codex

```bash
uv tool install --python 3.11 'git+ssh://git@github.com/codex-productivity/codex.helper.git@main'
codex.helper --help
```

helper 适合已有自己的项目组织方式、只想统一启动参数和模型别名的用户。

### 在现有目录管理任务

在 helper 之外安装 migrate 和 task：

```bash
uv tool install --python 3.11 'git+ssh://git@github.com/codex-productivity/codex.migrate.git@main'
uv tool install --python 3.11 'git+ssh://git@github.com/codex-productivity/codex.task.git@main'
codex.task --help
```

在目标项目目录中，以下命令仅查询当前任务：

```bash
codex.task list
```

准备执行真实需求时，可使用下面的形式；它会进入需求整理和执行流程，按 Codex 配置使用模型：

```bash
codex.task do '为示例项目补充输入校验'
```

如需先形成待办、稍后执行，使用 `codex.task publish`；已有任务的恢复方式见 `codex.task run --help`。查看其他目录时可显式传入路径：

```bash
codex.task -C /path/to/project list
```

### 统一管理多个项目

在上述任务组合之上安装 project：

```bash
uv tool install --python 3.11 'git+ssh://git@github.com/codex-productivity/codex.project.git@main'
codex.project --help
```

按 [project 的配置与使用说明](https://github.com/codex-productivity/codex.project#readme)设置项目根目录和分组。需要让 `go` 切换当前 Bash 的目录时安装 Shell 集成：

```bash
codex.project shell-install bash
```

此操作维护 Bash 启动文件。当前已经打开的 Bash 可执行一次初始化，使当前终端立即生效：

```bash
eval "$(command codex.project shell-init bash)"
```

随后可通过 `codex.project task list` 使用当前受管项目的任务入口。`c` 等短命令属于用户在 `[shell.aliases]` 中配置的别名；本文统一使用完整命令，避免依赖个人设置。

### 按需添加独立能力

| 需要的能力 | 安装入口 | 查询示例 |
| --- | --- | --- |
| 账号和用量管理 | [codex.tool README](https://github.com/codex-productivity/codex.tool#readme) | `codex.tool auth list` |
| 当前会话和历史标题维护 | [codex.session README](https://github.com/codex-productivity/codex.session#readme) | `codex.session title get --json` |
| 查询配置与私有数据路径 | [codex.config README](https://github.com/codex-productivity/codex.config#readme) | `codex.config paths --workspace . --json` |

当前标题命令需在可识别目标会话的环境中运行；完整条件见 session 的说明。应用安装会解析需要的 config、appserver 库，但不会自动把其他应用的可执行文件装进 `PATH`；需要 `codex.config` 命令时单独安装它。

## 安装后检查

1. 确认所选工具的 `--help` 或版本命令可运行。
2. 在目标目录执行 `codex.task list`，确认所查看的工作区正确，再创建任务。
3. 查询生效配置与运行数据位置，确认它们指向私有存储。已有任务数据需要按[迁移边界](architecture.md#迁移与外部数据)处理。

以上安装示例跟随各仓库的 `main` 分支。需要可重复部署时，可将 `@main` 替换为经过验证的完整 commit；应用中的共享库依赖由各仓库固定。升级后仍需验证实际命令入口和受影响功能，不能只以源码已更新作为安装完成的依据。
