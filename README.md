# dsh-purge-pro

DeepSeek Harness（dsh）插件：一个包内置四个模式——清洗（系统提示词注入与宿主补丁）、红队（台账/战法/知识库）、逆向（配方/弹药/环境）、软件开发（项目/任务/Git 台账）。装好即用，全部离线。

## 有什么用

- **清洗**：把人设注入 system prompt，让会话按注入的人格与规则工作；对宿主文件打 65 条可回滚补丁（pi-ai、web-app、agent-loop、api-session-controller 等）。
- **红队模式**：舵标（engagement）级资产/端口/指纹/漏洞/凭据/会话台账，SQLite 存储；战法库（playbook）按步骤编排并自动推进；攻击路径图谱（从入口到域控的最短路径与缺口）；离线 CVE 库（411k 条 + nuclei 模板 + ExploitDB + PoC-in-GitHub）；单文件 HTML 报告。
- **逆向模式**：44 条可执行配方（Windows/Linux/macOS/iOS/Android/Web）、25 个落盘脚本（Frida hook、Ghidra 脚本、PE/ELF patch、keygen）、反调试/反虚拟机/反混淆对抗层、环境清单（各平台工具与模拟器）、REA 工具链接入。
- **软件开发模式**：项目/任务/问题/评审/提交五张台账表，dev_commit 归档 Git 提交；17 篇开发技能（规划、TDD、代码审查、UI 规范、回归门禁、自审清单、Git 纪律等）；交付门禁四件套（验收清单/UI token/回归门禁/自审）。

## 该怎么用

- **面板**：dsh 里打开插件面板（清洗页签），有体检、应用/还原/卸载、版本与更新卡片；红队/演练台页签里是舵标与战法；逆向子页在演练台内。
- **CLI**：`node bin/dsh-purge-pro.js --doctor`（预检 20+ 项）、`--apply`（打补丁）、`--status`、`--playbooks`、`--kb <关键词>`、`--report-html`、`--stats` 等，`--help` 看全量。
- **模式切换**：会话预设下拉里选「无限制模式 / 红队模式 / 软件开发模式」；逆向能力已并入红队模式。
- **数据位置**：`~/.dsh/dsh-purge-pro/`（清洗状态与备份）、`~/.dsh/redteam/`（红队台账与 CVE 库）、`~/.dsh/rev/`（逆向目标与文档）、`~/.dsh/dev/`（开发台账）。

## 支持的 dsh 版本

| dsh 版本 | 状态 | 验证方式 |
| --- | --- | --- |
| 0.2.2-rc.3 | ✅ 支持 | 本机全量真打（65/65 applied，语法 0 失败） |
| 0.2.2-rc.4 | ✅ 支持 | 全量真打（65/65） |
| 0.2.2-rc.5 | ✅ 支持 | 全量真打（65/65） |
| 0.2.3-alpha.1 | ✅ 支持 | 全量真打（65/65） |
| 0.2.3-alpha.2 | ✅ 支持 | 全量真打（65/65） |

- 插件声明：`dshTargets` 覆盖上表五个版本，`dshTarget` 指向 0.2.3-alpha.2。
- Node.js 要求：**>= 22.5.0**（红队/开发台账用内置 `node:sqlite`，FTS5 不可用时自动降级）。
- 更老的 dsh（0.2.1 及以下）不在支持范围：宿主源码结构差异过大，补丁锚点会落空。
- 换版本后建议跑一次 `node bin/dsh-purge-pro.js --doctor`，全绿再 `--apply`。

## 怎么安装

### 给 AI 的安装说明（复制给任意 agent 执行）

1. 下载本页最新 release 的 `dsh-purge-pro-<版本>.zip` 并解压到任意目录，得到插件源目录（内含 package.json、lib/、bin/ 等）。
2. 找到 dsh 的 profile 目录（默认 `~/.dsh/profiles/desktop/`，飞牛/web 端是 `~/.dsh/profiles/web/`，即包含 `package.json` 与 `node_modules/` 的那个）。
3. 在 profile 的 `package.json` 的 `dependencies` 里加一行：`"dsh-purge-pro": "link:<插件源目录绝对路径>"`（Windows 路径用正斜杠，如 `link:C:/tools/dsh-purge-pro`）。
4. 在 profile 的 `node_modules/` 下建链接指向插件源目录（Windows：`mklink /J node_modules\dsh-purge-pro <插件源目录>`；Linux/macOS：`ln -s <插件源目录> node_modules/dsh-purge-pro`）。
5. 重启 dsh（桌面端重启应用；飞牛/web 端重启 Harness 服务）。
6. 重启后验证：开一个新会话，在插件面板点「体检」应全绿；预设下拉应出现各模式；`node <插件源目录>/bin/dsh-purge-pro.js --status` 应显示 65/65。

### 人工安装（同上，只是自己动手）

按上面六步操作即可；第 3-4 步是把插件以本地 link 依赖挂进 profile，不要用 npm install（该插件不发布 npm）。

## 更新

面板「版本与更新」卡片可勾选每 6 小时检查 GitHub Releases；发现新版可一键下载安装，安装后按页面提示重启 dsh 生效。
