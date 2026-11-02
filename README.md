# Codex Productivity · 组织文档

本仓库承载 [codex-productivity 组织首页](https://github.com/codex-productivity)与工具体系的公开说明。

- [首页内容](profile/README.md)：用途、架构总览与工具选择。
- [体系架构](docs/architecture.md)：工具职责、调用关系、共享依赖和数据边界。
- [开始使用](docs/getting-started.md)：安装条件、组合顺序与命令示例。
- [架构图](assets/architecture.svg)：可直接编辑的 SVG 源文件。
- [调用关系图](assets/calls.svg)与 [Mermaid 源文件](assets/calls.mmd)：命令调用、文件访问与通信库边界。

## 维护约定

`profile/README.md` 自动展示在 GitHub 组织首页。调整工具职责、调用关系或配置路径时，同步检查首页、架构文档、SVG 与 Mermaid；具体命令与协议仍以各实现仓库为准。

本仓库只保存通用文档与合成示例。个人配置、账号、真实会话与任务、业务上下文和操作证据保存在私有使用层，不进入本仓库。新增内容发布前检查正文、链接、图片与实际暂存文件；使用本机检查，不启用 GitHub Actions。
