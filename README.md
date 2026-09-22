# 终末地 · BAKER — DSH 皮肤

把 [DSH](https://github.com/) Web GUI 改造成《明日方舟：终末地》现场终端的纯 CSS 皮肤：BAKER 会话界面（青色标头竖条、信号黄选中行、切角控制台卡片、白色胶囊输入条、磨砂灰聊天底板）+ 工业语汇壳层（细网格、斜纹信号条、等宽微标签）。浅色 / 深色共用同一套夜航终端配色。

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
3. 验收：打开 `http://127.0.0.1:3080/?bust=<时间戳>`（**必须带 `?bust=`**），确认 `data-dsh-skin="endfield-baker"`，且 `GET /api/skin-center/v2/skins/endfield-baker/patches` 返回 200。

## 自己改

skill 文件放到 `$DSH_HOME/skills/<名称>/SKILL.md` 即可被 Agent 加载。皮肤是纯 CSS，改完无需重启。

## 预览

见包内 `preview/light.png` 与 `preview/dark.png`。
