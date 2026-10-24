# DSH 科技新闻每日归档

由 GitHub Actions 每天 23:05（北京时间）自动抓取 14 个 RSS 源，把快照提交到 `archive/<日期>.json`。

**为什么要这个仓库**：RSS 只保留最近 20–60 条，一周前的内容会被挤掉，所以周报要覆盖完整 7 天就必须每天留快照。本仓库跑在 GitHub 的机器上，**不依赖你本机开机**。

## 数据格式

每份快照：

```json
{
  "generatedAt": "2026-10-24T15:05:12.000Z",
  "targetDate": "2026-10-24",
  "uniqueItems": [ "…当日窗口内的条目…" ],
  "allItems":    [ "…本次抓到的全部条目（约回溯 1–3 天）…" ],
  "stats": { "…": "…" }
}
```

`allItems` 是关键：即使某天没抓到，后一份快照也能补出前一天。

## 本地怎么用

```bash
# 拉取最近 7 天的快照到本地归档目录
node scripts/archive-pull.mjs --days=7

# 合并成周报素材
node scripts/archive-merge.mjs --days=7 --digest --max=6
```

## 手动补抓

Actions → archive → Run workflow。想补某一天，用 `daily-collect.mjs --date=YYYY-MM-DD --archive` 本地跑一次再提交即可。
