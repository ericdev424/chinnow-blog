---
layout: ../../layouts/PostLayout.astro
title: 'Cloudflare + GoDaddy 域名設定筆記'
description: '把 GoDaddy 的 Nameservers 轉移到 Cloudflare，設定 CNAME 指向 GitHub Pages，全程記錄。'
pubDate: '2024-01-20'
tags: ['技術', 'DNS', 'Cloudflare']
minutesRead: 5
---

## 背景

買了 `chinnow.live` 之後，想把 DNS 交給 Cloudflare 管理，享受免費的 CDN 加速與 SSL。

## 步驟

### 1. 在 Cloudflare 新增網站

登入後選 **Add Site**，輸入域名，選 Free 方案。Cloudflare 會給你兩個 Nameservers。

### 2. 回 GoDaddy 換 NS

**我的域名 → DNS → Nameservers → 輸入我自己的 nameservers**

填入 Cloudflare 給的兩個 NS，儲存。等待生效（通常 30 分鐘內）。

### 3. Cloudflare 新增 DNS 記錄

| Type | Name | Content |
|------|------|---------|
| CNAME | @ | 你的帳號.github.io |
| CNAME | www | 你的帳號.github.io |

Proxy status 開啟（橘色雲朵）。

### 4. SSL 設定

**SSL/TLS → Full**，然後開啟 **Always Use HTTPS**。

## 踩坑記錄

- CNAME Flatten：Cloudflare 支援 root domain 用 CNAME，不需要改成 A record
- GitHub Pages custom domain：記得在 Repo Settings → Pages 填入自訂域名，不然會 404
- SSL 憑證：選 Full 而非 Flexible，否則可能出現重定向迴圈

## 結果

設定完成後，`chinnow.live` 正常上線，HTTPS 自動，Cloudflare 報告顯示有快取命中。

整個過程大約花了 1 小時（等 DNS 生效佔了大半時間）。
