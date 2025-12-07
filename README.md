# asl — AndroidSubsystem4GNU/Linux
[FORK FROM](https://github.com/RuriOSS/asl)
简介 (中文)
----------
ASL（AndroidSubsystem4GNU/Linux）是一个基于 Kam 的 Android 模块，旨在为 Android 设备提供一个轻量、易用、以 Zsh 为默认 shell 的 Linux 子系统运行环境。模块以 `rurima` 为统一入口并提供若干发行版镜像模板（如 Arch / Alpine / CentOS / Debian / Fedora / Kali / Ubuntu），支持 Termux 集成、zsh/Powerlevel10k、.zim 配置，并附带 Web 管理面板（ModuleWebUI）用于日常管理与操作。

主要特性：
- 一键进入 Linux 环境：通过 `rurima` 命令进入模块环境（需 su 权限）
- 多发行版模板：包含并支持多种 Linux 发行版的容器镜像模板
- 方便的管理命令：`rurima pull`、`rurima ota`、`rurima docker`、`rurima backup`、`rurima unpack`、`rurima dep`、`rurima r` 等
- 优化的 shell：zsh + Powerlevel10k + zim，开箱即用的交互体验
- Termux 兼容：当 Termux 存在时提供默认集成
- Web UI ：提供一个本地 Web 面板（ModuleWebUI）来查看状态和进行一些操作（dev）

安装（Install）
---------------
- 预编译的 Release 安装（推荐）：
  1. 前往 Releases 页面，下载你需要的发行版 zip（例如：`asl-ubuntu-oracular-v1.2.3.zip`）。
  2. 在 Magisk Manager / KernelSU 管理器中选择安装该 ZIP。
  3. 安装完成后，重启系统（或根据你的模块管理器提示操作）。
  4. 打开终端（Termux 或 adb shell），先执行 `su`，然后运行 `rurima` 来进入 Linux 子系统。

- 构建并安装（开发或测试）：
  1. 在项目根目录中使用 `kam build` 生成 dist 包（需要已安装 `kam` 工具）。
  2. 在生成的 `dist` 下找到构建产物并通过 Magisk / KernelSU 安装。

使用说明（Usage）
-----------------
- 进入环境：
  - su 后直接运行：
    ```
    su
    rurima
    ```
  - 进入后默认是 zsh 环境，可以享用 `Powerlevel10k`、`zim` 等配置。

- 常用命令示例（在模块环境或借助 `rurima`）：
  - `rurima --help` 或 `rurima -v`： 获取帮助 / 版本信息
  - `rurima pull`： 从远端镜像或仓库拉取镜像/模板（参考模块文档或 `--help` 的具体实现）
  - `rurima ota`： 执行模块容器的 OTA 更新
  - `rurima docker`： rurima 相关的 docker/容器辅助功能
  - `rurima backup`： 备份容器（示例命令，视模块实现可能有详细参数）
  - `rurima unpack`： 解包镜像模板
  - `rurima dep`： 安装依赖
  - `rurima r [command]`： 一次性在 rurima 环境中执行 `[command]`

- 调试与日志：
  - 日志目录：模块内的 `logs/` 或 `/data/adb/modules/asl/logs/`
  - 在 Issues 中报告日志或问题时，把关键的 log 内容贴上可以帮助尽快定位

模块文件结构（简要）
-------------------
- `src/asl/`：模块源码目录（包含 `customize.sh`、`module.prop`、脚本与配置）
  - `system/xbin/rurima`：模块的入口脚本
  - `.rurima.env`：默认环境变量与 Termux 集成配置
  - `.rurimarc` / `.zshrc`：shell 启动脚本与别名、快捷命令
  - `customize.sh`：安装钩子与文件权限修复脚本
  - `uninstall.sh`：卸载脚本

模块 Web 管理界面（ModuleWebUI）
-------------------------------
仓库包含用于本地管理模块的 Web UI（位于 `ModuleWebUI/`）。该 WebUI 提供模块状态展示、日志查看、一些常用操作按钮及设置面板。你可以在本地构建并部署 WebUI（查看 `ModuleWebUI/docs/` 内的详细文档）。

开发与自定义（Customize & Build）
--------------------------------
- 修改安装逻辑、额外文件或权限：编辑 `src/asl/customize.sh`
- 修改模块配置：编辑 `kam.toml`、`module.prop`、`.rurima.env` 或 `.rurimarc`
- 使用 `kam` 构建模块分发：
  - `kam build` → `dist/` 下生成 ZIP 文件
  - 可在 `hooks/` 中添加自定义构建钩子

常见问题（Troubleshooting）
---------------------------
- 无法进入 rurima：
  - 请先确保模块已安装并启用、并在终端里得到 `su` 权限；
  - 确认 `system/xbin/rurima` 权限为 700，并且脚本存在；
  - 如果使用 Termux，请确认 `Termux` 已安装并且 `PATH` 配置正确。

- 无法安装或运行某些命令：
  - 检查 `customize.sh` 对应的权限设置（`set_perm` / `set_perm_recursive`）
  - 检查模块日志目录下的日志是否包含报错信息

反馈与支持（Support）
--------------------
- 报告 issue / 请求功能：请在 GitHub 仓库的 Issues 中提交（https://github.com/Moe-hacker/asl/issues）
- 如果你想贡献：Fork 仓库 → 新分支 → PR，并在 PR 中说明你所做的改动
- 联系作者：`Moe-hacker`, `Lin1328`, `LIghtJUNction`

许可与贡献（License & Contributing）
-----------------------------------
- https://github.com/RuriOSS/asl
- 希腊奶......

- 授权：MIT License（见仓库 LICENSE 文件）

- 欢迎贡献代码、报告 bug、提出 feature request

English Overview
----------------
ASL (AndroidSubsystem4GNU/Linux) is a Kam module for Android that provides a convenient Linux subsystem environment. It provides a consistent shell experience (zsh + Powerlevel10k), supports multiple distro templates, and includes helper commands via the `rurima` entry point to manage images, updates, and backups. A Web-based UI is bundled for easier module management.

Quick start:
1. Download the appropriate release ZIP (e.g., `asl-ubuntu-oracular-v1.2.3.zip`) from the Releases page.
2. Install via Magisk Manager (or KernelSU manager).
3. Reboot if necessary.
4. Open a terminal, run `su`, and execute `rurima` to enter the environment.

Commands / Tips:
- `rurima --help` / `rurima -v` for help and version
- `rurima pull`, `rurima ota`, `rurima backup`, `rurima unpack`, `rurima dep`, `rurima r` are available helpers
- Use the included web UI (ModuleWebUI) to check the module status, logs and quick actions

Build / Customize:
- `kam build` to build module zip files
- Edit `src/asl/customize.sh` and the environment files to modify installation behaviours
- See `ModuleWebUI/docs/` for web UI customization and configuration

Contributors & License:
- Authors: Moe-hacker, Lin1328, LIghtJUNction
- License: MIT

感谢使用 ASL —— 期待你的反馈与贡献！
