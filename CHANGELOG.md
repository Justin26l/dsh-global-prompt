# 更新日志

本项目所有值得记录的变更都会写在这里。

## [0.2.1] - 2026-10-31

### 修复
- 设置面板卡在「正在读取设置…」。dsh 0.2.x 的 `connection` 句柄不再有 `.api` 属性，原代码 `ctx.get('connection').api.workspace.list()` 抛错，被 catch 后面板一直停在 loading。
- 工作区列表改读 `ctx.get('workspaces').list.getSnapshot().items`，并单独兜底：工作区读取失败不再影响配置面板加载。

## [0.2.0] - 2026-10-31

### 破坏性变更
- 适配 dsh `0.2.x`。`@deepseek-ai/dsh-settings` 在 0.2 中移除了 `settingsNamespace` 导出，且 `ctx.settings` 由 `SettingsProvider` 改为 `SettingsForms`，不再提供 `register(ns, schema)`。插件不再注册 settings 命名空间，改为自持久化到 `$DSH_HOME/global-prompt.json`。
- 不再兼容 dsh `0.1.x`；`engines.dsh` 收紧为 `>=0.2.0-rc.1 <0.3.0-0`。

### 修复
- 修复在 dsh `0.2.0-rc.2` / `0.2.1-rc.2` 上启动时报 `does not provide an export named 'settingsNamespace'`、导致插件整体无法加载的问题。

### 说明
- 配置存储位置从 DSH settings 层改为 `$DSH_HOME/global-prompt.json`，功能等价。
- 首次启动仍以磁盘上的 `AGENTS.md` 为准回填配置，不会覆盖用户已有内容。
- 本版本以 scoped 包名 `@justin26l/dsh-global-prompt` 发布（npm 上的 `dsh-global-prompt` 仍归原作者维护）。

## [0.1.2] - 2026-08-25

### 新增
- `AGENTS.md` 与设置面板**双向同步**：插件外改文件，面板能读到；面板保存，文件被重写。两个方向都有内容守卫，不会互相触发写入循环。

### 修复
- 关闭「启用」不再清空你手动维护过的 `AGENTS.md`；禁用状态改由提示词组装层过滤承担。
- 启动时若磁盘上已有 `AGENTS.md`，以磁盘内容为准回填设置，不会被默认空值覆盖。
- 文件监听忽略插件自身的写入，UI 保存不会回写回设置。
- 兼容 Windows 上小写或 `null` 文件名的事件（rename 原子写）。
- 超过 1MiB 的 `AGENTS.md` 不回写进设置（与 PUT 校验一致）。

## [0.1.1] - 2026-08-21

- 独立发布：全局/项目 `AGENTS.md` 编辑器、身份与人设注入、运行时上下文抑制、结果通知、通过 bundle patch 重新启用 `agent-instructions`。
