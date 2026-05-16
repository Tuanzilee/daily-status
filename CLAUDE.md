# CLAUDE.md

## Repo 用途

每日狀態紀錄文字生成器。填表單 → 生成 emoji 開頭的純文字段 → 複製到 Notion。**Notion 是真理之源**,本 app 純 input helper,不存任何東西、重整就清空。

線上部署:**https://tuanzilee.github.io/daily-status/**(GitHub Pages,push 後 1-2 分鐘自動部署)

姊妹專案:`~/Desktop/psy/`、`~/Desktop/stats/`、`~/Desktop/eng/`、`~/Desktop/wri/`(全部是 quiz / 範本類,**性質不同**,別套錯架構)。

## 檔案結構

```
daily-status/
├── index.html       ← 主程式(593 行,19KB)。源 = 部署檔,直接改
├── README.md
└── CLAUDE.md        ← 本檔
```

## 四個維度(全部 hardcode 在 index.html `<script>` 區)

| 維度 | 變數 | 行號 | 內容 |
|---|---|---|---|
| 狀態等級 | `LEVELS` | 447 | 🟢 Lv1-2 / 🟡 Lv3-4 / 🟠 Lv5-6 / 🔴 Lv7-8 / ⚫ Lv9-10 |
| 硬推狀態 | `PUSHES` | 454 | ✅ 滑順 / ⚠️ 有點 / 🚨 硬推 |
| 影響因素(多選 + 可自訂) | `DEFAULT_TAGS` | 459 | 睡眠不足/充足、壓力大、身體不適、飲食不佳、心情好、焦慮、運動恢復中 |
| 學習模式(每科目下拉) | `MODES` | 460 | 深度學習 / 做題目 / 輕量複習 / 錯題整理 / AI 輔助 |

自訂 tag 走 `customTags` 陣列(in-memory only,重整就消)。

## 跟其他 4 個 repo 的差異

| | psy | stats | eng | wri | **daily-status** |
|---|---|---|---|---|---|
| 性質 | 考古題 | 考古題 PWA | 考古題 | 範本抽卡 | **狀態紀錄生成器** |
| 持久化 | localStorage | localStorage + SW | localStorage | localStorage + Gist | **❌ 完全無** |
| 子系統數 | 1 | 1 | 2 | 3 | **0(線性表單)** |
| Build / PWA / AI / fetch | 看各 repo | 看各 repo | 看各 repo | 看各 repo | **全無** |
| 檔案數 | 27 | 8 | 6 | 3 | **1 個 .html** |

→ daily-status 是 **5 個 repo 裡最瘦的**。性質跟其他 4 個都不同,**不要拿任何一個的工程化模板套上來**。

## 不要做的事(精瘦路線,2026-05-16 確認)

- ❌ **不加 localStorage 持久化** — Notion 是真理之源,本 app 不該存歷史
- ❌ **不補完 PWA**(`manifest.json` + `sw.js`) — 已有 apple-mobile-web-app meta 半套就夠
- ❌ **不接 Notion API 直送** — 複製貼上的 UX 成本低於 token 設定成本
- ❌ **不加 AI hint**(Anthropic API)
- ❌ **不加 build pipeline / template / Actions**
- ❌ **不拆子系統** — 線性表單就夠

## 工作流(改維度)

1. 編輯 `index.html` 的 `<script>` 區常數(`LEVELS` / `PUSHES` / `DEFAULT_TAGS` / `MODES`)
2. `git add index.html && git commit -m "..." && git push origin main`
3. GitHub Pages 1-2 分鐘自動部署

**不要再用 GitHub web 拖拉上傳**(早期 2 個 commit 是這樣建的,已切到 git CLI)。
