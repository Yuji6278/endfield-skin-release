# 终末地 · BAKER — DSH 皮肤

把 [DSH](https://github.com/deepseek-ai/deepseek-harness/) Web GUI 改造成《明日方舟：终末地》现场终端的纯 CSS 皮肤。
不是简单换色：会话区按 BAKER 通讯界面整套重做，其余壳层与常见插件页面按终末地工业语汇补齐。
浅色 / 深色共用同一套终端配色。

## 效果预览

点击图片查看完整尺寸。

<img width="2547" height="1243" alt="v0 8 0-1" src="https://github.com/user-attachments/assets/0b0876f1-f404-4168-b82a-61e6ad270e5d" />
<img width="2559" height="1259" alt="v0 8 0-2" src="https://github.com/user-attachments/assets/44769e12-9cb2-4b4d-a34c-15776b0dc67b" />
<img width="2559" height="1254" alt="v0 8 0-3" src="https://github.com/user-attachments/assets/8ac0348a-a152-44b3-9cd7-77a3a3c62645" />
<img width="2559" height="1248" alt="v0 8 0-4" src="https://github.com/user-attachments/assets/cffe1d02-1219-4bfc-b735-a335d99e70f8" />

## 这个皮肤具体做了什么

- **会话区**：青色标头竖条与顶栏标头图、顶栏下方黑色实体收边与三色信号条、信号黄选中行、切角控制台卡片（工具调用 / 思考 / 上下文三类折叠行统一缩进）、白色胶囊输入条、磨砂灰聊天底板。
- **侧栏与壳层**：名录式会话行与工作区行（等宽微标签、单像素浅灰描边）、细网格与斜纹信号条、新建会话入口、tooltip 与设置弹窗描边。
- **其他插件页面适配**：任务看板（新建任务主按钮、卡片与行样式）、SSH 远程运维（新增主机等主按钮）、插件配置卡展开区（网页搜索 / Subagent / Agent 循环 / 终端 / ego-browser 等）、宠物与创意工坊设置卡，均在 `patches.css` 内按功能分节做了结构补丁；未安装的插件对应补丁自然闲置，不会报错。
- **统一调色板**：全部颜色集中在 `skin.css` 的 `:root`（`--ef-*` 原语），改一处全局生效；背景为终末地工业终端图加深色遮罩，随亮 / 暗主题同一套呈现。

## 前置要求

- 本皮肤依赖 [dsh-web](https://github.com/zhu1090093659/dsh-web) 的**皮肤 / 皮肤中心**（`packages/dsh-skins` / `packages/skins`）提供加载与应用能力；DSH 原生不识别 `$DSH_HOME/skins/`，没有皮肤中心就无法安装。
- **推荐直接在 `dsh-web-all` 的基础上安装本皮肤**：`dsh-web-all` 是含皮肤中心在内的全家桶聚合包，装完即可应用；本皮肤对全家桶内各插件页面的适配也都能完整生效。
- 已单独安装皮肤中心插件的用户，可跳过聚合包，按下面的手动步骤安装。

## 安装

可以让 AI Agent 按照本 README 与 zip 内的 `README.md`（面向 Agent 的三步安装 / 验收说明）完成下载与安装；本皮肤上线 [DSH-Market](https://dsh-market.com) 后也可以在创意工坊直接安装。

到 [Releases](../../releases) 下载皮肤包附件，两个 skill 文件按需下载：

| 附件 | 用途 |
|---|---|
| `endfield-skin-release-vX.Y.Z.zip` | 皮肤包（解压安装） |
| `baker-skin.md` | 皮肤维护 skill（给 AI Agent ，皮肤元素有Bug时协助修改） |
| `making-skin.md` | DSH 皮肤制作通用 skill（给 AI Agent ，想自己做皮肤可以参考使用） |

zip 内含完整三步安装 / 验收说明（`README.md`，面向 AI Agent），概要：

1. 解压，把 `endfield-baker/` 整个目录放到 `$DSH_HOME/skins/` 下；
2. 应用：设置 → 皮肤中心 → 应用 `endfield-baker`（或 `POST /api/skin-center/v2/active` body `{"active":"endfield-baker"}`）；
3. 验收：打开 `http://127.0.0.1:3080/?bust=<时间戳>`（**必须带 ?bust=**），确认 `data-dsh-skin="endfield-baker"`，且 `GET /api/skin-center/v2/skins/endfield-baker/patches` 返回 200。

## 自己改 / 按设备微调

skill 文件放到 `$DSH_HOME/skills/<名称>/SKILL.md` 即可被 Agent 加载。皮肤是纯 CSS，改完无需重启，只需刷新浏览器重进页面以加载新的修改项。

环境相关参数集中在 `skin.css` 的 `:root` 一处：

| 场景 | 调整 |
|---|---|
| 屏幕 / 侧栏宽度差异大 | `--ef-bk`（侧栏名录整体缩放系数） |
| 输入条高度 / 留白 | `--ef-input-max` / `--ef-input-inset` / `--ef-input-pad` |
| 顶栏右侧图形比例 | `--ef-art-ratio`（需与 patches.css 第 2 节两处同步） |
| 用户机器缺字体 | `--ef-baker-font` 回退链里加本地字体名 |

## 兼容性

- 平台：Web
- 依赖：dsh-web 皮肤中心（`packages/dsh-skins` / `packages/skins`）或 `dsh-web-all`
- 浏览器：纯 CSS 皮肤，Chromium 系通用；`:has()` / `color-mix()` 需要较新内核（Chromium 105+ / 116+）
- 最近验证日期：2026-09-22（v0.8.0 发布，门禁全绿）

## 更新日志

### v0.8.0 — 2026-09-22

- 首个公开发布：皮肤包 zip + `baker-skin.md` / `making-skin.md` 两个 skill 附件
- 同步提交上游 dsh-web 创意工坊：[PR #1679](https://github.com/zhu1090093659/dsh-web/pull/1679)

历史版本与附件见 [Releases](../../releases)。

## 致谢

| 来源 | 说明 |
|---|---|
| Nuclear_Creeper（bilibili） | 参考截图与纹理素材来自其所制作的网站 [Baker AI](https://chat.peilika.beer/) |
| blue-fantasy（powerdog996 / DreamSkin 社区） | 本皮肤的改作基础 |
| [dsh-web](https://github.com/zhu1090093659/dsh-web)（zhu1090093659） | 皮肤中心（skin-center）的加载与应用能力 |
| [DSH](https://github.com/deepseek-ai/deepseek-harness/) | 本体与 Web GUI |

* 反馈问题请在 issue 中发起。

## 许可

本仓库以 **CC BY-NC-SA 4.0**（署名-非商业性使用-相同方式共享）发布，禁止商业性使用；署名链见「致谢」一节与 `skin.json` 的 `author` 字段，完整协议文本见仓库内 `LICENSE`。

Arknights: Endfield and related artwork referenced here are trademarks of Hypergryph (鹰角网络). This skin is a fan work and is not affiliated with or endorsed by Hypergryph.
