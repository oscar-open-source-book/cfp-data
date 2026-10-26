# cfp-data

「OSCAR·开源之书·共读」议题征集（CFP）的公开数据。

## 为什么独立成库

投稿数据若写在 `website/static/` 下，**每有一条投稿就会触发一次完整的
GitHub Pages 构建**（约 4 分钟）。高峰期会排队、互相取消。
独立成库后 `website` 只在页面内容变更时构建。

页面通过 `raw.githubusercontent.com` 读取本仓库的 `proposals.json`。

## 数据来源

历史数据（2021-12 → 2026-09，64 条）导入自腾讯文档表单：
「「开源之书·共读」· 分享Meetup 议题征集（常年有效）（收集结果）」
Drive fileId `1UKpnseZ74_ZEPyLyh07agmG4uHzUEYzf`

之后的新投稿由 `oscar_signup_server.py` 的 `/api/cfp` 端点写入。

## 字段（仅公开部分）

| 字段 | 说明 |
|---|---|
| `id` | 稳定标识，`YYYYMMDD-<sha1前8位>`，由提交日期+标题派生 |
| `speaker` | 分享者称呼（投稿人自填） |
| `submitted_at` | 提交日期 `YYYY-MM-DD` |
| `title` | 议题标题 |
| `summary` | 议题概要 |
| `city` | 城市；`Online` 表示线上 |
| `duration` | 预计时长（多为空） |
| `bio` | 自我介绍（**经投稿人同意公开**——这是展示自己的机会） |

## 隐私边界

**以下字段永远不进入本仓库：**

- `email` —— 联系方式
- `cover` —— 图书封面附件

它们单独存放在内网服务器的 JSONL：
`8.211.12.147:/home/lee/oscar-signups/cfp/proposals.jsonl`

写库顺序：**先写私密库，成功后才写公开 JSON**。私密失败则整单不落。
