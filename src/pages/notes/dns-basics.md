---
layout: ../../layouts/PostLayout.astro
title: 'DNS 運作原理筆記'
description: '從輸入網址到看到網頁，中間發生了什麼事？DNS 查詢流程完整記錄。'
pubDate: '2024-09-10'
section: notes
emoji: '📝'
tags: ['DNS', '網路', '基礎知識']
minutesRead: 4
---

每次設定 DNS 都要重新查一遍，乾脆整理成筆記備查。

## DNS 是什麼

Domain Name System，把人類看得懂的域名（`chinnow.live`）翻譯成電腦看得懂的 IP 位址（`104.21.xxx.xxx`）。

## 查詢流程

當你在瀏覽器輸入 `chinnow.live`：

1. **瀏覽器快取** — 先看自己有沒有記過這個域名
2. **作業系統快取** — 問本機的 `/etc/hosts` 和 DNS 快取
3. **Recursive Resolver** — 通常是 ISP 提供的，或 `8.8.8.8`（Google）、`1.1.1.1`（Cloudflare）
4. **Root Nameserver** — 全球只有 13 組，知道誰負責 `.live` 這個 TLD
5. **TLD Nameserver** — 知道 `chinnow.live` 的 Authoritative NS 在哪裡
6. **Authoritative Nameserver** — 最終答案在這裡，回傳 IP

## 常見 DNS 記錄類型

| 記錄 | 用途 |
|------|------|
| A | 域名 → IPv4 |
| AAAA | 域名 → IPv6 |
| CNAME | 域名 → 另一個域名 |
| MX | 郵件伺服器 |
| TXT | 文字資訊（驗證、SPF 等） |
| NS | 指定 Nameserver |

## 為什麼 DNS 變更需要等待

每筆 DNS 記錄都有 TTL（Time To Live），單位是秒。TTL = 3600 代表快取保留 1 小時。

這段時間內，各地的 DNS 伺服器仍會回傳舊的記錄。所以 DNS 變更最多可能需要 48 小時全球生效。

## Cloudflare 的 CNAME Flatten

一般來說，根域名（`@`，即 `chinnow.live`）不能用 CNAME，只能用 A record。

Cloudflare 的 CNAME Flatten 功能自動把 CNAME 解析成 IP，讓根域名也能指向 GitHub Pages。

這就是為什麼不需要知道 GitHub Pages 的 IP，直接設 CNAME 就行。
