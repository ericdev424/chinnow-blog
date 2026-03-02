---
layout: ../../layouts/PostLayout.astro
title: '用 Astro + GitHub Pages 建立自己的部落格'
description: '記錄從零開始建立這個部落格的完整過程，包含 Astro 設定、GitHub Actions 自動部署、Cloudflare DNS 配置。'
pubDate: '2024-01-15'
section: tech
emoji: '🚀'
tags: ['Astro', 'DevOps']
minutesRead: 8
---

## 為什麼選擇 Astro？

一直想有一個自己的地方，可以隨手記下學到的東西。試過很多平台 —— Medium、Notion、HackMD —— 但總覺得不夠「自己的」。

最後選擇了 **Astro**，原因很簡單：靜態輸出、支援 Markdown、零 JavaScript by default。

## 架構

```
開發 → git push → GitHub Actions → GitHub Pages → Cloudflare CDN → chinnow.live
```

沒有 Server，沒有資料庫，純靜態。維護成本幾乎是零。

## 心得

建這個部落格花了一個週末。比起用現成平台，自己搭的感覺就是不一樣。
