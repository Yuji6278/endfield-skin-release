# 终末地 · BAKER — DSH 皮肤

把 [DSH](https://github.com/) Web GUI 改造成《明日方舟：终末地》现场终端的纯 CSS 皮肤。
不是简单换色：会话区按 BAKER 通讯界面整套重做，其余壳层与常见插件页面按终末地工业语汇补齐。
浅色 / 深色共用同一套终端配色。

## 这个皮肤具体做了什么

- **会话区**：青色标头竖条与顶栏标头图、顶栏下方黑色实体收边与三色信号条、信号黄选中行、切角控制台卡片（工具调用 / 思考 / 上下文三类折叠行统一缩进）、白色胶囊输入条、磨砂灰聊天底板。
- **侧栏与壳层**：名录式会话行与工作区行（等宽微标签、单像素浅灰描边）、细网格与斜纹信号条、新建会话入口、tooltip 与设置弹窗描边。
- **其他插件页面适配**：任务看板（新建任务主按钮、卡片与行样式）、SSH 远程运维（新增主机等主按钮）、插件配置卡展开区（网页搜索 / Subagent / Agent 循环 / 终端 / ego-browser 等）、宠物与创意工坊设置卡，均在 `patches.css` 内按功能分节做了结构补丁；未安装的插件对应补丁自然闲置，不会报错。
- **统一调色板**：全部颜色集中在 `skin.css` 的 `:root`（`--ef-*` 原语），改一处全局生效；背景为终末地工业终端图加深色遮罩，随亮 / 暗主题同一套呈现。

## 前置要求

- 本皮肤依赖 dsh-web 的**皮肤 / 皮肤中心**（`packages/dsh-skins` / `packages/skins`）提供加载与应用能力；DSH 原生不识别 `$DSH_HOME/skins/`，没有皮肤中心就无法安装。
- **推荐直接在 `dsh-web-all` 的基础上安装本皮肤**：`dsh-web-all` 是含皮肤中心在内的全家桶聚合包，装完即可应用；本皮肤对全家桶内各插件页面的适配也都能完整生效。
- 已单独安装皮肤中心插件的用户，可跳过聚合包，按下面的手动步骤安装。

## 安装

到 [Releases](../../releases) 下载最新版三个附件：

| 附件 | 用途 |
|---|---|
| `endfield-skin-release-vX.Y.Z.zip` | 皮肤包（解压安装） |
| `baker-skin.md` | 皮肤维护 skill（给 AI Agent） |
| `making-skin.md` | DSH 皮肤制作通用 skill（给 AI Agent） |

zip 内含完整三步安装 / 验收说明（`README.md`，面向 AI Agent），概要：

1. 解压，把 `endfield-baker/` 整个目录放到 `$DSH_HOME/skins/` 下；
2. 应用：设置 → 皮肤中心 → 应用 `endfield-baker`（或 `POST /api/skin-center/v2/active` body `{"active":"endfield-baker"}`）；
3. 验收：打开 `http://127.0.0.1:3080/?bust=<时间戳>`（**必须带 ?bust=**），确认 `data-dsh-skin="endfield-baker"`，且 `GET /api/skin-center/v2/skins/endfield-baker/patches` 返回 200。

## 自己改

skill 文件放到 `$DSH_HOME/skills/<名称>/SKILL.md` 即可被 Agent 加载。皮肤是纯 CSS，改完无需重启。

## 预览

见包内 `preview/light.png` 与 `preview/dark.png`。
