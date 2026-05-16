# 每日狀態記錄

填表單 → 生成 emoji 開頭的純文字 → 複製到 Notion 的單頁工具。無後端、無持久化、重整就清空。

## 線上

**https://tuanzilee.github.io/daily-status/**

iOS Safari 可「分享 → 加入主畫面」,有 apple-mobile-web-app meta 標籤支援。

## 本機啟動

```bash
cd ~/Desktop/daily-status
python3 -m http.server 8080
# 瀏覽器開 http://localhost:8080
```

## 開發 / 改維度

請見 [`CLAUDE.md`](./CLAUDE.md)。
