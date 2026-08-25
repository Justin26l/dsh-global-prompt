# @dsh-desktop/plugin-global-prompt

[English](README.md) | 中文

[![awesome · DSH plugin](https://awesome-dsh-plugin.com/badge.svg)](https://awesome-dsh-plugin.com)

DeepSeek Harness（DSH）的设置类插件：管理全局 `$DSH_HOME/AGENTS.md` 与各工作区的 `AGENTS.md`，可选注入身份行与人设，控制运行时上下文注入。适用于 DSH Web 与 dsh-desktop Electron 壳。

## 功能

- **全局指令** — 在设置面板编辑 `$DSH_HOME/AGENTS.md`，下一条会话消息即生效，无需重启。
- **项目指令** — 按工作区管理 `AGENTS.md`，路径由 DSH 工作区注册表在服务端解析。
- **双向同步** — 插件外改 `AGENTS.md`，面板能读到；面板保存，文件被重写。两个方向都有内容守卫，不会互相触发写入循环。
- **身份注入** — 可选的 `harness:identity` 段。
- **人设注入** — 可选的 `deployment:persona` 覆盖；`{{model}}`、`{{cwd}}` 占位符由 DSH 渲染时展开。
- **运行时上下文开关** — 不需要时抑制 DSH 官方运行时上下文快照。
- **结果通知** — 桌面壳用系统通知，纯 Web 用浏览器通知。

## 安装

```
dsh plugin add @dsh-desktop/plugin-global-prompt
```

或随 dsh-desktop 安装器内置（默认启用，可在插件管理中关闭）。

bundle patch 会重新启用 `dsh-agent-instructions`（web-app bundle 默认禁用），插件管理的 `AGENTS.md` 由该机制注入。

## 开发

纯 ESM，无构建步骤。`index.js` 为服务端，`client.js` 为设置 UI，`lib/core.js` 为校验工具。

对运行中的 DSH web 服务跑测试脚本：

```
node _tmp/test-global-prompt-sync.mjs
```

## 许可

MIT
