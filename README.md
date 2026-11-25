# dsh-purge-pro

DeepSeek Harness（dsh）插件：一个包内置四个模式——清洗（系统提示词注入与宿主补丁）、红队（舵标/战法/知识库）、逆向（配方/弹药/环境）、软件开发（项目/任务/Git 台账）。装好即用，全部离线。

## 有什么用

- **清洗**：把人设注入 system prompt，让会话按注入的人格与规则工作；对宿主文件打 65 条可回滚补丁（pi-ai、web-app、agent-loop、api-session-controller 等）。
- **红队模式**：舵标（engagement）级资产/端口/指纹/漏洞/凭据/会话台账，SQLite 存储；战法库（playbook）按步骤编排并自动推进；攻击路径图谱（从入口到域控的最短路径与缺口）；离线 CVE 库（411k 条 + nuclei 模板 + ExploitDB + PoC-in-GitHub）；单文件 HTML 报告。
- **逆向模式**：44 条可执行配方（Windows/Linux/macOS/iOS/Android/Web）、25 个落盘脚本（Frida hook、Ghidra 脚本、PE/ELF patch、keygen）、反调试/反虚拟机/反混淆对抗层、环境清单（各平台工具与模拟器）、REA 工具链接入。已并入红队模式，在演练台内切换。
- **软件开发模式**：项目/任务/问题/评审/提交五张台账表，dev_commit 归档 Git 提交；17 篇开发技能（规划、TDD、代码审查、UI 规范、回归门禁、自审清单、Git 纪律等）；交付门禁四件套（验收清单 / UI token / 回归门禁 / 自审）。

## 该怎么用

- **面板**：dsh 里打开插件面板（清洗页签），有体检、应用/还原/卸载、版本与更新卡片；红队/演练台页签里是舵标与战法；逆向子页在演练台内切换。
- **CLI**：`node bin/dsh-purge-pro.js --doctor`（预检 20+ 项）、`--apply`（打补丁）、`--status`、`--playbooks`、`--kb <关键词>`、`--report-html`、`--stats` 等，`--help` 看全量。
- **模式切换**：会话预设下拉里选「无限制模式 / 红队模式 / 软件开发模式」；逆向能力已并入红队模式。
- **数据位置**：`~/.dsh/dsh-purge-pro/`（清洗状态与备份）、`~/.dsh/redteam/`（红队台账与 CVE 库）、`~/.dsh/rev/`（逆向目标与文档）、`~/.dsh/dev/`（开发台账）。

## 支持的 dsh 版本

| dsh 版本 | 状态 |
| --- | --- |
| 0.2.2-rc.3 | ✅ |
| 0.2.2-rc.4 | ✅ |
| 0.2.2-rc.5 | ✅ |
| 0.2.3-alpha.1 | ✅ |
| 0.2.3-alpha.2 | ✅ |

0.2.1 及以下不支持。Node.js >= 22.5.0。

## 怎么安装

把这个仓库链接发给任意 AI agent，让它装：

```
https://github.com/anyehttp/dsh-purge-pro
```

它会去 Releases 下最新的 `dsh-purge-pro-<版本>.zip`，解压到本地目录，再把该目录以 `link:` 依赖挂进 dsh 的 profile，最后重启 dsh。
